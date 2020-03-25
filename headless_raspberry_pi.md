# Headless Raspberry Pi

1. Create image on microSD with raspbian (download from raspberry pi)

2. Configure SSH
* on a Mac in a terminal run `cd /Volumes/boot`
* create a SSH file: `touch ssh`

3. Configure Wifi to auto connect
* on a Mac in a terminal run `cd /Volumes/boot`
* vi wpa_supplicant.conf
* Populate with
```
country=AU # Your 2-digit country code
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
network={
    ssid="[YOUR WIFI SSID]"
    psk="[YOUR WIFI PASSWORD]"
    key_mgmt=WPA-PSK
}
```

4. Boot PI and ssh in
* on Mac termaninal run `ssh pi@raspberrypi.local` (or similar in your network)

5. Change PI hostname
* in PI terminal run `raspi-config`
* 2. Network Options -> N1 Hostname
