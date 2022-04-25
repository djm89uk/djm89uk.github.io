# [Root-Me](./rootme.md) Root-Me Networks [16/26]

Investigate captured traffic, network services and perform packet analysis.

## Contents

1. [FTP - authentication](#ftp-authentication) 🗸
2. [TELNET - authentication](#telnet-authentication) 🗸
3. [ETHERNET - frame](#ethernet-frame) 🗸
4. [Twitter authentication](#twitter-authentication) 🗸
5. [Bluetooth - Unknown file](#bluetooth-unknown-file) 🗸
6. [CISCO - password](#cisco-password) 🗸
7. [DNS - zone transfert](#dns-zone-transfert) 🗸
8. [IP - Time To Live](#ip-time-to-live) 🗸
9. [LDAP - null bind](#ldap-null-bind) 🗸
10. [POP - APOP](#pop-apop) 🗸
11. [RF - AM Transmission](#rf-am-transmission) 🗸
12. [RF - FM Transmission](#rf-fm-transmission) 🗸
13. [SIP - authentication](#sip-authentication) 🗸
14. [ETHERNET - Patched transmission](#ethernet-patched-transmission) 🗸
15. [Global System Traffic for Mobile communication](#global-system-traffic-for-mobile-communication) 🗸
16. [HTTP - DNS Rebinding](#http-dns-rebinding)
17. [RF - Key Fixed Code](#rf-key-fixed-code) 🗸
18. [SSL - HTTP exchange](#ssl-http-exchange) 🗸
19. [Netfilter - common mistakes](#netfilter-common-mistakes)
20. [SNMP - Authentification](#snmp-authentification)
21. [Wired Equivalent Privacy](#wired-equivalent-privacy)
22. [ICMP payload](#icmp-payload)
23. [RIPv1 - no authentication](#ripv1-no-authentication)
24. [XMPP - authentication](#xmpp-authentication)
25. [RF - Satellite transmission](#rf-satellite-transmission)
25. [RF - L Band](#rf-l-band)

---

### [Networks](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## FTP Authentication

- Author: g0uZ
- Date: 30 August 2010
- Points: 5
- Level: 1

### Statement

An authenticated file exchange achieved through FTP. Recover the password used by the user.

### Related Resources

1. [RFC 959](https://repository.root-me.org/RFC/EN%20-%20rfc959.txt).

### Attachments

1. [ch1.pcap](http://challenge01.root-me.org/reseau/ch1/ch1.pcap) 276 kB.

### Solutions

<details>

<summary markdown="span">Solution</summary>

We are given a pcap file, [ch1.pcap](http://challenge01.root-me.org/reseau/ch1/ch1.pcap).  This file is unreadable with tcpdump, but can be read by tshark.  This details an authenticated file exchange through FTP.  We can review the packet summary using tshark:
 
~~~shell
$ tshark -r ch1.pcap -PQ
    1   0.000000 10.20.144.150 → 10.20.144.151 TCP 74 35974 → 21 [SYN] Seq=0 Win=32648 Len=0 MSS=1380 WS=1 TSval=1657560000 TSecr=0 35974 21 
    2   0.000320 10.20.144.151 → 10.20.144.150 TCP 78 21 → 35974 [SYN, ACK] Seq=0 Ack=1 Win=16384 Len=0 MSS=1356 WS=1 TSval=1657390000 TSecr=1657560000 21 35974 
    3   0.000570 10.20.144.150 → 10.20.144.151 TCP 66 35974 → 21 [ACK] Seq=1 Ack=1 Win=32648 Len=0 TSval=1657560000 TSecr=1657390000 35974 21 
    4   0.060630 10.20.144.151 → 10.20.144.150 FTP 106 Response: 220-QTCP at fran.csg.stercomm.com. 21 35974 
    5   0.275440 10.20.144.150 → 10.20.144.151 TCP 66 35974 → 21 [ACK] Seq=1 Ack=37 Win=32648 Len=0 TSval=1657560500 TSecr=1657390000 35974 21 
    6   0.275760 10.20.144.151 → 10.20.144.150 FTP 126 Response: 220 Connection will close if idle more than 5 minutes. 21 35974 
    7   0.276140 10.20.144.150 → 10.20.144.151 TCP 66 35974 → 21 [ACK] Seq=1 Ack=93 Win=32648 Len=0 TSval=1657560500 TSecr=1657390000 35974 21 
    8   4.216600 10.20.144.150 → 10.20.144.151 FTP 81 Request: USER cdts3500 35974 21 
    9   4.217350 10.20.144.151 → 10.20.144.150 FTP 91 Response: 331 Enter password. 21 35974 
   10   4.217630 10.20.144.150 → 10.20.144.151 TCP 66 35974 → 21 [PSH, ACK] Seq=16 Ack=114 Win=32648 Len=0 TSval=1657564500 TSecr=1657394000 35974 21 
   11   7.639420 10.20.144.150 → 10.20.144.151 FTP 81 Request: PASS cdts3500 35974 21 
   12   7.843260 10.20.144.151 → 10.20.144.150 TCP 70 21 → 35974 [PSH, ACK] Seq=114 Ack=31 Win=16384 Len=0 TSval=1657397500 TSecr=1657568000 21 35974 
   13   8.184000 10.20.144.151 → 10.20.144.150 FTP 95 Response: 230 CDTS3500 logged on. 21 35974 
   14   8.184360 10.20.144.150 → 10.20.144.151 TCP 66 35974 → 21 [PSH, ACK] Seq=31 Ack=139 Win=32648 Len=0 TSval=1657568500 TSecr=1657398000 35974 21 
   15   8.185040 10.20.144.150 → 10.20.144.151 FTP 72 Request: SYST 35974 21 
   16   8.185260 10.20.144.151 → 10.20.144.150 TCP 70 21 → 35974 [PSH, ACK] Seq=139 Ack=37 Win=16384 Len=0 TSval=1657398000 TSecr=1657568500 21 35974 
   17   8.192750 10.20.144.151 → 10.20.144.150 FTP 147 Response: 215  OS/400 is the remote operating system. The TCP/IP version is "V5R2M0". 21 35974 
   18   8.193000 10.20.144.150 → 10.20.144.151 TCP 66 35974 → 21 [PSH, ACK] Seq=37 Ack=216 Win=32648 Len=0 TSval=1657568500 TSecr=1657398000 35974 21 
   19   8.193570 10.20.144.150 → 10.20.144.151 FTP 80 Request: SITE NAMEFMT 35974 21 
   20   8.193780 10.20.144.151 → 10.20.144.150 TCP 70 21 → 35974 [PSH, ACK] Seq=216 Ack=51 Win=16384 Len=0 TSval=1657398000 TSecr=1657568500 21 35974 
   21   8.194900 10.20.144.151 → 10.20.144.150 FTP 105 Response: 250  Now using naming format "0". 21 35974 
   22   8.195140 10.20.144.150 → 10.20.144.151 TCP 66 35974 → 21 [PSH, ACK] Seq=51 Ack=251 Win=32648 Len=0 TSval=1657568500 TSecr=1657398000 35974 21 
   23   8.195700 10.20.144.150 → 10.20.144.151 FTP 71 Request: PWD 35974 21 
   24   8.195910 10.20.144.151 → 10.20.144.150 TCP 70 21 → 35974 [PSH, ACK] Seq=251 Ack=56 Win=16384 Len=0 TSval=1657398000 TSecr=1657568500 21 35974 
   25   8.197050 10.20.144.151 → 10.20.144.150 FTP 106 Response: 257 "CDTS3500" is current library. 21 35974 
   26   8.197280 10.20.144.150 → 10.20.144.151 TCP 66 35974 → 21 [PSH, ACK] Seq=56 Ack=287 Win=32648 Len=0 TSval=1657568500 TSecr=1657398000 35974 21 
   27  20.765720 10.20.144.150 → 10.20.144.151 FTP 72 Request: PASV 35974 21 
   28  20.766000 10.20.144.151 → 10.20.144.150 TCP 70 21 → 35974 [PSH, ACK] Seq=287 Ack=62 Win=16384 Len=0 TSval=1657410500 TSecr=1657581000 21 35974 
   29  20.787770 10.20.144.151 → 10.20.144.150 FTP 121 Response: 227 Entering Passive Mode (10,20,144,151,62,141). 21 35974 
   30  20.788010 10.20.144.150 → 10.20.144.151 TCP 66 35974 → 21 [PSH, ACK] Seq=62 Ack=338 Win=32648 Len=0 TSval=1657581000 TSecr=1657410500 35974 21 
   31  20.797560 10.20.144.150 → 10.20.144.151 TCP 74 35976 → 16013 [SYN] Seq=0 Win=32768 Len=0 MSS=1380 WS=1 TSval=1657581000 TSecr=0 35976 16013 
   32  20.797850 10.20.144.151 → 10.20.144.150 TCP 78 16013 → 35976 [SYN, ACK] Seq=0 Ack=1 Win=32768 Len=0 MSS=1356 WS=1 TSval=1657410500 TSecr=1657581000 16013 35976 
   33  20.798130 10.20.144.150 → 10.20.144.151 TCP 66 35976 → 16013 [ACK] Seq=1 Ack=1 Win=32768 Len=0 TSval=1657581000 TSecr=1657410500 35976 16013 
   34  20.798250 10.20.144.150 → 10.20.144.151 FTP 91 Request: RETR qgpl/apkeyf.apkeyf 35974 21 
   35  20.798450 10.20.144.151 → 10.20.144.150 TCP 70 21 → 35974 [PSH, ACK] Seq=338 Ack=87 Win=16384 Len=0 TSval=1657410500 TSecr=1657581000 21 35974 
   36  21.202190 10.20.144.151 → 10.20.144.150 FTP 132 Response: 150 Retrieving member APKEYF in file APKEYF in library QGPL. 21 35974 
   37  21.202460 10.20.144.150 → 10.20.144.151 TCP 66 35974 → 21 [PSH, ACK] Seq=87 Ack=400 Win=32648 Len=0 TSval=1657581500 TSecr=1657411000 35974 21 
   38  21.313290 10.20.144.151 → 10.20.144.150 FTP-DATA 509 FTP Data: 439 bytes (PASV) (RETR qgpl/apkeyf.apkeyf) 16013 35976 
   39  21.393980 10.20.144.151 → 10.20.144.150 TCP 70 16013 → 35976 [FIN, PSH, ACK] Seq=440 Ack=1 Win=32768 Len=0 TSval=1657411500 TSecr=1657581000 16013 35976 
   40  21.394160 10.20.144.151 → 10.20.144.150 FTP 113 Response: 250 File transfer completed successfully. 21 35974 
   41  21.394310 10.20.144.150 → 10.20.144.151 TCP 66 35976 → 16013 [ACK] Seq=1 Ack=441 Win=32768 Len=0 TSval=1657581500 TSecr=1657411500 35976 16013 
   42  21.394430 10.20.144.150 → 10.20.144.151 TCP 66 35974 → 21 [PSH, ACK] Seq=87 Ack=443 Win=32648 Len=0 TSval=1657581500 TSecr=1657411500 35974 21 
   43  22.169470 10.20.144.150 → 10.20.144.151 TCP 66 35976 → 16013 [FIN, PSH, ACK] Seq=1 Ack=441 Win=32768 Len=0 TSval=1657582500 TSecr=1657411500 35976 16013 
   44  22.169800 10.20.144.151 → 10.20.144.150 TCP 70 16013 → 35976 [PSH, ACK] Seq=441 Ack=2 Win=32768 Len=0 TSval=1657412000 TSecr=1657582500 16013 35976 
   45  31.007220 10.20.144.150 → 10.20.144.151 FTP 72 Request: QUIT 35974 21 
   46  31.007560 10.20.144.151 → 10.20.144.150 TCP 70 21 → 35974 [PSH, ACK] Seq=443 Ack=93 Win=16384 Len=0 TSval=1657421000 TSecr=1657591500 21 35974 
   47  31.007750 10.20.144.151 → 10.20.144.150 FTP 101 Response: 221 QUIT subcommand received. 21 35974 
   48  31.007830 10.20.144.151 → 10.20.144.150 TCP 70 21 → 35974 [FIN, PSH, ACK] Seq=474 Ack=93 Win=16384 Len=0 TSval=1657421000 TSecr=1657591500 21 35974 
   49  31.008000 10.20.144.150 → 10.20.144.151 TCP 66 35974 → 21 [PSH, ACK] Seq=93 Ack=474 Win=32648 Len=0 TSval=1657591500 TSecr=1657421000 35974 21 
   50  31.008810 10.20.144.150 → 10.20.144.151 TCP 66 35974 → 21 [FIN, PSH, ACK] Seq=93 Ack=474 Win=32648 Len=0 TSval=1657591500 TSecr=1657421000 35974 21 
   51  31.008840 10.20.144.150 → 10.20.144.151 TCP 66 35974 → 21 [PSH, ACK] Seq=94 Ack=475 Win=32648 Len=0 TSval=1657591500 TSecr=1657421000 35974 21 
   52  31.009050 10.20.144.151 → 10.20.144.150 TCP 70 21 → 35974 [PSH, ACK] Seq=475 Ack=94 Win=16384 Len=0 TSval=1657421000 TSecr=1657591500 21 35974 
   53  35.659010 10.20.144.150 → 10.20.144.151 TCP 74 35977 → 23 [SYN] Seq=0 Win=32648 Len=0 MSS=1380 WS=1 TSval=1657596000 TSecr=0 35977 23 
   54  35.659340 10.20.144.151 → 10.20.144.150 TCP 78 23 → 35977 [SYN, ACK] Seq=0 Ack=1 Win=16384 Len=0 MSS=1356 WS=1 TSval=1657425500 TSecr=1657596000 23 35977 
   55  35.659660 10.20.144.150 → 10.20.144.151 TCP 66 35977 → 23 [ACK] Seq=1 Ack=1 Win=32648 Len=0 TSval=1657596000 TSecr=1657425500 35977 23 
   56  35.660510 10.20.144.151 → 10.20.144.150 TELNET 76 Telnet Data ... 23 35977 
   57  35.713440 10.20.144.150 → 10.20.144.151 TELNET 69 Telnet Data ... 35977 23 
   58  35.713670 10.20.144.151 → 10.20.144.150 TELNET 76 Telnet Data ... 23 35977 
   59  35.740240 10.20.144.150 → 10.20.144.151 TELNET 69 Telnet Data ... 35977 23 
   60  35.740480 10.20.144.151 → 10.20.144.150 TELNET 95 Telnet Data ... 23 35977 
   61  35.740750 10.20.144.150 → 10.20.144.151 TELNET 82 Telnet Data ... 35977 23 
   62  35.740960 10.20.144.151 → 10.20.144.150 TELNET 82 Telnet Data ... 23 35977 
   63  35.741210 10.20.144.150 → 10.20.144.151 TCP 66 35977 → 23 [PSH, ACK] Seq=23 Ack=50 Win=32648 Len=0 TSval=1657596000 TSecr=1657426000 35977 23 
   64  35.741580 10.20.144.150 → 10.20.144.151 TELNET 108 Telnet Data ... 35977 23 
   65  35.945290 10.20.144.151 → 10.20.144.150 TCP 70 23 → 35977 [PSH, ACK] Seq=50 Ack=65 Win=16384 Len=0 TSval=1657426000 TSecr=1657596000 23 35977 
   66  35.945610 10.20.144.150 → 10.20.144.151 TELNET 78 Telnet Data ... 35977 23 
   67  35.945810 10.20.144.151 → 10.20.144.150 TCP 70 23 → 35977 [PSH, ACK] Seq=50 Ack=77 Win=16384 Len=0 TSval=1657426000 TSecr=1657596500 23 35977 
   68  36.350870 10.20.144.151 → 10.20.144.150 TN5250 145 TN5250 Data from Mainframe[Malformed Packet] 23 35977 
   69  37.136450 10.20.144.150 → 10.20.144.151 TCP 66 35977 → 23 [PSH, ACK] Seq=77 Ack=125 Win=32648 Len=0 TSval=1657597000 TSecr=1657426500 35977 23 
   70  37.140450 10.20.144.151 → 10.20.144.150 TN5250 573 TN5250 Data from Mainframe 23 35977 
   71  37.143150 10.20.144.150 → 10.20.144.151 TCP 66 35977 → 23 [PSH, ACK] Seq=77 Ack=628 Win=32648 Len=0 TSval=1657597000 TSecr=1657426500 35977 23 
   72  41.737360 10.20.144.150 → 10.20.144.151 TN5250 100 TN5250 Data to Mainframe 35977 23 
   73  41.737640 10.20.144.151 → 10.20.144.150 TCP 70 23 → 35977 [PSH, ACK] Seq=628 Ack=111 Win=16384 Len=0 TSval=1657432000 TSecr=1657602000 23 35977 
   74  41.964780 10.20.144.151 → 10.20.144.150 TN5250 89 TN5250 Data from Mainframe 23 35977 
   75  41.965040 10.20.144.150 → 10.20.144.151 TCP 66 35977 → 23 [PSH, ACK] Seq=111 Ack=647 Win=32648 Len=0 TSval=1657602500 TSecr=1657432000 35977 23 
   76  42.075290 10.20.144.150 → 10.20.144.151 TN5250 139 TN5250 Data to Mainframe 35977 23 
   77  42.075500 10.20.144.151 → 10.20.144.150 TCP 70 23 → 35977 [PSH, ACK] Seq=647 Ack=184 Win=16384 Len=0 TSval=1657432000 TSecr=1657602500 23 35977 
   78  42.076210 10.20.144.151 → 10.20.144.150 TN5250 82 TN5250 Data from Mainframe 23 35977 
   79  42.076530 10.20.144.150 → 10.20.144.151 TCP 66 35977 → 23 [PSH, ACK] Seq=184 Ack=659 Win=32648 Len=0 TSval=1657602500 TSecr=1657432000 35977 23 
   80  42.156700 10.20.144.151 → 10.20.144.150 TN5250 157 TN5250 Data from Mainframe 23 35977 
   81  42.156960 10.20.144.150 → 10.20.144.151 TCP 66 35977 → 23 [PSH, ACK] Seq=184 Ack=746 Win=32648 Len=0 TSval=1657602500 TSecr=1657432500 35977 23 
   82  42.179050 10.20.144.151 → 10.20.144.150 TN5250 233 TN5250 Data from Mainframe 23 35977 
   83  42.179310 10.20.144.150 → 10.20.144.151 TCP 66 35977 → 23 [PSH, ACK] Seq=184 Ack=909 Win=32648 Len=0 TSval=1657602500 TSecr=1657432500 35977 23 
   84  42.179570 10.20.144.151 → 10.20.144.150 TN5250 152 TN5250 Data from Mainframe 23 35977 
   85  42.179830 10.20.144.150 → 10.20.144.151 TCP 66 35977 → 23 [PSH, ACK] Seq=184 Ack=991 Win=32648 Len=0 TSval=1657602500 TSecr=1657432500 35977 23 
   86  43.279170 10.20.144.150 → 10.20.144.151 TN5250 81 TN5250 Data to Mainframe 35977 23 
   87  43.279500 10.20.144.151 → 10.20.144.150 TCP 70 23 → 35977 [PSH, ACK] Seq=991 Ack=199 Win=16384 Len=0 TSval=1657433500 TSecr=1657604000 23 35977 
   88  43.326260 10.20.144.151 → 10.20.144.150 TN5250 84 TN5250 Data from Mainframe 23 35977 
   89  43.326500 10.20.144.150 → 10.20.144.151 TCP 66 35977 → 23 [PSH, ACK] Seq=199 Ack=1005 Win=32648 Len=0 TSval=1657604000 TSecr=1657433500 35977 23 
   90  43.334860 10.20.144.151 → 10.20.144.150 TN5250 812 TN5250 Data from Mainframe 23 35977 
   91  43.335150 10.20.144.150 → 10.20.144.151 TCP 66 35977 → 23 [PSH, ACK] Seq=199 Ack=1747 Win=32648 Len=0 TSval=1657604000 TSecr=1657433500 35977 23 
   92  46.018550 10.20.144.150 → 10.20.144.151 TN5250 93 TN5250 Data to Mainframe 35977 23 
   93  46.018860 10.20.144.151 → 10.20.144.150 TCP 70 23 → 35977 [PSH, ACK] Seq=1747 Ack=226 Win=16384 Len=0 TSval=1657436000 TSecr=1657606500 23 35977 
   94  47.763420 10.20.144.151 → 10.20.144.150 TCP 1426 Telnet Data ... [TCP segment of a reassembled PDU] 23 35977 
   95  47.763550 10.20.144.151 → 10.20.144.150 TN5250 450 TN5250 Data from Mainframe 23 35977 
   96  47.763900 10.20.144.150 → 10.20.144.151 TCP 66 35977 → 23 [PSH, ACK] Seq=226 Ack=3103 Win=32648 Len=0 TSval=1657608500 TSecr=1657438000 35977 23 
   97  47.764010 10.20.144.150 → 10.20.144.151 TCP 66 35977 → 23 [PSH, ACK] Seq=226 Ack=3483 Win=32648 Len=0 TSval=1657608500 TSecr=1657438000 35977 23 
   98  49.806640 10.20.144.150 → 10.20.144.151 TN5250 81 TN5250 Data to Mainframe 35977 23 
   99  49.806870 10.20.144.151 → 10.20.144.150 TCP 70 23 → 35977 [PSH, ACK] Seq=3483 Ack=241 Win=16384 Len=0 TSval=1657440000 TSecr=1657610500 23 35977 
  100  49.825890 10.20.144.151 → 10.20.144.150 TN5250 729 TN5250 Data from Mainframe 23 35977 
  101  49.826140 10.20.144.150 → 10.20.144.151 TCP 66 35977 → 23 [PSH, ACK] Seq=241 Ack=4142 Win=32648 Len=0 TSval=1657610500 TSecr=1657440000 35977 23 
  102  53.784480 10.20.144.150 → 10.20.144.151 TCP 66 35977 → 23 [FIN, PSH, ACK] Seq=241 Ack=4142 Win=32648 Len=0 TSval=1657614500 TSecr=1657440000 35977 23 
  103  53.784750 10.20.144.151 → 10.20.144.150 TCP 70 23 → 35977 [PSH, ACK] Seq=4142 Ack=242 Win=16384 Len=0 TSval=1657444000 TSecr=1657614500 23 35977 
  104  53.791460 10.20.144.151 → 10.20.144.150 TCP 70 23 → 35977 [FIN, PSH, ACK] Seq=4142 Ack=242 Win=16384 Len=0 TSval=1657444000 TSecr=1657614500 23 35977 
  105  53.791680 10.20.144.150 → 10.20.144.151 TCP 66 35977 → 23 [PSH, ACK] Seq=242 Ack=4143 Win=32648 Len=0 TSval=1657614500 TSecr=1657444000 35977 23 
~~~
 
The FTP packets can be extracted to a new file using tshark:
 
~~~shell
$ tshark -r ch1.pcap -w ch1_ftp.pcap ftp
~~~
 
We can review the ftp pcap using tshark:

~~~shell
$ tshark -r ch1_ftp.pcap -PQ
    1   0.000000 10.20.144.151 → 10.20.144.150 FTP 106 Response: 220-QTCP at fran.csg.stercomm.com. 21 35974 
    2   0.215130 10.20.144.151 → 10.20.144.150 FTP 126 Response: 220 Connection will close if idle more than 5 minutes. 21 35974 
    3   4.155970 10.20.144.150 → 10.20.144.151 FTP 81 Request: USER cdts3500 35974 21 
    4   4.156720 10.20.144.151 → 10.20.144.150 FTP 91 Response: 331 Enter password. 21 35974 
    5   7.578790 10.20.144.150 → 10.20.144.151 FTP 81 Request: PASS cdts3500 35974 21 
    6   8.123370 10.20.144.151 → 10.20.144.150 FTP 95 Response: 230 CDTS3500 logged on. 21 35974 
    7   8.124410 10.20.144.150 → 10.20.144.151 FTP 72 Request: SYST 35974 21 
    8   8.132120 10.20.144.151 → 10.20.144.150 FTP 147 Response: 215  OS/400 is the remote operating system. The TCP/IP version is "V5R2M0". 21 35974 
    9   8.132940 10.20.144.150 → 10.20.144.151 FTP 80 Request: SITE NAMEFMT 35974 21 
   10   8.134270 10.20.144.151 → 10.20.144.150 FTP 105 Response: 250  Now using naming format "0". 21 35974 
   11   8.135070 10.20.144.150 → 10.20.144.151 FTP 71 Request: PWD 35974 21 
   12   8.136420 10.20.144.151 → 10.20.144.150 FTP 106 Response: 257 "CDTS3500" is current library. 21 35974 
   13  20.705090 10.20.144.150 → 10.20.144.151 FTP 72 Request: PASV 35974 21 
   14  20.727140 10.20.144.151 → 10.20.144.150 FTP 121 Response: 227 Entering Passive Mode (10,20,144,151,62,141). 21 35974 
   15  20.737620 10.20.144.150 → 10.20.144.151 FTP 91 Request: RETR qgpl/apkeyf.apkeyf 35974 21 
   16  21.141560 10.20.144.151 → 10.20.144.150 FTP 132 Response: 150 Retrieving member APKEYF in file APKEYF in library QGPL. 21 35974 
   17  21.333530 10.20.144.151 → 10.20.144.150 FTP 113 Response: 250 File transfer completed successfully. 21 35974 
   18  30.946590 10.20.144.150 → 10.20.144.151 FTP 72 Request: QUIT 35974 21 
   19  30.947120 10.20.144.151 → 10.20.144.150 FTP 101 Response: 221 QUIT subcommand received. 21 35974 
~~~

We can see packet 3 and 5 are the user name and password for the FTP session.  We can further extract the data to clarify:

~~~shell
$ tshark -r ch1_ftp.pcap -z follow,tcp,ascii,0 | grep PASS
    5   7.578790 10.20.144.150 → 10.20.144.151 FTP 81 Request: PASS cdts3500 35974 21 
PASS cdts3500
~~~

This gives the password cdts3500 which we can submit to solve this challenge.
  
</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
cdts3500
~~~

</details>

---

### [Networks](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## TELNET authentication

- Author: g0uZ
- Date: 30 August 2010
- Points: 5
- Level: 1

### Statement

Find the user password in this TELNET session capture.

### Related Resources

1. [RFC 854](https://repository.root-me.org/RFC/EN%20-%20rfc854.txt).

### Attachments

1. [ch2.pcap](http://challenge01.root-me.org/reseau/ch2/ch2.pcap) 23.8 kB.

### Solutions

<details>

<summary markdown="span">Solution</summary>

As with challenge 1, we are given a pcap file, [ch2.pcap](http://challenge01.root-me.org/reseau/ch2/ch2.pcap).  We can extract the TELNET packets using tshark:
 
~~~shell
$ tshark -r ch2.pcap -w ch2_telnet.pcap telnet
~~~

Using tcpflow, we can review the telnet conversations:
  
~~~shell
$ tcpflow -C -r ch2_telnet.pcap
reportfilename: ./report.xml
........... ..!.."..'.....#
..%
..%
........... ..!..".."....
....P. ....".....b........b.....B.
........................"....
..'.....#..&..&..$
..&..&..$
.. .....#.....'.........
.. .9600,9600....#.bam.zing.org:0.0....'..DISPLAY.bam.zing.org:0.0......xterm-color..
...
...
.....!......
......
.."............

OpenBSD/i386 (oof) (ttyp1)


login: 
.."...
...
.."
f
f
a
a
k
k
e
e
.


Password:
u
s
e
r
.


Last login: Thu Dec  2 21:32:59 on ttyp1 from bam.zing.org

Warning: no Kerberos tickets issued.

OpenBSD 2.6-beta (OOF) #4: Tue Oct 12 20:42:32 CDT 1999

Welcome to OpenBSD: The proactively secure Unix-like operating system.

Please use the sendbug(1) utility to report bugs in the system.
Before reporting a bug, please try to reproduce it with the latest
version of the code.  With bug reports, please try to ensure that
enough information to reproduce the problem is enclosed, and if a
known fix for it exists, include that as well.


$ 
l
l
s
s
.


$ 
l
l
s
s
 
 
-
-
a
a
.


.         ..        .cshrc    .login    .mailrc   .profile  .rhosts

$ 
/
/
s
s
b
b
i
i
n
n
/
/
p
p
i
i
n
n
g
g
 
 
w
w
w
w
w
w
.
.
y
y
a
a
h
h
o
o
o
o
.
.
c
c
o
o
m
m
.


PING www.yahoo.com (204.71.200.74): 56 data bytes

64 bytes from 204.71.200.74: icmp_seq=0 ttl=239 time=73.569 ms

64 bytes from 204.71.200.74: icmp_seq=1 ttl=239 time=71.099 ms

64 bytes from 204.71.200.74: icmp_seq=2 ttl=239 time=68.728 ms

64 bytes from 204.71.200.74: icmp_seq=3 ttl=239 time=73.122 ms

64 bytes from 204.71.200.74: icmp_seq=4 ttl=239 time=71.276 ms

64 bytes from 204.71.200.74: icmp_seq=5 ttl=239 time=75.831 ms

64 bytes from 204.71.200.74: icmp_seq=6 ttl=239 time=70.101 ms

64 bytes from 204.71.200.74: icmp_seq=7 ttl=239 time=74.528 ms

64 bytes from 204.71.200.74: icmp_seq=9 ttl=239 time=74.514 ms

64 bytes from 204.71.200.74: icmp_seq=10 ttl=239 time=75.188 ms

64 bytes from 204.71.200.74: icmp_seq=11 ttl=239 time=72.925 ms

.
.
.
.--- www.yahoo.com ping statistics ---
13 packets transmitted, 11 packets received, 15% packet loss
round-trip min/avg/max = 68.728/72.807/75.831 ms
$ 
e
e
x
x
i
i
t
t
.
~~~
  
We can see the TELNET username and password: 
- username: fake
- password: user
  
</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
user
~~~

</details>

---

### [Networks](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## ETHERNET Frame

- Author: abu_youssef
- Date: 20 May 2013
- Points: 10
- Level: 2

### Statement

Find the (supposed to be) confidential data in this ethernet frame.

### Related Resources

1. [RFC 1024](https://repository.root-me.org/RFC/EN%20-%20rfc1042.txt).
2. [HTTP Basic Authentication and Digest Authentication](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20HTTP%20basic%20authentication%20and%20digest%20authentication.pdf)

### Attachments

1. [ch12.txt](http://challenge01.root-me.org/reseau/ch12/ch12.txt) 628 B.

### Solutions

<details>

<summary markdown="span">Solution</summary>

We are given a text file, [ch12.txt](http://challenge01.root-me.org/reseau/ch12/ch12.txt) with 209 bytes encoded in hex:
  
~~~
00 05 73 a0 00 00 e0 69 95 d8 5a 13 86 dd 60 00
00 00 00 9b 06 40 26 07 53 00 00 60 2a bc 00 00
00 00 ba de c0 de 20 01 41 d0 00 02 42 33 00 00
00 00 00 00 00 04 96 74 00 50 bc ea 7d b8 00 c1
d7 03 80 18 00 e1 cf a0 00 00 01 01 08 0a 09 3e
69 b9 17 a1 7e d3 47 45 54 20 2f 20 48 54 54 50
2f 31 2e 31 0d 0a 41 75 74 68 6f 72 69 7a 61 74
69 6f 6e 3a 20 42 61 73 69 63 20 59 32 39 75 5a
6d 6b 36 5a 47 56 75 64 47 6c 68 62 41 3d 3d 0d
0a 55 73 65 72 2d 41 67 65 6e 74 3a 20 49 6e 73
61 6e 65 42 72 6f 77 73 65 72 0d 0a 48 6f 73 74
3a 20 77 77 77 2e 6d 79 69 70 76 36 2e 6f 72 67
0d 0a 41 63 63 65 70 74 3a 20 2a 2f 2a 0d 0a 0d
0a
~~~
 
We can convert this into ASCII to inspect the frame payload:
  
~~~py
import binascii
file_HEX = "000573a00000e06995d85a1386dd60000000009b06402607530000602abc00000000badec0de200141d000024233000000000000000496740050bcea7db800c1d703801800e1cfa000000101080a093e69b917a17ed3474554202f20485454502f312e310d0a417574686f72697a6174696f6e3a20426173696320593239755a6d6b365a47567564476c6862413d3d0d0a557365722d4167656e743a20496e73616e6542726f777365720d0a486f73743a207777772e6d79697076362e6f72670d0a4163636570743a202a2f2a0d0a0d0a"
file_ASCII = binascii.unhexlify(file_HEX)
print(file_ASCII)
~~~

This returns:
  
~~~
b'\x00\x05s\xa0\x00\x00\xe0i\x95\xd8Z\x13\x86\xdd`\x00\x00\x00\x00\x9b\x06@&\x07S\x00\x00`*\xbc\x00\x00\x00\x00\xba\xde\xc0\xde \x01A\xd0\x00\x02B3\x00\x00\x00\x00\x00\x00\x00\x04\x96t\x00P\xbc\xea}\xb8\x00\xc1\xd7\x03\x80\x18\x00\xe1\xcf\xa0\x00\x00\x01\x01\x08\n\t>i\xb9\x17\xa1~\xd3GET / HTTP/1.1\r\nAuthorization: Basic Y29uZmk6ZGVudGlhbA==\r\nUser-Agent: InsaneBrowser\r\nHost: www.myipv6.org\r\nAccept: */*\r\n\r\n'
~~~

We can see an "Authorization" field with "Basic" and a base64 string, Y29uZmk6ZGVudGlhbA==.  In python, we can decode this base64 into ascii:

~~~py
import base64 as b64
  
word_b64 = "Y29uZmk6ZGVudGlhbA=="
word_ASCII = b64.b64decode(word_b64).decode()
print(word_ASCII)
~~~

This provides the solution: confi:dential
  
</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
confi:dential
~~~

</details>

---

### [Networks](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---


## Twitter Authentication

- Author: g0uZ
- Date: 30 August 2010
- Points: 15
- Level: 2

### Statement

A twitter authentication session has been captured, you have to retrieve the password.

### Attachments

1. [ch3.pcap](http://challenge01.root-me.org/reseau/ch3/ch3.pcap) 558 B.

### Solutions

<details>

<summary markdown="span">Solution</summary>

We have been given a packet capture file, [ch3.pcap](http://challenge01.root-me.org/reseau/ch3/ch3.pcap).  We find a single packet has been captured:

~~~shell
$ tshark -r ch3.pcap
    1   0.000000 128.222.228.85 → 128.121.146.100 HTTP 518 GET /statuses/replies.xml HTTP/1.1  55872 80 
~~~

This is a HTTP GET request so we know it it an ip tcp packet.  We can extract the tcp payload using tshark:

~~~shell
$ tshark -r ch3.pcap -T fields -e tcp.payload > payload.txt
~~~

This gives us the packet data in hex within payload.txt:

~~~
474554202f73746174757365732f7265706c6965732e786d6c20485454502f312e310d0a557365722d4167656e743a2043464e6574776f726b2f3333300d0a436f6f6b69653a205f747769747465725f736573733d4241683743446f4a64584e6c636a413642326c6b4969566d5a4751324f4463354d544d774d5746684f5446694d5745785a4456695a6d51774d47457a25323530414f574e6b4d79494b5a6d78686332684a517a6f6e51574e30615739755132397564484a766247786c636a6f36526d7868633267364f6b5a7359584e6f25323530415347467a61487341426a6f4b5148567a5a5752374141253235334425323533442d2d656131326537626330393064303532303263643765336639373263326234343134613937663635370d0a4163636570743a202a2f2a0d0a4163636570742d4c616e67756167653a20656e2d75730d0a4163636570742d456e636f64696e673a20677a69702c206465666c6174650d0a417574686f72697a6174696f6e3a2042617369632064584e6c636e526c633351366347467a63336476636d513d0d0a436f6e6e656374696f6e3a206b6565702d616c6976650d0a486f73743a20747769747465722e636f6d0d0a0d0a
~~~

We can use python to convert this into ASCII:
 
~~~py
import binascii

payload_HEX = "474554202f73746174757365732f7265706c6965732e786d6c20485454502f312e310d0a557365722d4167656e743a2043464e6574776f726b2f3333300d0a436f6f6b69653a205f747769747465725f736573733d4241683743446f4a64584e6c636a413642326c6b4969566d5a4751324f4463354d544d774d5746684f5446694d5745785a4456695a6d51774d47457a25323530414f574e6b4d79494b5a6d78686332684a517a6f6e51574e30615739755132397564484a766247786c636a6f36526d7868633267364f6b5a7359584e6f25323530415347467a61487341426a6f4b5148567a5a5752374141253235334425323533442d2d656131326537626330393064303532303263643765336639373263326234343134613937663635370d0a4163636570743a202a2f2a0d0a4163636570742d4c616e67756167653a20656e2d75730d0a4163636570742d456e636f64696e673a20677a69702c206465666c6174650d0a417574686f72697a6174696f6e3a2042617369632064584e6c636e526c633351366347467a63336476636d513d0d0a436f6e6e656374696f6e3a206b6565702d616c6976650d0a486f73743a20747769747465722e636f6d0d0a0d0a"
payload_ASCII = binascii.unhexlify(payload_HEX)
print(payload_ASCII)
~~~

This gives us the ASCII payload data:

~~~
GET /statuses/replies.xml HTTP/1.1\r\nUser-Agent: CFNetwork/330\r\nCookie: _twitter_sess=BAh7CDoJdXNlcjA6B2lkIiVmZGQ2ODc5MTMwMWFhOTFiMWExZDViZmQwMGEz%250AOWNkMyIKZmxhc2hJQzonQWN0aW9uQ29udHJvbGxlcjo6Rmxhc2g6OkZsYXNo%250ASGFzaHsABjoKQHVzZWR7AA%253D%253D--ea12e7bc090d05202cd7e3f972c2b4414a97f657\r\nAccept: */*\r\nAccept-Language: en-us\r\nAccept-Encoding: gzip, deflate\r\nAuthorization: Basic dXNlcnRlc3Q6cGFzc3dvcmQ=\r\nConnection: keep-alive\r\nHost: twitter.com\r\n\r\n
~~~

We can see an authorization field with base64 encoded text.  This can be decoded in python:

~~~py
import base64 as b64

word_b64 = "dXNlcnRlc3Q6cGFzc3dvcmQ="
word_ASCII = b64.b64decode(word_b64).decode()
print(word_ASCII)
~~~

This gives us the ASCII string:

~~~
usertest:password
~~~

The answer for this challenge is password.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
password
~~~

</details>

---

### [Networks](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Bluetooth Unknown File

- Author: Neptune
- Date: 01 March 2019
- Points: 15
- Level: 2

### Statement

Your friend working at NSA recovered an unreadable file from a hacker’s computer. The only thing he knows is that it comes from a communication between a computer and a phone.

The answer is the sha-1 hash of the concatenation of the MAC address (uppercase) and the name of the phone.

Example:

~~~
AB:CD:EF:12:34:56myPhone -> 023cc433c380c2618ed961000a681f1d4c44f8f1
~~~

### Related Resources

1. [Bluetooth](https://en.wikipedia.org/wiki/Bluetooth).
2. [fte.com - BT Snoop File Format](https://repository.root-me.org/R%C3%A9seau/EN%20-%20fte.com%20-%20BT%20Snoop%20File%20Format.pdf).

### Attachments

1. [ch18.bin](http://challenge01.root-me.org/reseau/ch18/ch18.bin) 1.4 kB.

### Solutions

<details>

<summary markdown="span">Solution</summary>

Reviewing the fte.com pdf, we can deconstruct the file in python, however lets first see if tshark recognises the file:

~~~shell
$ tshark -r ch18.bin
    1   0.000000   controller → host         HCI_EVT 13 Rcvd Connect Request   
    2   0.000995   controller → host         HCI_EVT 7 Rcvd Command Status (Accept Connection Request)   
    3   0.151001   controller → host         HCI_EVT 14 Rcvd Connect Complete   
    4   0.151927   controller → host         HCI_EVT 7 Rcvd Command Status (Read Remote Supported Features)   
    5   0.158944   controller → host         HCI_EVT 14 Rcvd Read Remote Supported Features   
    6   0.160013   controller → host         HCI_EVT 7 Rcvd Command Status (Read Remote Extended Features)   
    7   0.165028   controller → host         HCI_EVT 16 Rcvd Read Remote Extended Features Complete   
    8   0.166012   controller → host         HCI_EVT 7 Rcvd Command Status (Remote Name Request)   
    9   0.184990   controller → host         HCI_EVT 258 Rcvd Remote Name Request Complete   
   10   0.187930   controller → host         HCI_EVT 13 Rcvd Command Complete (IO Capability Request Reply)   
   11   3.518018   controller → host         HCI_EVT 13 Rcvd Command Complete (User Confirmation Request Reply)   
   12   4.557935   controller → host         HCI_EVT 7 Rcvd Encryption Change   
   13   9.704002   controller → host         HCI_EVT 7 Rcvd Disconnect Complete   
   14  16.677023   controller → host         HCI_EVT 13 Rcvd Connect Request   
   15  16.678020   controller → host         HCI_EVT 7 Rcvd Command Status (Accept Connection Request)   
   16  16.827024   controller → host         HCI_EVT 14 Rcvd Connect Complete   
   17  16.827935   controller → host         HCI_EVT 7 Rcvd Command Status (Read Remote Supported Features)   
   18  16.838025   controller → host         HCI_EVT 14 Rcvd Read Remote Supported Features   
   19  16.839019   controller → host         HCI_EVT 7 Rcvd Command Status (Read Remote Extended Features)   
   20  16.847014   controller → host         HCI_EVT 16 Rcvd Read Remote Extended Features Complete   
   21  16.848003   controller → host         HCI_EVT 7 Rcvd Command Status (Remote Name Request)   
   22  16.866918   controller → host         HCI_EVT 258 Rcvd Remote Name Request Complete   
   23  16.983007   controller → host         HCI_EVT 13 Rcvd Command Complete (Link Key Request Reply)   
   24  17.037004   controller → host         HCI_EVT 7 Rcvd Encryption Change   
   25  17.066004   controller → host         HCI_EVT 7 Rcvd Command Complete (Set AFH Host Channel Classification)   
   26  22.301026   controller → host         HCI_EVT 7 Rcvd Command Complete (Set AFH Host Channel Classification)   
   27  22.607029   controller → host         HCI_EVT 7 Rcvd Disconnect Complete 
~~~

Indeed, we get a 27-packet "HCI_EVT" capture. We need to find the MAC address and hostname of the tranmitter.  We can use the fields specified in the [bthci_evt filter reference](https://www.wireshark.org/docs/dfref/b/bthci_evt.html) using tshark with strings:

~~~shell
$ tshark -r ch18.bin -T fields -e bthci_evt.remote_name -e bthci_evt.bd_addr | strings | uniq 
	0c:b3:19:b9:4f:c6
GT-S7390G	0c:b3:19:b9:4f:c6
	0c:b3:19:b9:4f:c6
GT-S7390G	0c:b3:19:b9:4f:c6
	0c:b3:19:b9:4f:c6
~~~

We have:
 
- MAC address = 0c:b3:19:b9:4f:c6
- hostname = GT-S7390G

We can calculate the hash as required for this challenge in python:

~~~py
import hashlib
 
MAC = "0c:b3:19:b9:4f:c6"
Name = "GT-S7390G"
raw = (MAC+Name).upper().encode()

hash_obj = hashlib.sha1(raw)
 
hexa_value = hash_obj.hexdigest()
 
print(hexa_value)
~~~

This returns c1d0349c153ed96fe2fadf44e880aef9e69c122b which is the challenge solution.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
c1d0349c153ed96fe2fadf44e880aef9e69c122b
~~~

</details>

---

### [Networks](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## CISCO password

- Author: Thanat0s
- Date: 10 July 2013
- Points: 15
- Level: 2

### Statement

Find the "Enable" password.

### Related Resources

1. [Cisco passwords](https://repository.root-me.org/R%C3%A9seau/EN%20-%20Cisco%20passwords.pdf).
2. [Cisco passwords and encryption facts](https://repository.root-me.org/R%C3%A9seau/EN%20-%20Cisco%20passwords%20encryption%20facts.pdf).

### Attachments

1. [ch15.txt](http://challenge01.root-me.org/reseau/ch15/ch15.txt) 1.3 kB.

### Solutions

<details>

<summary markdown="span">Solution</summary>

This cisco config file details several users and passwords.  The challenge asks for the "enable" password.  Enable is a command used to configure a cisco device.  We have the following password hashes:

1. username hub password 7 025017705B3907344E 
2. username admin privilege 15 password 7 10181A325528130F010D24
3. username guest password 7 124F163C42340B112F3830
4. interface: line con0 password 7 144101205C3B29242A3B3C3927
5. enable secret 5 $1$p8Y6$MCdRLBzuGlfOs9S.hXOp0.
 
We can decypt the password 7s using [ciscot7](https://github.com/theevilbit/ciscot7):

~~~shell
$ python3 ciscot7.py -d -p 025017705B3907344E
Decrypted password: 6sK0_hub
$ python3 ciscot7.py -d -p 124F163C42340B112F3830
Decrypted password: 6sK0_guest
$ python3 ciscot7.py -d -p 144101205C3B29242A3B3C3927
Decrypted password: 6sK0_console
~~~

We now have the PT password 7 solutions:

| user    | Password hash              | Password PT  |
|---------|----------------------------|--------------|
| hub     | 025017705B3907344E         | 6sK0_hub     |
| guest   | 124F163C42340B112F3830     | 6sK0_guest   |
| console | 144101205C3B29242A3B3C3927 | 6sK0_console |
| admin   | 10181A325528130F010D24     | 6sK0_admin   |
 
Following the above password formats, we can check if 6sK0_enable is the solution.  This is correct.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
6sK0_enable
~~~

</details>

---

### [Networks](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## DNS zone transfert

- Author: g0uZ
- Date: 20 May 2013
- Points: 15
- Level: 2

### Statement

A not really dutiful administrator has set up a DNS service for the "ch11.challenge01.root-me.org" domain...

### Connection Details

- Host: challenge01.root-me.org
- Protocol: DNS
- Port: 54011

### Related Resources

1. [RFC 1035](https://repository.root-me.org/RFC/EN%20-%20rfc1035.txt).
2. [RFC 5936](https://repository.root-me.org/RFC/EN%20-%20rfc5936.txt).
3. [RFC 1034](https://repository.root-me.org/RFC/EN%20-%20rfc1034.txt).

### Solutions

<details>

<summary markdown="span">Solution</summary>

This is a zone transfer attack.  We can use dig to download the DNS zone data:

~~~shell
$ dig axfr @challenge01.root-me.org -p 54011 ch11.challenge01.root-me.org

; <<>> DiG 9.16.1-Ubuntu <<>> axfr @challenge01.root-me.org -p 54011 ch11.challenge01.root-me.org
; (2 servers found)
;; global options: +cmd
ch11.challenge01.root-me.org. 604800 IN	SOA	ch11.challenge01.root-me.org. root.ch11.challenge01.root-me.org. 2 604800 86400 2419200 604800
ch11.challenge01.root-me.org. 604800 IN	TXT	"DNS transfer secret key : CBkFRwfNMMtRjHY"
ch11.challenge01.root-me.org. 604800 IN	NS	ch11.challenge01.root-me.org.
ch11.challenge01.root-me.org. 604800 IN	A	127.0.0.1
challenge01.ch11.challenge01.root-me.org. 604800 IN A 192.168.27.101
ch11.challenge01.root-me.org. 604800 IN	SOA	ch11.challenge01.root-me.org. root.ch11.challenge01.root-me.org. 2 604800 86400 2419200 604800
;; Query time: 27 msec
;; SERVER: 212.129.38.224#54011(212.129.38.224)
;; WHEN: Thu Jan 06 13:05:42 GMT 2022
;; XFR size: 6 records (messages 1, bytes 274)
~~~
	
We specify the dns server @challenge01.root-me.org, the port -p 54011 the domain ch11.challenge01.root-me.org and use the acfr response to retrieve the zone data.  We can see the secret key is provided from the DNS TXT:

~~~
ch11.challenge01.root-me.org. 604800 IN	TXT	"DNS transfer secret key : CBkFRwfNMMtRjHY"
~~~

This gives us the solution to the challenge.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
CBkFRwfNMMtRjHY
~~~

</details>

---

### [Networks](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## IP Time to Live

- Author: g0uZ
- Date: 01 September 2010
- Points: 15
- Level: 2

### Statement

Find the TTL used to reach the targeted host in this ICMP exchange.

### Resources

1. [RFC 793](https://repository.root-me.org/RFC/EN%20-%20rfc793.txt).
2. [RFC 1035](https://repository.root-me.org/RFC/EN%20-%20rfc1035.txt).

### Attachments

1. [ch7.pcap](http://challenge01.root-me.org/reseau/ch7/ch7.pcap).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This is a simple challenge to find the TTL for the ICMP target.  [traceroute](https://en.wikipedia.org/wiki/Traceroute) works by increasing the TTL by 1 for each transmission and recording the TTL exceeded response from the intermediary hosts.  From our packet capture we can see the traceroute command increasing the TTL flag by 1 for each response until the TTL exceeded response is not returned:

~~~shell
$ tshark -r ch7.pcap 
    1   0.000000 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=768/3, ttl=1   64 AmbitMic_aa:af:80 
    2   3.364382 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=1024/4, ttl=1   64 AmbitMic_aa:af:80 
    3   6.368126 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=1280/5, ttl=1   64 AmbitMic_aa:af:80 
    4   9.371704 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=1536/6, ttl=2   64 AmbitMic_aa:af:80 
    5   9.393904 12.244.25.161 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
    6   9.394103 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=1792/7, ttl=2   64 AmbitMic_aa:af:80 
    7   9.407045 12.244.25.161 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
    8   9.407187 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=2048/8, ttl=2   64 AmbitMic_aa:af:80 
    9   9.433282 12.244.25.161 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
   10  15.040775 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=2304/9, ttl=3   64 AmbitMic_aa:af:80 
   11  15.063530 12.244.67.17 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
   12  15.066158 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=2560/10, ttl=3   64 AmbitMic_aa:af:80 
   13  15.076118 12.244.67.17 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
   14  15.076262 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=2816/11, ttl=3   64 AmbitMic_aa:af:80 
   15  15.098114 12.244.67.17 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
   16  20.819234 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=3072/12, ttl=4   64 AmbitMic_aa:af:80 
   17  20.832207 12.244.72.210 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
   18  20.832403 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=3328/13, ttl=4   64 AmbitMic_aa:af:80 
   19  20.853357 12.244.72.210 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
   20  20.853611 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=3584/14, ttl=4   64 AmbitMic_aa:af:80 
   21  20.869107 12.244.72.210 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
   22  26.399007 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=3840/15, ttl=5   64 AmbitMic_aa:af:80 
   23  26.419143 12.122.2.250 → 24.6.126.218 ICMP 134 Time-to-live exceeded (Time to live exceeded in transit)   64 Cadant_22:89:c2 
   24  26.419435 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=4096/16, ttl=5   64 AmbitMic_aa:af:80 
   25  26.439858 12.122.2.250 → 24.6.126.218 ICMP 134 Time-to-live exceeded (Time to live exceeded in transit)   64 Cadant_22:89:c2 
   26  26.439996 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=4352/17, ttl=5   64 AmbitMic_aa:af:80 
   27  26.461652 12.122.2.250 → 24.6.126.218 ICMP 134 Time-to-live exceeded (Time to live exceeded in transit)   64 Cadant_22:89:c2 
   28  27.472452 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=4608/18, ttl=6   64 AmbitMic_aa:af:80 
   29  27.497676 12.123.28.129 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
   30  27.498027 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=4864/19, ttl=6   64 AmbitMic_aa:af:80 
   31  27.528548 12.123.28.129 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
   32  27.528748 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=5120/20, ttl=6   64 AmbitMic_aa:af:80 
   33  27.560144 12.123.28.129 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
   34  28.622120 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=5376/21, ttl=7   64 AmbitMic_aa:af:80 
   35  28.653204 129.250.9.109 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
   36  28.653466 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=5632/22, ttl=7   64 AmbitMic_aa:af:80 
   37  28.673285 129.250.9.109 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
   38  28.673425 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=5888/23, ttl=7   64 AmbitMic_aa:af:80 
   39  28.708714 129.250.9.109 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
   40  34.285156 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=6144/24, ttl=8   64 AmbitMic_aa:af:80 
   41  34.307675 129.250.2.112 → 24.6.126.218 ICMP 182 Time-to-live exceeded (Time to live exceeded in transit)   64 Cadant_22:89:c2 
   42  34.307988 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=6400/25, ttl=8   64 AmbitMic_aa:af:80 
   43  34.329477 129.250.2.112 → 24.6.126.218 ICMP 182 Time-to-live exceeded (Time to live exceeded in transit)   64 Cadant_22:89:c2 
   44  34.329820 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=6656/26, ttl=8   64 AmbitMic_aa:af:80 
   45  34.365728 129.250.2.112 → 24.6.126.218 ICMP 182 Time-to-live exceeded (Time to live exceeded in transit)   64 Cadant_22:89:c2 
   46  35.759869 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=6912/27, ttl=9   64 AmbitMic_aa:af:80 
   47  35.822520 129.250.4.197 → 24.6.126.218 ICMP 182 Time-to-live exceeded (Time to live exceeded in transit)   64 Cadant_22:89:c2 
   48  35.822858 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=7168/28, ttl=9   64 AmbitMic_aa:af:80 
   49  35.876630 129.250.4.197 → 24.6.126.218 ICMP 182 Time-to-live exceeded (Time to live exceeded in transit)   64 Cadant_22:89:c2 
   50  35.876783 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=7424/29, ttl=9   64 AmbitMic_aa:af:80 
   51  35.926870 129.250.4.197 → 24.6.126.218 ICMP 182 Time-to-live exceeded (Time to live exceeded in transit)   64 Cadant_22:89:c2 
   52  36.959693 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=7680/30, ttl=10   64 AmbitMic_aa:af:80 
   53  37.038390 129.250.5.35 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
   54  37.038719 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=7936/31, ttl=10   64 AmbitMic_aa:af:80 
   55  37.118674 129.250.5.35 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
   56  37.119738 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=8192/32, ttl=10   64 AmbitMic_aa:af:80 
   57  37.199696 129.250.5.35 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
   58  38.205514 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=8448/33, ttl=11   64 AmbitMic_aa:af:80 
   59  38.290346 129.250.27.187 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
   60  38.290703 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=8704/34, ttl=11   64 AmbitMic_aa:af:80 
   61  38.385020 129.250.27.187 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
   62  38.410403 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=8960/35, ttl=11   64 AmbitMic_aa:af:80 
   63  38.493348 129.250.27.187 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
   64  44.552267 24.6.126.218 → 216.148.227.68 ICMP 70 Destination unreachable (Port unreachable) 53 3637  AmbitMic_aa:af:80 
   65  44.790695 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=9216/36, ttl=12   64 AmbitMic_aa:af:80 
   66  44.870689 204.2.121.162 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
   67  44.874186 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=9472/37, ttl=12   64 AmbitMic_aa:af:80 
   68  44.969505 204.2.121.162 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
   69  44.973782 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=9728/38, ttl=12   64 AmbitMic_aa:af:80 
   70  45.077511 204.2.121.162 → 24.6.126.218 ICMP 70 Time-to-live exceeded (Time to live exceeded in transit)    Cadant_22:89:c2 
   71  49.252888 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=9984/39, ttl=13   64 AmbitMic_aa:af:80 
   72  49.345998 198.173.244.32 → 24.6.126.218 ICMP 106 Echo (ping) reply    id=0x0200, seq=9984/39, ttl=51 (request in 71)   64 Cadant_22:89:c2 
   73  49.346312 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=10240/40, ttl=13   64 AmbitMic_aa:af:80 
   74  49.424540 198.173.244.32 → 24.6.126.218 ICMP 106 Echo (ping) reply    id=0x0200, seq=10240/40, ttl=51 (request in 73)   64 Cadant_22:89:c2 
   75  49.425163 24.6.126.218 → 198.173.244.32 ICMP 106 Echo (ping) request  id=0x0200, seq=10496/41, ttl=13   64 AmbitMic_aa:af:80 
   76  49.503822 198.173.244.32 → 24.6.126.218 ICMP 106 Echo (ping) reply    id=0x0200, seq=10496/41, ttl=51 (request in 75)   64 Cadant_22:89:c2 
~~~

We can see the TTL exceeded response stops at 13.  There are 13 hosts between the traceroute transmitter and the target.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
13
~~~

</details>

---

### [Networks](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## LDAP null bind

- Author: g0uZ
- Date: 26 May 2013
- Points: 15
- Level: 2

### Statement

It seems that one of the anonymous created a new branch in the LDAP directory, somewhere in:

~~~
dc=challenge01,dc=root-me,dc=org
~~~

Get access to its data and get his email adress.

### Connection Details

- Host: challenge01.root-me.org
- Protocol: TCP
- Port: 54013

### Resources

1. [RFC 4512](https://repository.root-me.org/RFC/EN%20-%20rfc4512.txt).
2. [RFC 4513](https://repository.root-me.org/RFC/EN%20-%20rfc4513.txt).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

The [Lightweight Directory Access Protocol](https://en.wikipedia.org/wiki/Lightweight_Directory_Access_Protocol) is a protocol for maintaining directory  services across a network.  It is often used for distributing user data across a network.  We can use [ldap3](https://ldap3.readthedocs.io/en/latest/) to query the ldap server for this challenge:
	
~~~py
import ldap3

HOST = "challenge01.root-me.org"
PORT = 54013

svr = ldap3.Server(HOST, port=PORT, get_info = ldap3.ALL)
con = ldap3.Connection(svr)
con.bind()
print("-"*30+"\n")
print("LDAP Server Information:\n")
print("-"*30+"\n")
print(svr.info)
print("-"*30+"\n")
~~~

This provides the LDAP server details:

~~~
------------------------------

LDAP Server Information:

------------------------------

DSA info (from DSE):
  Supported LDAP versions: 3
  Naming contexts: 
    dc=challenge01,dc=root-me,dc=org
  Supported controls: 
    1.2.826.0.1.3344810.2.3 - Matched Values - Control - RFC3876
    1.2.840.113556.1.4.319 - LDAP Simple Paged Results - Control - RFC2696
    1.3.6.1.1.12 - Assertion - Control - RFC4528
    1.3.6.1.1.13.1 - LDAP Pre-read - Control - RFC4527
    1.3.6.1.1.13.2 - LDAP Post-read - Control - RFC4527
    1.3.6.1.1.22 - LDAP Don't Use Copy - Control - RFC6171
    1.3.6.1.4.1.4203.1.10.1 - Subentries - Control - RFC3672
    2.16.840.1.113730.3.4.18 - Proxy Authorization Control - Control - RFC6171
    2.16.840.1.113730.3.4.2 - ManageDsaIT - Control - RFC3296
  Supported extensions: 
    1.3.6.1.1.8 - Cancel Operation - Extension - RFC3909
    1.3.6.1.4.1.4203.1.11.1 - Modify Password - Extension - RFC3062
    1.3.6.1.4.1.4203.1.11.3 - Who am I - Extension - RFC4532
  Supported features: 
    1.3.6.1.1.14 - Modify-Increment - Feature - RFC4525
    1.3.6.1.4.1.4203.1.5.1 - All Op Attrs - Feature - RFC3673
    1.3.6.1.4.1.4203.1.5.2 - OC AD Lists - Feature - RFC4529
    1.3.6.1.4.1.4203.1.5.3 - True/False filters - Feature - RFC4526
    1.3.6.1.4.1.4203.1.5.4 - Language Tag Options - Feature - RFC3866
    1.3.6.1.4.1.4203.1.5.5 - language Range Options - Feature - RFC3866
  Supported SASL mechanisms: 
    DIGEST-MD5, NTLM, CRAM-MD5
  Schema entry: 
    cn=Subschema
Other:
  objectClass: 
    top
    OpenLDAProotDSE
  structuralObjectClass: 
OpenLDAProotDSE
  configContext: 
    cn=config
  entryDN: 


------------------------------
~~~

we can see 3 Domain Component names that match the challenge statement.  We can copy the LDAP schema using ldap3:

~~~py
f = open("ldap_schema.txt","w")
f.write(str(svr.schema))
f.close()
~~~

This provides a large schema for this challenge, within which we can find the attributes "*mail" for which we are looking for the anonymous user.  We can find 3 mail attributes, mail, otherMailbox and janetMailbox.  These are found in object classes inetOrgPerson and pilotPerson which are classes within the top/person/organizationalPerson and top/person superior object classes respectively.
	
From the challenge, we can see the user is "one of the anonymous".  We can try searching the ldap server within the organizationalUnit.  We set our search to base ou=anonymous,dc=challenge01,dc=root-me,dc=org; filter to objectClass=inetOrgPerson, scope to SUBTREE and our attribute to mail:

~~~py
base = "ou=anonymous,dc=challenge01,dc=root-me,dc=org"
filt = "(&(objectClass=inetOrgPerson))"
scope= "SUBTREE"
attr = "mail"
users = con.search(search_base = base,search_filter=filt,search_scope=scope,attributes=attr)
if users:
    print(con.entries)
~~~

This returns the email address of all inetOrgPerson objects in the anonymous organizationalUnit, we get:

~~~
[DN: uid=sabu,ou=anonymous,dc=challenge01,dc=root-me,dc=org - STATUS: Read - READ TIME: 2022-01-06T15:22:49.999820
    mail: sabu@anonops.org
]
~~~

Which provides the email address.
	
</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
sabu@anonops.org
~~~

</details>

---

### [Networks](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## POP APOP

- Author: lutzenfried
- Date: 11 November 2020
- Points: 15
- Level: 2

### Statement

Find the user password in this network frame.

### Related Resources

1. [RFC 1939](https://repository.root-me.org/RFC/EN%20-%20rfc1939.txt).

### Attachments

1. [ch23.zip](http://challenge01.root-me.org/reseau/ch23/ch23.zip) 175 kB.

### Solutions

<details>

<summary markdown="span">Solution</summary>

We are given a zip file with a packet capture file, ch23.pcapng. As described in the challenge and the reference, this relates to a [Post Office Protocol](https://en.wikipedia.org/wiki/Post_Office_Protocol) conversation.  We can extract the POP packets using tshark:

~~~shell
$ tshark -r ch23.pcapng -w ch23_pop.pcap pop
~~~

This reduces our packet capture from 212.1 KiB to 1.2 KiB.  We can review the packets in tshark:

~~~shell
$ tshark -r ch23_pop.pcap
    1   0.000000 167.114.129.140 → 192.168.0.112 POP 149 S: +OK Hello little hackers. <1755.1.5f403625.BcWGgpKzUPRC8vscWn0wuA==@vps-7e2f5a72> 110 43188  ac:d9:f1:17:5b:f7 
    2  36.331587 192.168.0.112 → 167.114.129.140 POP 112 C: APOP bsmith 4ddd4137b84ff2db7291b568289717f0 43188 110  e8:71:b1:d9:4d:55 
    3  36.386548 167.114.129.140 → 192.168.0.112 POP 84 S: +OK Logged in. 110 43188  ac:d9:f1:17:5b:f7 
    4  39.587835 192.168.0.112 → 167.114.129.140 POP 72 C: LIST 43188 110  e8:71:b1:d9:4d:55 
    5  39.619931 167.114.129.140 → 192.168.0.112 POP 100 S: +OK 2 messages: 110 43188  ac:d9:f1:17:5b:f7 
    6  45.435223 192.168.0.112 → 167.114.129.140 POP 74 C: RETR 1 43188 110  e8:71:b1:d9:4d:55 
    7  45.465047 167.114.129.140 → 192.168.0.112 POP 92 S: +OK 6 octets 110 43188  ac:d9:f1:17:5b:f7 
    8  46.862121 192.168.0.112 → 167.114.129.140 POP 72 C: quit 43188 110  e8:71:b1:d9:4d:55 
    9  46.895866 167.114.129.140 → 192.168.0.112 POP 84 S: +OK Logging out. 110 43188  ac:d9:f1:17:5b:f7 
~~~

We can see an APOP response with what appears to be a username bsmith and a hex string, 4ddd4137b84ff2db7291b568289717f0.  As detailed in the RFC, this is an MD5 hash of the user password.  We can try to unhash it using an [online hashing/unhashing website](https://md5hashing.net).  This is succesful and we get 100%popprincess

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
100%popprincess
~~~

</details>

---

### [Networks](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## RF AM Transmission

- Author: Podalirius
- Date: 28 January 2021
- Points: 15
- Level: 2

### Statement

You have joined a team of radio frequency analysts. For your first mission, they ask you to decode this transmission.

### Related Resources

1. [GNU Radio Guided Tutorial](https://repository.root-me.org/R%C3%A9seau/EN%20-%20GNU%20Radio%20Guided%20Tutorial%20-%20gnuradio-org%20-%202020.pdf).
2. [Using GNU Radio for Analog Communications](https://repository.root-me.org/R%C3%A9seau/EN%20-%20Using%20GNU%20Radio%20forAnalog%20Communications%20-%20Derek%20Kozel%20Hackspace%20Brussels%20-%202019.pdf).

### Attachments

1. [ch24.zip](http://challenge01.root-me.org/reseau/ch24/ch24.zip) 2.0 MB.

### Solutions

<details>

<summary markdown="span">Solution</summary>

We are given a zip file with a raw binary file, am_capture.raw.  Reviewing the challenge details, we can see this is an AM demodulation challenge.  We use the raw file as a signal source and demodulate using the AM demodulation block in GNU Radio.  We can set sample rate to 32kHz, decimation to 2, audio lims to 4kHz and 8kHz and output the signal to the audio output block.  When running, we can playback the answer from the audio.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
rf_4m_tr4nsm1ss10n
~~~

</details>

---

### [Networks](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## RF FM Transmission

- Author: Podalirius
- Date: 28 January 2021
- Points: 20
- Level: 2

### Statement

For your second mission in the radio frequency analyst team, you have to decode this FM transmission.

The file you are working with is a complex IQ file, recorded at 8Msps.

### Related Resources

1. [GNU Radio Guided Tutorial](https://repository.root-me.org/R%C3%A9seau/EN%20-%20GNU%20Radio%20Guided%20Tutorial%20-%20gnuradio-org%20-%202020.pdf).
2. [Using GNU Radio for Analog Communications](https://repository.root-me.org/R%C3%A9seau/EN%20-%20Using%20GNU%20Radio%20forAnalog%20Communications%20-%20Derek%20Kozel%20Hackspace%20Brussels%20-%202019.pdf).

### Attachments

1. [ch25.zip](http://challenge01.root-me.org/reseau/ch25/ch25.zip) 286 MB.

### Solutions

<details>

<summary markdown="span">Solution</summary>

We are given a zip file with a raw binary file, capture.raw.  Reviewing the challenge details, we can see this is an FM demodulation challenge.  This file can be imported into gqrx to enable playback.  The following settings are used:
	
- Demodulation: Wideband FM (Mono)
- Frequency: 98.5 MHz
- Squelch: -50dB
- Filter Width: Normal
- Filter Shape: Normal
- Input Rate: 8,000,000
- Decimation: None
- Sample Rate: 8 Msps
- Audio rate: 48 kHz

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
rf_fr3qu3ncy_m0dul4t10n
~~~

</details>

---

### [Networks](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## SIP authentication

- Author: g0uZ
- Date: 30 August 2010
- Points: 20
- Level: 2

### Statement

Find the password used to authenticate on the SIP infrastructure.

### Related Resources

1. [Blackhat USA 06 Hacking VOIP exposed](https://repository.root-me.org/R%C3%A9seau/EN%20-%20Blackhat%20USA%2006%20Hacking%20VOIP%20exposed.pdf).

### Attachments

1. [ch4.txt](http://challenge01.root-me.org/reseau/ch4/ch4.txt).

### Solutions

<details>

<summary markdown="span">Solution</summary>

The challenge file can be retrived using wget:

~~~shell
$ wget http://challenge01.root-me.org/reseau/ch4/ch4.txt
--2022-01-16 12:08:23--  http://challenge01.root-me.org/reseau/ch4/ch4.txt
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 325 [text/plain]
Saving to: ‘ch4.txt’

ch4.txt                                                     100%[=========================================================================================================================================>]     325  --.-KB/s    in 0s      

2022-01-16 12:08:23 (111 MB/s) - ‘ch4.txt’ saved [325/325]

$ file ch4.txt 
ch4.txt: ASCII text
~~~

Opening the file:

~~~
172.25.105.3"172.25.105.40"555"asterisk"REGISTER"sip:172.25.105.40"4787f7ce""""PLAIN"1234
172.25.105.3"172.25.105.40"555"asterisk"INVITE"sip:1000@172.25.105.40"70fbfdae""""MD5"aa533f6efa2b2abac675c1ee6cbde327
172.25.105.3"172.25.105.40"555"asterisk"BYE"sip:1000@172.25.105.40"70fbfdae""""MD5"0b306e9db1f819dd824acf3227b60e07
~~~

This is a SIP authentication file with REGISTER, INVITE and BYE SIP signals.  This can be cracked using John the ripper and SIPCrack:

~~~shell
$ mkfifo myfifofile
$ john --incremental --stdout=6 > myfifofile & sipcrack -p 10000000 -w myfifofile ch4.txt
~~~

This conducts a bruteforce incremental attack on the hashed passwords and uses SIPCrack to handle the file structure.  We get the following result:

~~~
172.25.105.3"172.25.105.40"555"asterisk"REGISTER"sip:172.25.105.40"4787f7ce""""PLAIN"1234
172.25.105.3"172.25.105.40"555"asterisk"INVITE"sip:1000@172.25.105.40"70fbfdae""""PLAIN"1234
172.25.105.3"172.25.105.40"555"asterisk"BYE"sip:1000@172.25.105.40"70fbfdae""""PLAIN"1234
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
1234
~~~

</details>

---

### [Networks](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## ETHERNET Patched transmission

- Author: Thanat0s
- Date: 31 May 2013
- Points: 25
- Level: 3

### Statement

These frames have been altered upon interception, find the lost information.

Password’s format is 10 bytes in hexadecimal notation (i.e. 20 characters)

### Attachments

1. [ch14.txt](http://challenge01.root-me.org/reseau/ch14/ch14.txt).

### Solutions

<details>

<summary markdown="span">Solution</summary>

The challenge file can be retrived using wget:

~~~shell
$ wget http://challenge01.root-me.org/reseau/ch14/ch14.txt
--2022-01-16 12:39:43--  http://challenge01.root-me.org/reseau/ch14/ch14.txt
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1925 (1.9K) [text/plain]
Saving to: ‘ch14.txt’

ch14.txt                                                    100%[=========================================================================================================================================>]   1.88K  --.-KB/s    in 0s      

2022-01-16 12:39:43 (6.09 MB/s) - ‘ch14.txt’ saved [1925/1925]

$ file ch14.txt 
ch14.txt: ASCII text
~~~

Opening the file:

~~~
>>> INGRESS >>>
        0x0000:  0050 569e 7bf9 0050 569e 7bfb 8100 0185  
        0x0010:  86dd 6000 0000 0040 3a40 2002 c000 0203  
        0x0020:  0000 0000 0000 0000 7331 2002 c000 0203  
        0x0030:  0000 0000 0000 0000 dead 8000 0af0 0792  
        0x0040:  0001 146d a451 0000 0000 d020 0300 0000  
        0x0050:  0000 2d4d 452e 4f52 4720 524f 4f54 2d4d  
        0x0060:  452e 4f52 4720 524f 4f54 2d4d 452e 4f52  
        0x0070:  4720 524f 4f54 2d4d 452e


>>> INGRESS >>>
        0x0000:  0050 569e 7bf7 0050 569e 7bf9 8100 0186  
        0x0010:  86dd 6000 0000 0040 3a40 2002 c000 0203  
        0x0020:  0000 0000 0000 0000 b00b 2002 c000 0203  
        0x0030:  0000 0000 0000 0000 fada 8000 0af0 0792  
        0x0040:  0001 146d a451 0000 0000 d020 0300 0000  
        0x0050:  0000 2d4d 452e 4f52 4720 524f 4f54 2d4d  
        0x0060:  452e 4f52 4720 524f 4f54 2d4d 452e 4f52  
        0x0070:  4720 524f 4f54 2d4d 452e


>>> INGRESS >>>
        0x0000:  0050 569e 7bfe 0050 569e 7bf7 8100 0186  
        0x0010:  86dd 6000 0000 0040 3a40 2002 c000 0203  
        0x0020:  0000 0000 0000 0000 7331 2002 c000 0203  
        0x0030:  0000 0000 0000 0000 b00b 8000 c760 0795  
        0x0040:  0001 906d a451 0000 0000 8fac 0b00 0000  
        0x0050:  0000 2d4d 452e 4f52 4720 524f 4f54 2d4d  
        0x0060:  452e 4f52 4720 524f 4f54 2d4d 452e 4f52  
        0x0070:  4720 524f 4f54 2d4d 452e                 
                
<<< EGRESS <<<
        0x0000:  0050 569e 7b?? 0050 569e 7b?? ???? 0186  
        0x0010:  86dd 6000 0000 0040 ??40 2002 c000 0203  
        0x0020:  0000 0000 0000 0000 ???? 2002 c000 0203  
        0x0030:  0000 0000 0000 0000 ???? ??00 09f0 0792 
        0x0040:  0001 146d a451 0000 0000 d020 0300 0000  
        0x0050:  0000 2d4d 452e 4f52 4720 524f 4f54 2d4d  
        0x0060:  452e 4f52 4720 524f 4f54 2d4d 452e 4f52  
        0x0070:  4720 524f 4f54 2d4d 452e 
~~~

These can be concatenated into hex strings:

~~~
0050569e7bf90050569e7bfb8100018586dd6000000000403a402002c0000203000000000000000073312002c00002030000000000000000dead80000af007920001146da45100000000d0200300000000002d4d452e4f524720524f4f542d4d452e4f524720524f4f542d4d452e4f524720524f4f542d4d452e
0050569e7bf70050569e7bf98100018686dd6000000000403a402002c00002030000000000000000b00b2002c00002030000000000000000fada80000af007920001146da45100000000d0200300000000002d4d452e4f524720524f4f542d4d452e4f524720524f4f542d4d452e4f524720524f4f542d4d452e
0050569e7bfe0050569e7bf78100018686dd6000000000403a402002c0000203000000000000000073312002c00002030000000000000000b00b8000c76007950001906da451000000008fac0b00000000002d4d452e4f524720524f4f542d4d452e4f524720524f4f542d4d452e4f524720524f4f542d4d452e
0050569e7b??0050569e7b??????018686dd600000000040??402002c00002030000000000000000????2002c00002030000000000000000??????0009f007920001146da45100000000d0200300000000002d4d452e4f524720524f4f542d4d452e4f524720524f4f542d4d452e4f524720524f4f542d4d452e
~~~

The first component of each of these captures is the Ethernet header:

~~~
00 50 56 9e 7b f9 00 50 56 9e 7b fb 81 00
~~~

This can be deconstructed to fields:

~~~
Destination = (00:50:56:9E:7B:F9)
Source = (00:50:56:9E:7B:FB)
Type = 0x8100 (802.1Q VLAN)
~~~

The next part of the packet is the VLAN fields:

~~~
01 85 86 DD
~~~

This can be deconstructed:

~~~
VLAN ID = (0x0185) = 389
Type = (0x86DD) = IPv6
~~~

The IPv6 header:

~~~
60 00 00 00 00 40 3A 40 20 02 C0 00 02 03 00 00 00 00 00 00 00 00 73 31 20 02 C0 00 02 03 00 00 00 00 00 00 00 00 DE AD

~~~

This can be deconstructed:

~~~
IP Version = (0x60) = v6
Traffic Class = (0x00) = DSCP CS0
FLow Label = (0x0000) = 0
Payload Length = (0x0040) = 64
Next Header = (0x3A) = ICMPv6
Hop Limit = (0x40) = 64
Src Address = (2002:C000:0203:0000:0000:0000:0000:7331) = (2002:C000:203::7331)
Dst Address = (2002:C000:0203:0000:0000:0000:0000:DEAD) = (2002:C000:203::DEAD)
~~~

The ICMPv6 header:

~~~
80 00 0A F0 07 92 00 01
~~~

This can be deconstructed:

~~~
Type: (0x80) = Ping request (128)
Code: (0x00) = 0
Checksum: (0x0AF0)
ID: (0x0792)
Sequence: (0x0001) = 1
~~~

Two further field blocks (8B each) can  be seen but these are not identified:

~~~
90 6d a4 51 00 00 00 00
8f ac 0b 00 00 00 00 00
~~~

All 4 packets can be deconstructed:

| Packet  | 1                   | 2                   | 3                   | 4                   | Fix    |
|---------|---------------------|---------------------|---------------------|---------------------|--------|
| MAC Dst | 00:50:56:9E:7B:F9   | 00:50:56:9E:7B:F7   | 00:50:56:9E:7B:FE   | 00:50:56:9E:7B:??   | tbc    |
| MAC Src | 00:50:56:9E:7B:FB   | 00:50:56:9E:7B:F9   | 00:50:56:9E:7B:F7   | 00:50:56:9E:7B:??   | tbc    |
| Type    | 802.1Q VLAN         | 802.1Q VLAN         | 802.1Q VLAN         | ?? ??               | 0x8100 |
|---------|---------------------|---------------------|---------------------|---------------------|--------|
| VLAN ID | 389                 | 390                 | 390                 | 390                 |        |
| Type    | IPv6                | IPv6                | IPv6                | IPv6                |        |
|---------|---------------------|---------------------|---------------------|---------------------|--------|
| IP Vers | IPv6                | IPv6                | IPv6                | IPv6                |        |
| Class   | DSCP C0             | DSCP C0             | DSCP C0             | DSCP C0             |        |
| Label   | 0                   | 0                   | 0                   | 0                   |        |
| Len     | 64                  | 64                  | 64                  | 64                  |        |
| Type    | ICMPv6              | ICMPv6              | ICMPv6              | 0x??                | 0x3A   |
| Hop Lmt | 64                  | 64                  | 64                  | 64                  |        |
| Src Add | 2002:C000:203::7331 | 2002:C000:203::B00B | 2002:C000:203::7331 | 2002:C000:203::???? | tbc    |
| Dst Add | 2002:C000:203::DEAD | 2002:C000:203::FADA | 2002:C000:203::B00B | 2002:C000:203::???? | tbc    |
|---------|---------------------|---------------------|---------------------|---------------------|--------|
| Type    | Ping Request        | Ping Request        | Ping Request        | 0x??                | 0x81   |
| Code    | 0                   | 0                   | 0                   | 0                   |        |
| Chksm   | 0x0AF0              | 0x0AF0              | 0xC760              | 0x09F0              |        |
| ID      | 0x0792              | 0x0792              | 0x0795              | 0x0792              |        |
| Seq     | 1                   | 1                   | 1                   | 1                   |        |
|---------|---------------------|---------------------|---------------------|---------------------|--------|
| Block 1 | 0x146da45100000000  | 0x146da45100000000  | 0x906da45100000000  | 0x146da45100000000  |        |
| Block 2 | 0xd020030000000000  | 0xd020030000000000  | 0x8fac0b0000000000  | 0xd020030000000000  |        |
|---------|---------------------|---------------------|---------------------|---------------------|--------|

We can see it is an egress packet so is a ping reply (0x81).  It must be a reply for one of the ping requests originating within the same VLAN so is not a response to packet 1.

Block 1 and Block 2 match frame 2 so the src and destination fields are likely the destination and source from frame 2:

| Packet  | 2                   | 4                   | Solution |
|---------|---------------------|---------------------|----------|
| MAC Dst | 00:50:56:9E:7B:F7   | 00:50:56:9E:7B:F9   | f9       |
| MAC Src | 00:50:56:9E:7B:F9   | 00:50:56:9E:7B:F7   | f7       |
| Type    | 802.1Q VLAN         | 802.1Q VLAN         | 8100     |
|---------|---------------------|---------------------|----------|
| VLAN ID | 390                 | 390                 |          |
| Type    | IPv6                | IPv6                |          |
|---------|---------------------|---------------------|----------|
| IP Vers | IPv6                | IPv6                |          |
| Class   | DSCP C0             | DSCP C0             |          |
| Label   | 0                   | 0                   |          |
| Len     | 64                  | 64                  |          |
| Type    | ICMPv6              | ICMPv6              | 3A       |
| Hop Lmt | 64                  | 64                  |          |
| Src Add | 2002:C000:203::B00B | 2002:C000:203::FADA | fada     |
| Dst Add | 2002:C000:203::FADA | 2002:C000:203::B00B | b00b     |
|---------|---------------------|---------------------|----------|
| Type    | Ping Request        | Ping Reply          | 0x81     |
| Code    | 0                   | 0                   |          |
| Chksm   | 0x0AF0              | 0x09F0              |          |
| ID      | 0x0792              | 0x0792              |          |
| Seq     | 1                   | 1                   |          |
|---------|---------------------|---------------------|----------|
| Block 1 | 0x146da45100000000  | 0x146da45100000000  |          |
| Block 2 | 0xd020030000000000  | 0xd020030000000000  |          |
|---------|---------------------|---------------------|----------|

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
f9f781003afadab00b81
~~~

</details>

---

### [Networks](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---


## Global System Traffic for Mobile communication

- Author: koma
- Date: 25 April 2012
- Points: 25
- Level: 3

### Statement

You have been asked to check the network traffic file enclosed. Report your findings to your caller, even if it seems the trace was truncated.

### Attachments

1. [ch9.pcap](http://challenge01.root-me.org/reseau/ch9/ch9.pcap).

### Resources

1. [RFC 5724](https://repository.root-me.org/RFC/EN%20-%20rfc5724.txt).

### Solutions

<details>

<summary markdown="span">Solution</summary>

The challenge file can be retrived using wget:

~~~shell
$ wget http://challenge01.root-me.org/reseau/ch9/ch9.pcap
--2022-01-16 14:18:42--  http://challenge01.root-me.org/reseau/ch9/ch9.pcap
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 5048 (4.9K) [application/octet-stream]
Saving to: ‘ch9.pcap’

ch9.pcap                                                    100%[=========================================================================================================================================>]   4.93K  --.-KB/s    in 0.001s  

2022-01-16 14:18:42 (6.09 MB/s) - ‘ch9.pcap’ saved [5048/5048]
~~~

We can view the capture summary in tshark:

~~~shell
$ tshark -r ch9.pcap 
    1   0.000000        Modem → Unknown      ISI 31    7   
    2   3.498586        Modem → Unknown      ISI 31    7   
    3   9.383344        Modem → Unknown      ISI 31    7   
    4  11.733345        Modem → Unknown      ISI 31    7   
    5  14.085749        Modem → Unknown      ISI 31    7   
    6  15.267878        Modem → Unknown      ISI 31    7   
    7  17.621701        Modem → Unknown      ISI 31    7   
    8  19.971151        Modem → Unknown      ISI 31    7   
    9  23.501105        Modem → Unknown      ISI 31    7   
   10  25.860294        Modem → Unknown      ISI 31    7   
   11  28.214163        Modem → Unknown      ISI 31    7   
   12  30.567952        Modem → Unknown      ISI 31    7   
   13  31.744911        Modem → Unknown      ISI 31    7   
   14  36.448190        Modem → Unknown      ISI 31    7   
   15  45.868098        Modem → Unknown      ISI 31    7   
   16  52.929706        Modem → Unknown      ISI 31    7   
   17  58.814398        Modem → Unknown      ISI 31    7   
   18  63.522069        Modem → Unknown      ISI 31    7   
   19  67.052868        Modem → Unknown      ISI 31    7   
   20  68.229840        Modem → Unknown      ISI 31    7   
   21  69.406789        Modem → Unknown      ISI 31    7   
   22  70.583045        Modem → Unknown      ISI 31    7   
   23  77.645309        Modem → Unknown      ISI 31    7   
   24  78.822146        Modem → Unknown      ISI 31    7   
   25  81.176113        Modem → Unknown      ISI 31    7   
   26  83.529929        Modem → Unknown      ISI 31    7   
   27  85.879464        Modem → Unknown      ISI 31    7   
   28  87.055466        Modem → Unknown      ISI 31    7   
   29  89.414577        Modem → Unknown      ISI 31    7   
   30  92.945404        Modem → Unknown      ISI 31    7   
   31  94.122374        Modem → Unknown      ISI 31    7   
   32  96.471695        Modem → Unknown      ISI 31    7   
   33 103.537790        Modem → Unknown      ISI 31    7   
   34 107.068588        Modem → Unknown      ISI 31    7   
   35 109.422386        Modem → Unknown      ISI 31    7   
   36 111.776276        Modem → Unknown      ISI 31    7   
   37 115.737035      Unknown → Modem        ISI 30    6   
   38 115.747382        Modem → Unknown      ISI 41    17   
   39 115.747836      Unknown → Modem        ISI 32    8   
   40 115.750607        Modem → Unknown      ISI 41    17   
   41 115.750958      Unknown → Modem        ISI 32    8   
   42 115.753651        Modem → Unknown      ISI 41    17   
   43 115.754149      Unknown → Modem        ISI 30    6   
   44 115.756600        Modem → Unknown      ISI 31    7   
   45 116.480202        Modem → Unknown      ISI 31    7   
   46 118.837866        Modem → Unknown      ISI 31    7   
   47 120.019345        Modem → Unknown      ISI 31    7   
   48 121.191836        Modem → Unknown      ISI 31    7   
   49 122.368719        Modem → Unknown      ISI 31    7   
   50 123.545275        Modem → Unknown      ISI 31    7   
   51 125.901035        Modem → Unknown      ISI 31    7   
   52 127.076217        Modem → Unknown      ISI 31    7   
   53 136.491751        Modem → Unknown      ISI 31    7   
   54 137.668723        Modem → Unknown      ISI 31    7   
   55 138.845654        Modem → Unknown      ISI 31    7   
   56 140.022570        Modem → Unknown      ISI 31    7   
   57 142.376499        Modem → Unknown      ISI 31    7   
   58 143.553437        Modem → Unknown      ISI 31    7   
   59 144.732358        Modem → Unknown      ISI 31    7   
   60 145.907247        Modem → Unknown      ISI 31    7   
   61 149.438121        Modem → Unknown      ISI 31    7   
   62 155.324860        Modem → Unknown      ISI 31    7   
   63 160.029812        Modem → Unknown      ISI 31    7   
   64 161.206752        Modem → Unknown      ISI 31    7   
   65 167.092809        Modem → Unknown      ISI 31    7   
   66 176.503638        Modem → Unknown      ISI 31    7   
   67 184.746050        Modem → Unknown      ISI 31    7   
   68 187.099848        Modem → Unknown      ISI 31    7   
   69 189.453592        Modem → Unknown      ISI 31    7   
   70 191.806959        Modem → Unknown      ISI 31    7   
   71 196.515342        Modem → Unknown      ISI 31    7   
   72 197.692203        Modem → Unknown      ISI 31    7   
   73 201.223327        Modem → Unknown      ISI 31    7   
   74 208.284658        Modem → Unknown      ISI 31    7   
   75 210.638598        Modem → Unknown      ISI 31    7   
   76 211.815127        Modem → Unknown      ISI 31    7   
   77 212.992090        Modem → Unknown      ISI 31    7   
   78 214.169255        Modem → Unknown      ISI 31    7   
   79 216.523162        Modem → Unknown      ISI 31    7   
   80 218.877042        Modem → Unknown      ISI 31    7   
   81 220.053338        Modem → Unknown      ISI 31    7   
   82 223.584721        Modem → Unknown      ISI 31    7   
   83 227.115560        Modem → Unknown      ISI 32    8   
   84 227.122030        Modem → Unknown      ISI 31    7   
   85 227.839941        Modem → Unknown      ISI 31    7   
   86 230.664583        Modem → Unknown      ISI 31    7   
   87 230.766381        Modem → Unknown      ISI 126    72   
   88 230.820201      Unknown → Modem        ISI 35    11   
   89 230.822655        Modem → Unknown      ISI 35    11   
   90 231.135551        Modem → Unknown      ISI 31    7   
   91 231.785911        Modem → Unknown      ISI 32    8   
   92 231.792340        Modem → Unknown      ISI 31    7   
   93 231.792517        Modem → Unknown      ISI 32    8   
   94 231.833350      Unknown → Modem        ISI 30    6   
   95 231.836878        Modem → Unknown      ISI 41    17   
   96 231.837612      Unknown → Modem        ISI 32    8   
   97 231.839362        Modem → Unknown      ISI 41    17   
   98 231.840025      Unknown → Modem        ISI 32    8   
   99 231.841295        Modem → Unknown      ISI 41    17   
  100 231.842338      Unknown → Modem        ISI 30    6   
  101 231.844230        Modem → Unknown      ISI 31    7   
  102 234.177142        Modem → Unknown      ISI 31    7   
  103 237.708011        Modem → Unknown      ISI 31    7   
  104 241.238448        Modem → Unknown      ISI 31    7  
~~~

This shows 104 "intelligent service interface" packets containing data between 6 and 72 Bytes long.  We can open the pcap in wireshark and copy the hexstream for the largest packet.  In python, this can be used to retrieve the message:

~~~py
from PDUUSSDConverter import converter as con

a = 0x000003340001a00020202020202000f5a00001006900006700ff9c0402030201ffff0b5a0791233010210068040b917120336603f800002140206165028047c7f79b0c52bfc52c101d5d0699d9e133283d0785e764f87b6da7956bb7f82d2c8b
a = hex(a)[2:]

b = len(a)%7*"0"+a
text = con.pdu_to_text(b)
print(text)
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
asdpokv4e57q7a2
~~~

</details>

---

### [Networks](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---
	
## RF Key Fixed Code

- Author: Podalirius
- Date: 28 January 2021
- Points: 30
- Level: 3

### Statement

Bob is tired of thieves trying to lockpick his garage door. He replaced his traditional lock with an electronic lock.

In order to prove to Bob that his new garage door does not improve security, your team of radio analysts captured the radio transmissions around his house when he opened his garage door.

The flag is the sha256 hash of the code sent by the key in binary form. Example (printf "0110101101010" | sha256sum = 0d690e963de37180bb9b4ce77145d90e677444e9ebba9e738839fe60bda906f8 )

### Related Resources

1. [GNU Radio Tutorial](https://repository.root-me.org/R%C3%A9seau/EN%20-%20GNU%20Radio%20Guided%20Tutorial%20-%20gnuradio-org%20-%202020.pdf).
2. [Using GNU Radio for Analog Communications](https://repository.root-me.org/R%C3%A9seau/EN%20-%20Using%20GNU%20Radio%20forAnalog%20Communications%20-%20Derek%20Kozel%20Hackspace%20Brussels%20-%202019.pdf).

### Attachments

1. [ch26.zip](http://challenge01.root-me.org/reseau/ch26/ch26.zip).

### Solutions

<details>

<summary markdown="span">Solution</summary>

Downloading and unpacking the zip file, we are given a raw data file.  This can be opened into Audacity and visibly a key shift transmission can be seen.  Reviewing the capture, we find a repeating pattern:

~~~
ssllsslllslslllssslslssss
~~~

Where s is a short pulse and l is a long pulse.  This can be transcibed into 2 different binary patterns:
	
~~~
1100110001010001110101111
0011001110101110001010000
~~~

In Python, teh SHA256 hash for both binary strings can be generated and each hash can be submitted to find the correct version:

~~~py
import hashlib

binT = "0110101101010"
bin1 = "1100110001010001110101111"
bin2 = "0011001110101110001010000"

hashT = hashlib.sha256(binT.encode('utf-8')).hexdigest()
hash1 = hashlib.sha256(bin1.encode('utf-8')).hexdigest()
hash2 = hashlib.sha256(bin2.encode('utf-8')).hexdigest()

print("Test Binary: {}, hash = {}.".format(binT,hashT))
print("Key Binary v1: {}, hash: {}.".format(bin1,hash1))
print("Key Binary v2: {}, hash: {}.".format(bin2,hash2))
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
99cd1ae4e7d01e76a116cf823b4262f0b6ad1496bc398da91903526e1ad6b4fe
~~~

</details>

---

### [Networks](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## SSL HTTP exchange

- Author: g0uZ
- Date: 30 August 2010
- Points: 30
- Level: 3

### Statement

This challenge comes from the 19th DEFCON CTF’s qualification (pkt300).

CLUE : "google is your friend : inurl:server.pem..."

### Related Resources

1. [BlackHat USA 09 Zusman AttackExtSSL slides](https://repository.root-me.org/R%C3%A9seau/EN%20-%20BlackHat%20USA%2009%20Zusman%20AttackExtSSL%20slides.pdf).
2. [BlackHat USA 09 Marlin Spike DefeatSSL slides](https://repository.root-me.org/R%C3%A9seau/EN%20-%20BlackHat%20USA%2009%20Marlin%20Spike%20DefeatSSL%20slides.pdf).
3. [BlackHat USA 09 Zusman AttackExtSSL paper](https://repository.root-me.org/R%C3%A9seau/EN%20-%20BlackHat%20USA%2009%20Zusman%20AttackExtSSL%20paper.pdf).
4. [DROWN: Breaking TLS using SSLv2](https://repository.root-me.org/Cryptographie/Asym%C3%A9trique/EN%20-%20DROWN:%20Breaking%20TLS%20using%20SSLv2.pdf).
5. [RFC2246](https://repository.root-me.org/RFC/EN%20-%20rfc2246.txt).

### Attachments

1. [ch5.pcap](http://challenge01.root-me.org/reseau/ch5/ch5.pcap).

### Solutions

<details>

<summary markdown="span">Solution</summary>

The challenge file can be retrived using wget:

~~~shell
$ wget http://challenge01.root-me.org/reseau/ch5/ch5.pcap
--2022-04-23 11:59:11--  http://challenge01.root-me.org/reseau/ch5/ch5.pcap
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3242 (3.2K) [application/octet-stream]
Saving to: ‘ch5.pcap’

ch5.pcap                                                    100%[=========================================================================================================================================>]   3.17K  --.-KB/s    in 0s      

2022-04-23 11:59:11 (127 MB/s) - ‘ch5.pcap’ saved [3242/3242]

$ ls
ch5.pcap
~~~

As described in the challenge description, we can find the relevant rsa key from DEFCON 19 on google.  The RSA key can be copied from [github](https://github.com/Seabreg/dnmap/blob/master/server.pem) and saved in a local server.pem key file:

~~~
-----BEGIN CERTIFICATE-----
MIIDBjCCAm+gAwIBAgIBATANBgkqhkiG9w0BAQQFADB7MQswCQYDVQQGEwJTRzER
MA8GA1UEChMITTJDcnlwdG8xFDASBgNVBAsTC00yQ3J5cHRvIENBMSQwIgYDVQQD
ExtNMkNyeXB0byBDZXJ0aWZpY2F0ZSBNYXN0ZXIxHTAbBgkqhkiG9w0BCQEWDm5n
cHNAcG9zdDEuY29tMB4XDTAwMDkxMDA5NTEzMFoXDTAyMDkxMDA5NTEzMFowUzEL
MAkGA1UEBhMCU0cxETAPBgNVBAoTCE0yQ3J5cHRvMRIwEAYDVQQDEwlsb2NhbGhv
c3QxHTAbBgkqhkiG9w0BCQEWDm5ncHNAcG9zdDEuY29tMFwwDQYJKoZIhvcNAQEB
BQADSwAwSAJBAKy+e3dulvXzV7zoTZWc5TzgApr8DmeQHTYC8ydfzH7EECe4R1Xh
5kwIzOuuFfn178FBiS84gngaNcrFi0Z5fAkCAwEAAaOCAQQwggEAMAkGA1UdEwQC
MAAwLAYJYIZIAYb4QgENBB8WHU9wZW5TU0wgR2VuZXJhdGVkIENlcnRpZmljYXRl
MB0GA1UdDgQWBBTPhIKSvnsmYsBVNWjj0m3M2z0qVTCBpQYDVR0jBIGdMIGagBT7
hyNp65w6kxXlxb8pUU/+7Sg4AaF/pH0wezELMAkGA1UEBhMCU0cxETAPBgNVBAoT
CE0yQ3J5cHRvMRQwEgYDVQQLEwtNMkNyeXB0byBDQTEkMCIGA1UEAxMbTTJDcnlw
dG8gQ2VydGlmaWNhdGUgTWFzdGVyMR0wGwYJKoZIhvcNAQkBFg5uZ3BzQHBvc3Qx
LmNvbYIBADANBgkqhkiG9w0BAQQFAAOBgQA7/CqT6PoHycTdhEStWNZde7M/2Yc6
BoJuVwnW8YxGO8Sn6UJ4FeffZNcYZddSDKosw8LtPOeWoK3JINjAk5jiPQ2cww++
7QGG/g5NDjxFZNDJP1dGiLAxPW6JXwov4v0FmdzfLOZ01jDcgQQZqEpYlgpuI5JE
WUQ9Ho4EzbYCOQ==
-----END CERTIFICATE-----
-----BEGIN RSA PRIVATE KEY-----
MIIBPAIBAAJBAKy+e3dulvXzV7zoTZWc5TzgApr8DmeQHTYC8ydfzH7EECe4R1Xh
5kwIzOuuFfn178FBiS84gngaNcrFi0Z5fAkCAwEAAQJBAIqm/bz4NA1H++Vx5Ewx
OcKp3w19QSaZAwlGRtsUxrP7436QjnREM3Bm8ygU11BjkPVmtrKm6AayQfCHqJoT
ZIECIQDW0BoMoL0HOYM/mrTLhaykYAVqgIeJsPjvkEhTFXWBuQIhAM3deFAvWNu4
nklUQ37XsCT2c9tmNt1LAT+slG2JOTTRAiAuXDtC/m3NYVwyHfFm+zKHRzHkClk2
HjubeEgjpj32AQIhAJqMGTaZVOwevTXvvHwNEH+vRWsAYU/gbx+OQB+7VOcBAiEA
oolb6NMg/R3enNPvS1O4UU1H8wpaF77L4yiSWlE0p4w=
-----END RSA PRIVATE KEY-----
-----BEGIN CERTIFICATE REQUEST-----
MIIBDTCBuAIBADBTMQswCQYDVQQGEwJTRzERMA8GA1UEChMITTJDcnlwdG8xEjAQ
BgNVBAMTCWxvY2FsaG9zdDEdMBsGCSqGSIb3DQEJARYObmdwc0Bwb3N0MS5jb20w
XDANBgkqhkiG9w0BAQEFAANLADBIAkEArL57d26W9fNXvOhNlZzlPOACmvwOZ5Ad
NgLzJ1/MfsQQJ7hHVeHmTAjM664V+fXvwUGJLziCeBo1ysWLRnl8CQIDAQABoAAw
DQYJKoZIhvcNAQEEBQADQQA7uqbrNTjVWpF6By5ZNPvhZ4YdFgkeXFVWi5ao/TaP
Vq4BG021fJ9nlHRtr4rotpgHDX1rr+iWeHKsx4+5DRSy
-----END CERTIFICATE REQUEST-----
~~~

We can view and check this key is parsable using openssl:

~~~shell
$ openssl rsa -noout -text -in server.pem 
RSA Private-Key: (512 bit, 2 primes)
modulus:
    00:ac:be:7b:77:6e:96:f5:f3:57:bc:e8:4d:95:9c:
    e5:3c:e0:02:9a:fc:0e:67:90:1d:36:02:f3:27:5f:
    cc:7e:c4:10:27:b8:47:55:e1:e6:4c:08:cc:eb:ae:
    15:f9:f5:ef:c1:41:89:2f:38:82:78:1a:35:ca:c5:
    8b:46:79:7c:09
publicExponent: 65537 (0x10001)
privateExponent:
    00:8a:a6:fd:bc:f8:34:0d:47:fb:e5:71:e4:4c:31:
    39:c2:a9:df:0d:7d:41:26:99:03:09:46:46:db:14:
    c6:b3:fb:e3:7e:90:8e:74:44:33:70:66:f3:28:14:
    d7:50:63:90:f5:66:b6:b2:a6:e8:06:b2:41:f0:87:
    a8:9a:13:64:81
prime1:
    00:d6:d0:1a:0c:a0:bd:07:39:83:3f:9a:b4:cb:85:
    ac:a4:60:05:6a:80:87:89:b0:f8:ef:90:48:53:15:
    75:81:b9
prime2:
    00:cd:dd:78:50:2f:58:db:b8:9e:49:54:43:7e:d7:
    b0:24:f6:73:db:66:36:dd:4b:01:3f:ac:94:6d:89:
    39:34:d1
exponent1:
    2e:5c:3b:42:fe:6d:cd:61:5c:32:1d:f1:66:fb:32:
    87:47:31:e4:0a:59:36:1e:3b:9b:78:48:23:a6:3d:
    f6:01
exponent2:
    00:9a:8c:19:36:99:54:ec:1e:bd:35:ef:bc:7c:0d:
    10:7f:af:45:6b:00:61:4f:e0:6f:1f:8e:40:1f:bb:
    54:e7:01
coefficient:
    00:a2:89:5b:e8:d3:20:fd:1d:de:9c:d3:ef:4b:53:
    b8:51:4d:47:f3:0a:5a:17:be:cb:e3:28:92:5a:51:
    34:a7:8c
~~~

We can view the pcap file in tshark and see TLSv1 conversation that likely holds the encrypted data we need to solve this challenge:

~~~shell
$ tshark -r ch5.pcap
    1   0.000000  192.168.1.5 → 192.168.1.9  TCP 78 51663 → 4433 [SYN] Seq=0 Win=65535 Len=0 MSS=1460 WS=8 TSval=883067051 TSecr=0 SACK_PERM=1 51663 4433     
    2   0.097069  192.168.1.9 → 192.168.1.5  TCP 78 4433 → 51663 [SYN, ACK] Seq=0 Ack=1 Win=65535 Len=0 MSS=1460 WS=8 TSval=602956726 TSecr=883067051 SACK_PERM=1 4433 51663     
    3   0.097177  192.168.1.5 → 192.168.1.9  TCP 66 51663 → 4433 [ACK] Seq=1 Ack=1 Win=524280 Len=0 TSval=883067052 TSecr=602956726 51663 4433     
    4   0.097601  192.168.1.5 → 192.168.1.9  SSLv2 193 Client Hello 51663 4433     
    5   0.127956  192.168.1.9 → 192.168.1.5  TCP 66 [TCP Dup ACK 2#1] 4433 → 51663 [ACK] Seq=1 Ack=1 Win=524280 Len=0 TSval=602956727 TSecr=883067052 4433 51663     
    6   0.151078  192.168.1.9 → 192.168.1.5  TCP 66 4433 → 51663 [ACK] Seq=1 Ack=128 Win=524280 Len=0 TSval=602956727 TSecr=883067052 4433 51663     
    7   0.170059  192.168.1.9 → 192.168.1.5  TLSv1 947 Server Hello, Certificate, Server Hello Done 4433 51663     
    8   0.170169  192.168.1.5 → 192.168.1.9  TCP 66 51663 → 4433 [ACK] Seq=128 Ack=882 Win=524280 Len=0 TSval=883067052 TSecr=602956727 51663 4433     
    9   0.171257  192.168.1.5 → 192.168.1.9  TLSv1 200 Client Key Exchange, Change Cipher Spec, Finished 51663 4433     
   10   0.201991  192.168.1.9 → 192.168.1.5  TCP 66 4433 → 51663 [ACK] Seq=882 Ack=262 Win=524280 Len=0 TSval=602956728 TSecr=883067052 4433 51663     
   11   0.204638  192.168.1.9 → 192.168.1.5  TLSv1 125 Change Cipher Spec, Finished 4433 51663     
   12   0.204714  192.168.1.5 → 192.168.1.9  TCP 66 51663 → 4433 [ACK] Seq=262 Ack=941 Win=524280 Len=0 TSval=883067053 TSecr=602956728 51663 4433     
   13   0.218063  192.168.1.9 → 192.168.1.5  TLSv1 156 Application Data, Application Data 4433 51663     
   14   0.218179  192.168.1.5 → 192.168.1.9  TCP 66 51663 → 4433 [ACK] Seq=262 Ack=1031 Win=524280 Len=0 TSval=883067053 TSecr=602956728 51663 4433     
   15   3.794403  192.168.1.5 → 192.168.1.9  TLSv1 140 Application Data, Application Data 51663 4433     
   16   3.824184  192.168.1.9 → 192.168.1.5  TCP 66 4433 → 51663 [ACK] Seq=1031 Ack=336 Win=524280 Len=0 TSval=602956764 TSecr=883067089 4433 51663     
   17   3.827807  192.168.1.9 → 192.168.1.5  TCP 66 4433 → 51663 [FIN, ACK] Seq=1031 Ack=336 Win=524280 Len=0 TSval=602956764 TSecr=883067089 4433 51663     
   18   3.827905  192.168.1.5 → 192.168.1.9  TCP 66 51663 → 4433 [ACK] Seq=336 Ack=1032 Win=524280 Len=0 TSval=883067089 TSecr=602956764 51663 4433     
   19   3.828064  192.168.1.5 → 192.168.1.9  TLSv1 103 Alert (Level: Warning, Description: Close Notify) 51663 4433     
   20   3.828104  192.168.1.5 → 192.168.1.9  TCP 66 51663 → 4433 [FIN, ACK] Seq=373 Ack=1032 Win=524280 Len=0 TSval=883067089 TSecr=602956764 51663 4433     
   21   3.857509  192.168.1.9 → 192.168.1.5  TCP 66 [TCP Dup ACK 16#1] 4433 → 51663 [ACK] Seq=1032 Ack=336 Win=524280 Len=0 TSval=602956764 TSecr=883067089 4433 51663     
   22   3.859417  192.168.1.9 → 192.168.1.5  TCP 54 4433 → 51663 [RST] Seq=1032 Win=0 Len=0 4433 51663 
~~~

We can use ssldump to decrypt and view the TLS traffic:

~~~shell
$ ssldump -k server.pem -r ch5.pcap -dnq
New TCP connection #1: 192.168.1.5(51663) <-> 192.168.1.9(4433)
1 1  0.0976 (0.0976)  C>S SSLv2 compatible client hello
1 2  0.1700 (0.0724)  S>C  Handshake      ServerHello
Short read: 0 bytes available (expecting 2)
1 3  0.1700 (0.0000)  S>C  Handshake      Certificate
1 4  0.1700 (0.0000)  S>C  Handshake      ServerHelloDone
1 5  0.1712 (0.0011)  C>S  Handshake      ClientKeyExchange
1 6  0.1712 (0.0000)  C>S  ChangeCipherSpec
1 7  0.1712 (0.0000)  C>S  Handshake      Finished
1 8  0.2046 (0.0333)  S>C  ChangeCipherSpec
1 9  0.2046 (0.0000)  S>C  Handshake      Finished
1 10 0.2180 (0.0134)  S>C  application_data
    ---------------------------------------------------------------
    ---------------------------------------------------------------
1 11 0.2180 (0.0000)  S>C  application_data
    ---------------------------------------------------------------
    twisted by design
    ---------------------------------------------------------------
1 12 3.7944 (3.5763)  C>S  application_data
    ---------------------------------------------------------------
    ---------------------------------------------------------------
1 13 3.7944 (0.0000)  C>S  application_data
    ---------------------------------------------------------------
    
    ---------------------------------------------------------------
1    3.8278 (0.0334)  S>C  TCP FIN
1 14 3.8280 (0.0002)  C>S  Alert          warning          close_notify
1    3.8281 (0.0000)  C>S  TCP FIN
Cleaning 0 remaining connection(s) from connection pool
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
twisted by design
~~~

</details>

---

### [Networks](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---
	
Last updated April 2022.

## [djm89uk.github.io](https://djm89uk.github.io)
