
# Networks Fundamentals II Homework: In a Network Far, Far Away!

## Mission 1

- Command(s) used:
	`nslookup -type=MX starwars.com`
	
- Results:
	From the above command, the returned email servers were:
		```
		starwars.com	mail exchanger = 1 aspmx.l.google.com
		starwars.com	mail exchanger = 10 aspmx3.googlemail.com
		starwars.com	mail exchanger = 5 alt1.aspx.l.google.com
		starwars.com	mail exchanger = 10 aspmx2.googlemail.com
		starwars.com	mail exchanger = 5 alt2.aspmx.l.google.com
		```
	The Resistance is not receiving emails because the MX record does not include `asltx.l.google.com` or `asltx.2.google.com`.  
	The corrected DNS record should be something like:
		```
		starwars.com	mail exchanger = 1 asltx.l.google.com
		starwars.com	mail exchanger = 5 asltx.2.google.com
		```

## Mission 2

- Command(s) used:
	`nslookup -type=TXT theforce.net`
	
- Results:
	From the above command, the returned SPF record was:
		```
		theforce.net text = "v=spf1 a mx mx:smtp.secureserver.net include:aspmx.googlemail.com ip4:104.156.250.80 ip4:45.63.15.159 ip4:45.63.4.215"
		```
	This record is absent the specified IP address of `45.23.176.21`, which is why users are encountering difficulties.  
	The corrected DNS record should be something like:
		```
		theforce.net text = "v=spf1 a mx mx:smtp.secureserver.net include:aspmx.googlemail.com ip4:104.156.250.80 ip4:45.63.15.159 ip4:45.63.4.215 ip4:45.23.176.21"
		```
		
## Mission 3

- Command(s) used:
	```
	nslookup -type=CNAME www.theforce.net
	nslookup -type=CNAME resistance.theforce.net
	```

- Results:
	From the first command above, a CNAME should look like:
		`www.theforce.net		canonical name = theforce.net`
	From the second command above, the returned record is:
		`** server can't find resistance.theforce.net: NXDOMAIN`
	Clearly, the sub page of `resistance.theforce.net` isn't redirecting to `theforce.net` because the record is non-existent.  
	The corrected DNS record should be something like:
		```
		www.theforce.net         	canonical name = theforce.net
        resistance.theforce.net     canonical name = www.theforce.net
		```
	
## Mission 4

- Command(s) used:
	`nslookup -type=NS princessleia.site`

- Results:
	From the above command, the returned DNS record was:
		```
		princessleia.site nameserver = ns26.domaincontrol.com
        princessleia.site nameserver = ns25.domaincontrol.com
		```
	In order to prevent this issue from re-occurring, the record should be adjusted to something like:
		```
		princessleia.site nameserver = ns26.domaincontrol.com
        princessleia.site nameserver = ns25.domaincontrol.com
		princessleia.site nameswerver = ns2.galaxybackup.com
		```
	
## Mission 5

- Results:
	The shortest OSPF path from Batuu to Jedha is:
	Batuu
	Planet D	1
	Planet C	2
	Planet E	1
	Planet F	1
	Planet J	1
	Planet I	1
	Planet L	6
	Planet Q	4
	Planet T	2
	Planet V	2
	Jedha
	-------------
	Total: 21 hops
	This is the documented shortest path, and can be used by the Resistance as their static route.  As can be seen, it does not include Planet N.
	
## Mission 6

- Command(s) used:
	`sudo aircrack-ng Darkside.pcap -w rockyou.txt`

- Results:
	From the above command, the result was:
		```
		KEY FOUND! [ dictionary]
		```
	Therefore, decryption can be achieved with `dictionary:linksys`.  
	The most interesting Dark Side information so revealed is:
		```
		172.16.0.101    is at   00:13:ce:55:98:ef
		172.16.0.9      is at   00:14:bf:0f:03:30
		172.16.0.1      is at   00:0f:66:e3:e4:01
		68.9.16.30      is at   00:0f:66:e3:e4:01
		68.9.16.25      is at   00:0f:66:e3:e4:01
		10.1.1.50       is at   00:0f:66:e3:e4:01
		```
	Good luck with the counter-attack, and may the Force be with you.
	
## Mission 7

- Command(s) used:
	`nslookup -type=TXT princessleia.site`

- Results:
	From the above command, the result was:
		```
		Run the following in a Kali Linux command line:		telnet towel.blinkenlights.nl
		```
	When `telnet towel.blinkenlights.nl` is entered, the entirety of `Star Wars: A New Hope` begins to play in the command line.  One of my favorite Linux commands :)
	A screenshot of this can be found at:
	https://drive.google.com/file/d/1KT52IFrd1bPecEqHgqH-BTj8I-Vm8bNw/view?usp=sharing