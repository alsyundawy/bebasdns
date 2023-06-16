# How To Use Alternative Port
If the ISP is using a Transparent DNS Proxy, it will not be able to use **bebasdns** via Do53 IPv4/6.<br>
Let's spoof, by using an alternative port so we can use **bebasdns**.

### MikroTik

Copy and paste this script to the terminal:

``` 
/ip firewall nat add action=dst-nat chain=dstnat comment="BebasID DNS" dst-port=53 protocol=tcp to-addresses=147.139.211.126 to-ports=1753
/ip firewall nat add action=dst-nat chain=dstnat comment="BebasID DNS" dst-port=53 protocol=udp to-addresses=147.139.211.126 to-ports=1753
/ip firewall nat add action=dst-nat chain=dstnat comment="BebasID DNS" dst-port=53 protocol=tcp to-addresses=47.254.192.66 to-ports=1753
/ip firewall nat add action=dst-nat chain=dstnat comment="BebasID DNS" dst-port=53 protocol=udp to-addresses=47.254.192.66 to-ports=1753
```

<b>If the network supports IPv6 and MikroTik is already configured for IPv6 (RouterOS version 7 or higher):</b><br>
```
/ipv6 firewall nat add action=dst-nat chain=dstnat comment="BebasID DNS" dst-port=53 protocol=tcp to-address=2a06:1287:1605:5353::beba:51d to-ports=1753
/ipv6 firewall nat add action=dst-nat chain=dstnat comment="BebasID DNS" dst-port=53 protocol=udp to-address=2a06:1287:1605:5353::beba:51d to-ports=1753
```
<b>(Telkomsel, Indihome, XL Axiata, and Indosat are using <i>Transparent DNS Proxy</i> for their IPv6. Make sure that above scripts are running.)</b>

### GoodbyeDPI

**1. Choose ``2_any_country_dnsredir.cmd``, click Edit or open with __Notepad++__** *(If third-party program is available)*

![tutorialygy](https://media.discordapp.net/attachments/1059052464919298049/1107666667732992130/image.png)

**2. Add this part into ``start "" goodbyedpi.exe -5``**
>  --dns-addr 147.139.211.126 --dns-port 1753 --dnsv6-addr 2001:470:36:9be:ba5::1d --dnsv6-port 1753

![goodbyedpi](https://media.discordapp.net/attachments/1059052464919298049/1107664890761580574/image.png)

**3. Then, save ``2_any_country_dnsredir.cmd`` file.**

### Pi-Hole
**1. Add these lines to Custom DNS and enable them**

Custom 1 (IPv4): ``147.139.211.126#1753``

Custom 2 (IPv4): ``47.254.192.66#1753``

![Pi-Hole](https://media.discordapp.net/attachments/1059052464919298049/1059052488428372030/image.png)

**2. Then click save.**

### Check if the Configuration is running

**To make sure that the configuration is already running properly, open Command Prompt then type:**
```
nslookup lamanlabuh.aduankonten.id
```
![cek](https://media.discordapp.net/attachments/1059052464919298049/1107658636001542154/image.png)

If the result is either `0.0.0.0`, `127.0.0.1`, `::`, or `Server Failed`, **bebasdns** is already running and working properly.