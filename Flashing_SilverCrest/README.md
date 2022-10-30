# SilverCrest Zigbee Gateway using Ubuntu 20.04LTS

## Kilde

* [zigbee.blakadder.com](https://zigbee.blakadder.com/Lidl_TYGWZ-01.html)
* [paulbanks.org](https://paulbanks.org/projects/lidl-zigbee/ha/)
* [lidl-gateway-freedom](https://github.com/banksy-git/lidl-gateway-freedom "Ny Software")
* [SSH returns: no matching host key type found. Their offer: ssh-dss](https://askubuntu.com/questions/836048/ssh-returns-no-matching-host-key-type-found-their-offer-ssh-dss)

## Klargør pc

### TTY access to Gateway

I første del af vejlingen som jeg linker til er der et afsnit "Retrieve Root Password", her valgte jeg at monterer 3 stk dupoint connector til at forbindelse til TTL-adapteren, de kan blive efter opsætningen, så er de der hvis der kommer nyt software.

| Gateway    | TTL-adapteren |
|:---:       |:---:          |
| Serial TX  | RX            |
| Serial RX  | TX            |
| GND        | GND           |

#### !! Husk at Serial til TTL adapteren skal være sat til 3,3V

#### Serial Terminal Settings

Serial_adapteren skal snakke med en tty terminal, her har jeg valgt at bruge Putty for Linux. Med Putty er det nemt at sætte de rigtiǵe indstillinger for samtalen, her er mine valg:

```txt
Settings: 
    Windows -> Font -> Font used for ordinary text ->
        Client: Ubuntu Mono 16
    Connection -> Serial ->
        Serial line to connect to: /dev/ttyUSB0
    Configure teh serial line ->
        Speed:          38400
        Data bits:      8
        Stop bits:      1
        Parity:         None
        Flow control:   None
    Session ->
        Saved session:  LidlGateway     
```

#### Decryptering software for ubuntu 20.04LTS

For at kunne få held med decryptering, skal der instaleres lidt hjælpe værktøjer på min Linux PC, [vejledning fundet her:](https://stackoverflow.com/questions/11596839/installing-pycrypto-on-ubuntu-fatal-error-on-build),
 komandoerne vist herunder:

```code
sudo apt-get install python3.8-dev
pip install pycrypto
```

### Now I clone [banksy-git/lidl-gateway-freedom](https://github.com/banksy-git/lidl-gateway-freedom)

```code
cd ~/
git clone git@github.com:banksy-git/lidl-gateway-freedom.git
```

### Copy files from script directory to my work direktory:

```code
mkdir ~/lidl-gateway-freedom/SEKT1
cd ~/lidl-gateway-freedom/SEKT1
cp ~/lidl-gateway-freedom/scripts/lidl_auskey_decode.py ./
cp ~/lidl-gateway-freedom/scripts/upgrade_ncp.py ./
```

### Download files for for EZSP upgrade

vi skal bruge 3 filer for upgrade

* [firmware_upgrade.sh](https://github.com/Ordspilleren/lidl-gateway-freedom/blob/master/scripts/firmware_upgrade.sh)  
* [sx](https://github.com/Ordspilleren/lidl-gateway-freedom/blob/master/scripts/sx)  
* [NCP_UHW_MG1B232_678_PA0-PA1-PB11_PA5-PA4.gbl](https://github.com/grobasoz/zigbee-firmware/raw/master/EFR32%20Series%201/EFR32MG1B-256k/NCP/NCP_UHW_MG1B232_678_PA0-PA1-PB11_PA5-PA4.gbl)  

Make sure the script **firmware_upgrade.sh** is executable:

```code
chmod +x ./firmware_upgrade.sh
```

### I run into problem after upgrading my Ubuntu from 18.04LTS to 20.04LTS

To get around the problem I did change all SSH command to include an -o option

```txt
-o option
    Can be used to give options in the format used in the configuration file.  This is useful for specifying options for
    which there is no separate command-line flag.  For full details of the options listed below, and their possible values,
    see ssh_config(5).
```

So they came to look like these:

```txt
ssh -p2333 -oHostKeyAlgorithms=+ssh-dss root@192.168.0.231
ssh -oHostKeyAlgorithms=+ssh-dss root@192.168.0.231
```

and the file firmware_upgrade.sh is change, there are 3 line to change:  

From:

```txt
#!/bin/bash
GATEWAY_HOST="$1"
SSH_PORT="$2"
FIRMWARE_FILE="$4"
EZSP_VERSION="$3"
CONFIGURATION_FRAME="\x00\x42\x21\xA8\x53\xDD\x4F\x7E"

if [ $EZSP_VERSION = "V8" ]; then
  CONFIGURATION_FRAME="\x00\x42\x21\xA8\x5C\x2C\xA0\x7E"
fi

cat sx | ssh -p${SSH_PORT} root@${GATEWAY_HOST} "cat > /tmp/sx"
cat ${FIRMWARE_FILE} | ssh -p${SSH_PORT} root@${GATEWAY_HOST} "cat > /tmp/firmware.gbl"

ssh -p${SSH_PORT} root@${GATEWAY_HOST} "
chmod +x /tmp/sx
killall -q serialgateway
stty -F /dev/ttyS1 115200 cs8 -cstopb -parenb -ixon crtscts raw
echo -en '\x1A\xC0\x38\xBC\x7E' > /dev/ttyS1
echo -en '$CONFIGURATION_FRAME' > /dev/ttyS1
echo -en '\x81\x60\x59\x7E' > /dev/ttyS1
echo -en '\x7D\x31\x43\x21\x27\x55\x6E\x90\x7E' > /dev/ttyS1
stty -F /dev/ttyS1 115200 cs8 -cstopb -parenb -ixon -crtscts raw
echo -e '1' > /dev/ttyS1
/tmp/sx /tmp/firmware.gbl < /dev/ttyS1 > /dev/ttyS1
reboot
"

echo "Successfully flashed new EZSP firmware! The device will now reboot."
```

To:

```txt
#!/bin/bash
GATEWAY_HOST="$1"
SSH_PORT="$2"
FIRMWARE_FILE="$4"
EZSP_VERSION="$3"
CONFIGURATION_FRAME="\x00\x42\x21\xA8\x53\xDD\x4F\x7E"

if [ $EZSP_VERSION = "V8" ]; then
  CONFIGURATION_FRAME="\x00\x42\x21\xA8\x5C\x2C\xA0\x7E"
fi

cat sx | ssh -p${SSH_PORT} -oHostKeyAlgorithms=+ssh-dss root@${GATEWAY_HOST} "cat > /tmp/sx"
cat ${FIRMWARE_FILE} | ssh -p${SSH_PORT} -oHostKeyAlgorithms=+ssh-dss root@${GATEWAY_HOST} "cat > /tmp/firmware.gbl"

ssh -p${SSH_PORT} -oHostKeyAlgorithms=+ssh-dss root@${GATEWAY_HOST} "
chmod +x /tmp/sx
killall -q serialgateway
stty -F /dev/ttyS1 115200 cs8 -cstopb -parenb -ixon crtscts raw
echo -en '\x1A\xC0\x38\xBC\x7E' > /dev/ttyS1
echo -en '$CONFIGURATION_FRAME' > /dev/ttyS1
echo -en '\x81\x60\x59\x7E' > /dev/ttyS1
echo -en '\x7D\x31\x43\x21\x27\x55\x6E\x90\x7E' > /dev/ttyS1
stty -F /dev/ttyS1 115200 cs8 -cstopb -parenb -ixon -crtscts raw
echo -e '1' > /dev/ttyS1
/tmp/sx /tmp/firmware.gbl < /dev/ttyS1 > /dev/ttyS1
reboot
"

echo "Successfully flashed new EZSP firmware! The device will now reboot."
```

## Now to the fun part: Retrieve Root Password

### Reading the key-encryption-key (KEK)

```code
FLR 80.000.000 401802 16
DW 80.000.000 4
```

Result:

```txt
80000000:      6672794E       7360263D       7968244E       34312653
```

### Read the encrypted AUSKEY

```code
FLR 80000000 402002 32
DW 80000000 8
```

Result:FLR

```txt
<RealTek>DW 80000000 8
80000000:      60DA8E0F       1EC0C493       9B17224A       8AEC396A
80000010:      008B85CC       B18438B5       052495AF       2D0DFB1D
```

## DECODE: 

### Run **lidl_auskey_decode.py** in terminal 

```code
cd ~/lidl-gateway-freedom/SEKT
```

### Åben terminal and run code

```code
python3 lidl_auskey_decode.py
```

Enter KEK hex string line>80000000:

```txt
75577563 75607230 3F66663C 7B24752D
```

Encoded aus-key as hex string line 1>80000000:

```txt
3C0B56A3 D9FACE44 E316B71C AE05DBB7
```

Encoded aus-key as hex string line 2>80000010:

```txt
3057C8F8 8F06B84F E9CE570A F6576F34
```

Auskey: WX8MCRKNNw3wZH6FLCbiXVcAasrk3w0L
Root password: asrk3w0L

## Customise running software on the gateway

This section must be run on Linux or WSL (Or any Bash like shell)

### Run from your host PC

SSH into your gateway with the username root and the password you decoded earlier, the SSH server will be running on port **2333** and run the following

* Note!! If [SSH returns: no matching host key type found. Their offer: ssh-dss](https://askubuntu.com/questions/836048/ssh-returns-no-matching-host-key-type-found-their-offer-ssh-dss)

SSH login as root:  asrk3w0L

```code
ssh -p2333 -oHostKeyAlgorithms=+ssh-dss root@192.168.0.231
```

### Run when logind to gateway

```code
if [ ! -f /tuya/ssh_monitor.original.sh ]; then cp /tuya/ssh_monitor.sh /tuya/ssh_monitor.original.sh; fi
echo "#!/bin/sh" >/tuya/ssh_monitor.sh
reboot
```

SSH Port is now change from 2333 to 22  

### Run from your host PC

Upload new [serialgateway.bin](https://paulbanks.org/download/files/lidl-zigbee/serialgateway.bin)

```code
cd ~/Dokumenter/Github/lidl-gateway-freedom/scripts
```

### Åben terminal and run code

```code
cat serialgateway.bin | ssh -oHostKeyAlgorithms=+ssh-dss root@192.168.0.231 "cat >/tuya/serialgateway"
```

SSH login as root:  asrk3w0L

```code
ssh -oHostKeyAlgorithms=+ssh-dss root@192.168.0.231
```

### Run the following on the Gateway

```code
if [ ! -f /tuya/tuya_start.original.sh ]; then cp /tuya/tuya_start.sh /tuya/tuya_start.original.sh; fi

cat >/tuya/tuya_start.sh <<EOF
#!/bin/sh
/tuya/serialgateway &
EOF
chmod 755 /tuya/serialgateway

reboot
```

## Upgrade the EZSP Version to 6.7.8.0

This section must be run on Linux or WSL (Or any Bash like shell)

### Run from your host PC

```code
chmod +x ./firmware_upgrade.sh
```

NB!! You may be prompted for the root password several times, when running next script.  

```code
./firmware_upgrade.sh [192.168.0.231] 22 V7 NCP_UHW_MG1B232_678_PA0-PA1-PB11_PA5-PA4.gbl
```

## For Home Assistant (ZHA)

* In Home Assistant (requires version 0.113+) go to 
  * Settings - Device & Service, 
    * click the [+ ADD INTEGRATION], 
      * search for ZHA integration and select: **Zigbee Home Automation**, 
    * for Radio Type choose **“EZSP”**

|+ ADD INTEGRATION|Radio Type|
|:---:|:---:|
|![](./Images/Sk%C3%A6rmbillede%20fra%202022-10-30%2018-13-41.png)|![](./Images/Sk%C3%A6rmbillede%20fra%202022-10-30%2018-14-00.png)|

* Under Serial device path enter 
  * **socket://[gateway_ip]:8888** replacing [gateway_ip] with its IP address.
    * NB!! Do not use hostnames.
  * Set port speed to “115200”

|Port Settings|Select Network Option|
|:---:|:---:|
|![](./Images/Sk%C3%A6rmbillede%20fra%202022-10-30%2018-17-40.png)|![](./Images/Sk%C3%A6rmbillede%20fra%202022-10-30%2018-18-13.png)|

* Select an Area

|Finish|
|:---:|
|![](./Images/Sk%C3%A6rmbillede%20fra%202022-10-30%2018-18-40.png)|

You are now up and running !!!!