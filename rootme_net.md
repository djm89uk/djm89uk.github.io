# [Root-Me](./rootme.md) Root-Me Networks [3/25]

Investigate captured traffic, network services and perform packet analysis.

## Contents

1. [FTP - authentication](#ftp-authentication) 🗸
2. [TELNET - authentication](#telnet-authentication) 🗸
3. [ETHERNET - frame](#ethernet-frame) 🗸
4. [Twitter authentication](#twitter-authentication)
5. [Bluetooth - Unknown file](#bluetooth-unknown-file)
6. [CISCO - password](#cisco-password)
7. [DNS - zone transfert](#dns-zone-transfert)
8. [IP - Time To Live](#ip-time-to-live)
9. [LDAP - null bind](#ldap-null-bind)
10. [POP - APOP](#pop-apop)
11. [RF - AM Transmission](#rf-am-transmission)
12. [RF - FM Transmission](#rf-fm-transmission)
13. [SIP - authentication](#sip-authentication)
14. [ETHERNET - Patched transmission](#ethernet-patched-transmission)
15. [Global System Traffic for Mobile communication](#global-system-traffic-for-mobile-communication)
16. [HTTP - DNS Rebinding](#http-dns-rebinding)
17. [RF - Key Fixed Code](#rf-key-fixed-code)
18. [SSL - HTTP exchange](#ssl-http-exchange)
19. [Netfilter - common mistakes](#netfilter-common-mistakes)
20. [SNMP - Authentification](#snmp-authentification)
21. [Wired Equivalent Privacy](#wired-equivalent-privacy)
22. [ICMP payload](#icmp-payload)
23. [RIPv1 - no authentication](#ripv1-no-authentication)
24. [XMPP - authentication](#xmpp-authentication)
25. [RF - Satellite transmission](#rf-satellite-transmission)

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

1. [RFC 959](https://repository.root-me.org/RFC/EN%20-%20rfc959.txt?_gl=1*5ifr48*_ga*MTI1ODExMDYzNC4xNjQxMzc5NDAz*_ga_SRYSKX09J7*MTY0MTQwNjA2MS40LjEuMTY0MTQwNzQ1MC4w).

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

1. [RFC 854](https://repository.root-me.org/RFC/EN%20-%20rfc854.txt?_gl=1*1760t9h*_ga*MTI1ODExMDYzNC4xNjQxMzc5NDAz*_ga_SRYSKX09J7*MTY0MTQwNjA2MS40LjEuMTY0MTQwODc5My4w).

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

1. [RFC 1024](https://repository.root-me.org/RFC/EN%20-%20rfc1042.txt?_gl=1*1bf0fpg*_ga*MTI1ODExMDYzNC4xNjQxMzc5NDAz*_ga_SRYSKX09J7*MTY0MTQwNjA2MS40LjEuMTY0MTQwOTQyMS4w).
2. [HTTP Basic Authentication and Digest Authentication](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20HTTP%20basic%20authentication%20and%20digest%20authentication.pdf?_gl=1*1bf0fpg*_ga*MTI1ODExMDYzNC4xNjQxMzc5NDAz*_ga_SRYSKX09J7*MTY0MTQwNjA2MS40LjEuMTY0MTQwOTQyMS4w)

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

Last updated Jan 2022.

## [djm89uk.github.io](https://djm89uk.github.io)
