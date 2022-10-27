# TODO

# 参考

📚 TCP/IP Guide https://explained-from-first-principles.com/internet

🔍 https://networkengineering.stackexchange.com/

## standing

https://www.youtube.com/watch?v=dV8mjZd1OtU
https://www.youtube.com/watch?v=F5rni9fr1yE
https://www.youtube.com/watch?v=37AFBZv4_6Y

spur to refactor
* view outgoing requests by domain
* was looking for HTTP, but running git clone
* given HTTPS, able to group requests 1 id domain's IP addr from SNI 2 group req/res using IP addr?

work through
* https://sirupsen.com/napkin/problem-15
* https://robertovitillo.com/what-every-developer-should-know-about-tcp/
* https://lowlvl.org/
* TCP-IP Ilustrated 2.3.2
* https://www.youtube.com/watch?v=z07HTSzzp3o
* https://realpython.com/python-ipaddress-module/
* https://jvns.ca/blog/2018/07/24/ip-addresses-routing/ 
* diff btw TCP and IP https://www.joelonsoftware.com/2002/11/11/the-law-of-leaky-abstractions/

foundational
* https://eater.net/inet
* https://wizardzines.com/zines/bite-size-networking/

## queue

## done

# IP

📙 Sanders packet analysis (ch 6)

* ASN, last mile https://chown.me/blog/getting-my-own-asn
* anonymization https://news.ycombinator.com/item?id=30002882
* https://news.ycombinator.com/item?id=26632178
* history https://www.potaroo.net/ispcol/2018-06/10years.html
* map IP to geography https://calpaterson.com/latency.html

request spoofing
* how to: Fiddler, Scapy
* use case: bypass client-side validation to see if server still validates
* use case: send request from invalid IP address to see if safelist catches
* spoof HTTP req https://stackoverflow.com/a/57503789/6813490

## addresses

