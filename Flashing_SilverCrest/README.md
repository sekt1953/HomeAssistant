# Flashing SilverCrest Zigbee Gateway

I første del af vejlingen som jeg linker til er der et afsnit "Retrieve Root Password", her valgte jeg at monterer 3 stk dupoint connector til at forbindelse til TTL-adapteren, de kan blive efter opsætningen, så er de der hvis der kommer nyt software.

| Gateway    | TTL-adapteren |
|:---:       |:---:          |
| Serial TX  | RX            |
| Serial RX  | TX            |
| GND        | GND           |

## !! Husk at Serial til TTL adapteren skal være sat til 3,3V

## Serial Terminal Settings

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

## Decryptering

For at kunne få held med decryptering, skal der instaleres lidt hjælpe værktøjer på min Linux PC, [vejledning fundet her:](https://stackoverflow.com/questions/11596839/installing-pycrypto-on-ubuntu-fatal-error-on-build),
 komandoerne vist herunder:

```code
sudo apt-get install python3.8-dev
pip install pycrypto
```

For resten af vejen [følg denne vejledning](https://zigbee.blakadder.com/Lidl_TYGWZ-01.html), god fornøjelse.
