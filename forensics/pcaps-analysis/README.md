# Pcaps analysis

Start **searching** for **malware** inside the pcap. Use the **tools** mentioned in [**Malware Analysis**](../malware-analysis.md).

A note about PCAP vs PCAPNG: there are two versions of the PCAP file format; PCAPNG is newer and not supported by all tools. You may need to convert a file from PCAPNG to PCAP using Wireshark or another compatible tool, in order to work with it in some other tools.

## Online tools for pcaps

* If the header of your pcap is **broken** you should try to **fix** it using: [http://f00l.de/hacking/**pcapfix.php**](http://f00l.de/hacking/pcapfix.php)\*\*\*\*
* Extract **information** and search for **malware** inside a pcap in [**PacketTotal**](https://packettotal.com/)\*\*\*\*

## Basic Statistics

### Capinfos

```text
capinfos capture.pcap
```

### Wireshark

Inside wireshark you can see different **statistics** that could be useful. Some interesting http filters: [https://www.wireshark.org/docs/dfref/h/http.html](https://www.wireshark.org/docs/dfref/h/http.html)

If you want to **search** for **content** inside the **packets** of the sessions press _CTRL+f_  
You can add new layers to the main information bar _\(No., Time, Source...\)_ pressing _right bottom_ and _Edit Column_

[Some WireShark tricks here.](wireshark-tricks.md)

## Suricata

### Install and setup

```text
apt-get install suricata
apt-get install oinkmaster
echo "url = http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz" >> /etc/oinkmaster.conf
oinkmaster -C /etc/oinkmaster.conf -o /etc/suricata/rules
```

### Check pcap

```text
suricata -r packets.pcap -c /etc/suricata/suricata.yaml -k none -v -l log
```

## Ngrep

If you are **looking** for **something** inside the pcap you can use **ngrep**. And example using the main filters:

```text
ngrep -I packets.pcap "^GET" "port 80 and tcp and host 192.168 and dst host 192.168 and src host 192.168"
```

## Xplico Framework

Xplico can **analyze** a **pcap** and extract information from it. For example, from a pcap file Xplico extracts each email \(POP, IMAP, and SMTP protocols\), all HTTP contents, each VoIP call \(SIP\), FTP, TFTP, and so on.

### Install

```text
sudo bash -c 'echo "deb http://repo.xplico.org/ $(lsb_release -s -c) main" /etc/apt/sources.list'
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 791C25CE
sudo apt-get update
sudo apt-get install xplico
```

### Run

```text
/etc/init.d/apache2 restart
/etc/init.d/xplico start
```

Access to _**127.0.0.1:9876**_ with credentials _**xplico:xplico**_

Then create a **new case**, create a **new session** inside the case and **upload the pcap** file.

## NetworkMiner

Like Xplico it is a tool to analyze and extract objects from pcaps. It has a free edition that you can download [here](https://www.netresec.com/?page=NetworkMiner).

## Other pcap analysis tricks

* [DNSCat pcap analysis](dnscat-exfiltration.md)
* [USB Keyboard pcap analysis](usb-keyboard-pcap-analysis.md)

