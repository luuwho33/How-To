# Performing a basic host discovery scan (Internal Networks)

[RFC 1918](https://tools.ietf.org/html/rfc1918) defines the following ranges as reserved for internal use:
- 10.0.0.08
- 172.16.0.0/12
- 192.168.0.0/16

For the purposes of this guide, we are going to assume these are the only internal ranges being used. This may differ in the real-world.

## Masscan 

Masscan is a tool that can perform a large scal network scan very quickly. The command we will run is:

`masscan --top-ports 20 10.0.0.0/8 172.16.0.0/12 192.168.0.0/16 --rate=10000 -oX ~/Desktop/masscan_output_file.xml`

Any time you are running a tool/command/script you need to understand what you are doing. Let's break this command down into four parts:

`masscan --top-ports 20`

This first part of the command is calling the tool masscan, and is specifying which ports will be scanned. This means for every IP address we scan, we will look for this list of ports. This list uses the nmap database to scan to 20 most common ports. 

1. 21 - ftp
2. 22 - ssh
3. 23 - telnet
4. 25 - smtp
5. 53 - domain name system
6. 80 - http
7. 110 - pop3
8. 111 - rpcbind
9. 135 - msrpc
10. 139 - netbios-ssn
11. 143 - imap
12. 443 - https
13. 445 - microsoft-ds
14. 993 - imaps
15. 995 - pop3s
16. 1723 - pptp
17. 3306 - mysql
18. 3389 - ms-wbt-server
19. 5900 - vnc
20. 8080 - http-proxy

`10.0.0.0/8 172.16.0.0/12 192.168.0.0/16` 

Here we list the target IP address, list of IP addresses, or ranges of IP addresses. As noted above, we are assuming only the RFC 1918 addresses are being used.

`--rate=10000`

This setting is telling masscan how many packets to send per second. This value of 10,000 packets should provide an adequate balance to accomplish the scan in a reasonable amount of time, without consuming too much bandwidth.

`-oX ~/Desktop/masscan_output_file.xml`

This last part of the command is telling masscan to save the results of the scan to an XML file (-oX) and is specificing the path and file name (~/Desktop/masscan_output_file.xml). 

### Optional flags

There are many more flags supported by masscan, but here are a few that you may use more often than the others.

`-p21,22,23,25,53,80,110,111,132,139,143,443,445,993,995,1723,3306,3389,5900,8080`

This accomplishes the same thing as `--top-ports 20` but has been included here as some masscan installs do not work well with that flag.

`--excludefile no_scan.txt`

This flag provides a list of IP addresses that massscan will NOT scan. This is useful when scanning a range of IPs, but know there are a few IPs that do not respond well to port scans.