* _address_: ID for network node; either 32 bit (IPV4; 4 billion adddresses) or 128 (IPV6; lot more; not widely supported by cloud vendors https://news.ycombinator.com/item?id=24058792) https://blog.apnic.net/2019/08/23/what-can-you-learn-from-an-ip-address
* _DHCP_: assign unique address to each node https://www.raspberrypi.org/learning/networking-lessons/lesson-3/plan/) 🗄 `practical-packet-analysis.pdf` chapter 7
* _NAT (network address translation)_: map private addresses (from LAN) to public address used by router (from ISP); implemented using routing tables, set up using iptables and inspected using iproute2 https://jvns.ca/blog/2018/03/05/things-ive-learned-networking/

* _subnet_: section of network e.g. `192.168.0.0` vs. `192.168.1.0`
* _subnet mask_: delineates between network and host portions

* _nslookup_: lookup domain's IP address
* _ifconfig_: figure out your own IP address https://jvns.ca/blog/2018/03/05/things-ive-learned-networking/

## packet

🗄 `evans-networking-ack.pdf` page 4

🗄 `practical-packet-analysis.pdf` chapters 1

how they work
* _packets_: headers = sections -> ethernet (MAC address of computer that forward packet to current recipient) IP (addr of machine where packet is heading) HTTP (actually data you are trying to send) [`evans-linux.pdf` 15]
* how Linux handles packets https://jvns.ca/blog/2018/03/05/things-ive-learned-networking/
* _MTU_: when packets get too big https://www.youtube.com/watch?v=Y6IMlPSl4fI https://jvns.ca/blog/2018/03/05/things-ive-learned-networking/

tools - inspect
* _Fiddler_: app layer only
* _Wireshark_: https://bsago.me/blog/waltzing-with-wireshark https://jvns.ca/blog/2018/06/19/what-i-use-wireshark-for https://jvns.ca/blog/2016/03/16/tcpdump-is-amazing/ https://news.ycombinator.com/item?id=30743141
* intercept outgoing requests https://httptoolkit.tech/
* packets to csv, dataframes https://github.com/aouinizied/nfstream

tools - capture
* _tcpdump_: `sudo tcpdump src port 80 or dst port 80 -w output.pcap` https://jvns.ca/blog/2016/03/16/tcpdump-is-amazing/ https://hackertarget.com/tcpdump-examples/ syntax is called 'pcap filters' https://jvns.ca/blog/2016/03/16/tcpdump-is-amazing capture outgoing HTTP requests https://stackoverflow.com/questions/4777042/can-i-use-tcpdump-to-get-http-requests-response-header-and-response-body
* _tcpflow_: 
* _dumpcap_: https://kushaldas.in/posts/tracking-my-phone-s-silent-connections.html
* _BPF_: low level tool to filter packets https://jvns.ca/blog/2017/06/28/notes-on-bpf---ebpf/ https://www.pearson.com/us/higher-education/program/Gregg-BPF-Performance-Tools/PGM2760714.html

---

* _Burp_: HTTP proxy to intercept requests, pen test scans, automation of common attacks like XSS and SQL injection; OSS alternative https://github.com/dstotijn/hetty
* _netcat_: https://stackoverflow.com/a/4777309/6813490 https://blog.ikuamike.io/posts/2021/netcat/
* _socat_: https://stackoverflow.com/a/4777309/6813490 https://jvns.ca/blog/2018/03/05/things-ive-learned-networking/
* _nmap_: check if anything listening on port
* _sink_: https://github.com/imsnif/bandwhich https://robertheaton.com/2020/02/05/wacom-drawing-tablets-track-name-of-every-application-you-open/ https://github.com/rhaidiz/broxy https://news.ycombinator.com/item?id=22394708

# ZA

models
* _OSI_: lost irl https://security.stackexchange.com/a/93338 📙 TCP-IP Ilustrated 1.2.1
* 🗄 `destroy-all-software-protocols.pdf` https://jvns.ca/blog/2021/05/11/what-s-the-osi-model-/
* DARPA/TCP-IP https://twobithistory.org/2021/03/08/arpanet-protocols.html https://twobithistory.org/2021/02/07/arpanet.html
* avian protocol https://datatracker.ietf.org/doc/html/rfc1149

---

* nc/netcat: check if TCP/UDP port is open
* _tc_: add network latency
* _ARP_: 🗄 `practical-packet-analysis.pdf` chapter 6
* _DMZ_: public-facing part of network https://en.wikipedia.org/wiki/DMZ_(computing)
* _ICMP_: protocol for routers; used by ping to see if you can get a response from a server https://hacker-tools.github.io/machine-introspection/ https://jvns.ca/blog/2018/03/05/things-ive-learned-networking/  🗄 `practical-packet-analysis.pdf` chapter 6
* ping alternative: gping https://github.com/ibraheemdev/modern-unix
* _ISP_: people who own the wires https://news.ycombinator.com/item?id=22511417 BYO https://startyourownisp.com/ Starlink https://news.ycombinator.com/item?id=26760735 https://news.ycombinator.com/item?id=27919015
> The simplest way to look at Starlink is to consider what costs it's avoiding. A typical ISP needs to run physical wires to physical houses, which requires an upfront expense. When Google was rolling out its fiber service, for example, researchers at Bernstein estimated that it was costing $564 per home just to pass homes so they'd be eligible for a connection, and another $464 to $794 to connect them. As a result of this, the industry tends to be concentrated: if one company passes a set of homes, it can name its own price; two companies can split the market; a third company has to pay the same capital expenditures but gets lower incremental returns. So most US households have little choice when they buy Internet service https://diff.substack.com/p/three-bull-cases-for-starlink
* _UDP_: don't have to establish connection before message sent, msg not acked i.e. unreliable; used by streaming audio/video https://wsvincent.com/tcp-vs-udp/ https://hpbn.co/building-blocks-of-udp/
* `127.0.0.1`: IP addr that only receives connections from same host; aka 'locahost' https://stackoverflow.com/a/20778887 [`evans-tcpdump.pdf` page 8] 🗄 `/etc/hosts` 
* use 127.0.0.1 bc localhost stills need to be resolved by hosts file https://stackoverflow.com/q/7382602
* `0.0.0.0`: IP addr that means "listen on every available network interface"; lets server receive req coming from outside os https://stackoverflow.com/a/20778887 

## TCP

🗄 `practical-packet-analysis.pdf` chapter 6

* _TCP_: one-to-one communication btw two nodes, have to establish connection before msg sent, msg acked i.e. reliable; can arrive in wrong order but works out somehow
* _connection settings_: https://jvns.ca/blog/2018/03/05/things-ive-learned-networking/
* _sink_: https://robertovitillo.com/what-every-developer-should-know-about-tcp/ https://blog.erratasec.com/2019/02/a-basic-question-about-tcp.html#.XHaBq1NKgWo https://robertheaton.com/2018/08/31/how-to-build-a-tcp-proxy-1/ https://hpbn.co/building-blocks-of-tcp/
> If you’re sending the same data from one machine to 30 others, with normal unicast connections like TCP you’d need to send 30 copies. This takes quite a lot of bandwidth. With multicast you can send just one copy of the data, no matter how many machines you’re sending to. - 搜 Itamar Turner-Trauring, 'software clown'
