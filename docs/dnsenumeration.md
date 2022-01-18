# [What’s DNS enumeration?][1]

It’s the act of detecting and enumerating all possible DNS records from a domain name. This includes hostnames, DNS record names, DNS record types, TTLs, IP addresses, and a bit more, depending on how much information you’re looking for.

## Impact

Once DNS enumeration is completed, unauthenticated users may use this information to observe internal network records, grabbing useful DNS information that provides the attacker access to a full DNS map. This allows him to explore the attack surface area of any company, so he can later scan it, collect data, and—while he’s at it—exploit it if there’s an open opportunity.

In the past we’ve seen a bit of DNS enumeration, such as in the [How to Find Subdomains](https://securitytrails.com/blog/subdomain-scanner-find-subdomains) article. However, that was only focused on subdomains. Today we’ll go one step forward and show you how to perform full DNS enumeration.

## Top 7 DNS enumeration tools

There are plenty of DNS recon and DNS enumeration tools around, from Bash to Python scripts; however, the easiest DNS enumeration can be performed with a single system command.

Let’s explore the best ways to perform a DNS enumeration.

### Dig

Once again, our beloved dig command comes to the rescue, helping us perform DNS enumeration by querying popular types of DNS records. Here’s how it’s done.

To perform a simple domain lookup to fetch A records:

```
dig dig zonetransfer.me +short
```

output:

```
5.196.105.14
```

Now let’s grab some mail server information adding -t mx parameters:

```
$ dig zonetransfer.me -t mx +short
10 ALT2.ASPMX.L.GOOGLE.COM.
20 ASPMX4.GOOGLEMAIL.COM.
0 ASPMX.L.GOOGLE.COM.
10 ALT1.ASPMX.L.GOOGLE.COM.
20 ASPMX2.GOOGLEMAIL.COM.
20 ASPMX3.GOOGLEMAIL.COM.
20 ASPMX5.GOOGLEMAIL.COM.
```

The same goes for NS, CNAME and other records:

```
dig zonetransfer.me -t ns +short
```

Output:

```
$ dig zonetransfer.me -t ns +short
nsztm2.digi.ninja.
nsztm1.digi.ninja.
```
Great! With this last command we now have the authoritative name servers.

Of course, dig allows DNS transfers and this leads us to use the AXFR argument against the nsztm2.digi.ninja. NS, as you see below:

```
dig axfr zonetransfer.me nsztm2.digi.ninja
; <<>> DiG 9.11.10-RedHat-9.11.10-1.fc30 <<>> axfr zonetransfer.me nsztm1.digi.ninja
;; global options: +cmd
; Transfer failed.
```

And the transfer failed, because our DNS servers are well secured.

Recon tip: sometimes a particular name server may be configured to reject AXFR requests. However, some others may not—that’s why we suggest you launch AXFR queries against all the authoritative NS.

### Host

Host is a command used to resolve the IP address of any given domain name.

As an example, we’ll use it to get all the public DNS records from zonetransfer.me. See below:

```
host zonetransfer.me
```

output:

```
$ host zonetransfer.me
zonetransfer.me has address 5.196.105.14
zonetransfer.me mail is handled by 10 ALT2.ASPMX.L.GOOGLE.COM.
zonetransfer.me mail is handled by 20 ASPMX4.GOOGLEMAIL.COM.
zonetransfer.me mail is handled by 0 ASPMX.L.GOOGLE.COM.
zonetransfer.me mail is handled by 10 ALT1.ASPMX.L.GOOGLE.COM.
zonetransfer.me mail is handled by 20 ASPMX2.GOOGLEMAIL.COM.
zonetransfer.me mail is handled by 20 ASPMX3.GOOGLEMAIL.COM.
zonetransfer.me mail is handled by 20 ASPMX5.GOOGLEMAIL.COM.
```

The default host command retrieves A, AAAA and MX records.

If you want to specify any specific type of DNS record, you can use the -t option. For example:

```
host -t ns zonetransfer.me
```
output:

```
$ host -t ns zonetransfer.me
zonetransfer.me name server nsztm2.digi.ninja.
zonetransfer.me name server nsztm1.digi.ninja.
```
What if you want to grab MX records? Just use -t mx, as shown here:

```
$ host -t mx zonetransfer.me
zonetransfer.me mail is handled by 10 ALT2.ASPMX.L.GOOGLE.COM.
zonetransfer.me mail is handled by 20 ASPMX4.GOOGLEMAIL.COM.
zonetransfer.me mail is handled by 0 ASPMX.L.GOOGLE.COM.
zonetransfer.me mail is handled by 10 ALT1.ASPMX.L.GOOGLE.COM.
zonetransfer.me mail is handled by 20 ASPMX2.GOOGLEMAIL.COM.
zonetransfer.me mail is handled by 20 ASPMX3.GOOGLEMAIL.COM.
zonetransfer.me mail is handled by 20 ASPMX5.GOOGLEMAIL.COM.
```

The -t option can be used to request any recognized query type such as: CNAME, NS, SOA, TXT, DNSKEY, AXFR, etc. If no query type is specified, host by default will look for A, AAAA and MX records.

Having said that, let’s try to perform a full DNS transfer:
```
$ host -t axfr zonetransfer.me nsztm2.digi.ninja
```

In the case of a successful DNS transfer, you should be able to get the full DNS zone for the given domain name.
```
Trying "zonetransfer.me"
Using domain server:
Name: nsztm2.digi.ninja
Address: 34.225.33.2#53
Aliases:

;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 43701
;; flags: qr aa; QUERY: 1, ANSWER: 51, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;zonetransfer.me.               IN      AXFR

;; ANSWER SECTION:
zonetransfer.me.        7200    IN      SOA     nsztm1.digi.ninja. robin.digi.ninja. 2019100801 172800 900 1209600 3600
zonetransfer.me.        300     IN      HINFO   "Casio fx-700G" "Windows XP"
zonetransfer.me.        301     IN      TXT     "google-site-verification=tyP28J7JAUHA9fw2sHXMgcCC0I6XBmmoVi04VlMewxA"
zonetransfer.me.        7200    IN      MX      0 ASPMX.L.GOOGLE.COM.
zonetransfer.me.        7200    IN      MX      10 ALT1.ASPMX.L.GOOGLE.COM.
zonetransfer.me.        7200    IN      MX      10 ALT2.ASPMX.L.GOOGLE.COM.
zonetransfer.me.        7200    IN      MX      20 ASPMX2.GOOGLEMAIL.COM.
zonetransfer.me.        7200    IN      MX      20 ASPMX3.GOOGLEMAIL.COM.
zonetransfer.me.        7200    IN      MX      20 ASPMX4.GOOGLEMAIL.COM.
zonetransfer.me.        7200    IN      MX      20 ASPMX5.GOOGLEMAIL.COM.
zonetransfer.me.        7200    IN      A       5.196.105.14
zonetransfer.me.        7200    IN      NS      nsztm1.digi.ninja.
zonetransfer.me.        7200    IN      NS      nsztm2.digi.ninja.
_acme-challenge.zonetransfer.me. 301 IN TXT     "2acOp15rSxBpyF6L7TqnAoW8aI0vqMU5kpXQW7q4egc"
_acme-challenge.zonetransfer.me. 301 IN TXT     "6Oa05hbUJ9xSsvYy7pApQvwCUSSGgxvrbdizjePEsZI"
_sip._tcp.zonetransfer.me. 14000 IN     SRV     0 0 5060 www.zonetransfer.me.
14.105.196.5.IN-ADDR.ARPA.zonetransfer.me. 7200 IN PTR www.zonetransfer.me.
asfdbauthdns.zonetransfer.me. 7900 IN   AFSDB   1 asfdbbox.zonetransfer.me.
asfdbbox.zonetransfer.me. 7200  IN      A       127.0.0.1
asfdbvolume.zonetransfer.me. 7800 IN    AFSDB   1 asfdbbox.zonetransfer.me.
canberra-office.zonetransfer.me. 7200 IN A      202.14.81.230
cmdexec.zonetransfer.me. 300    IN      TXT     "; ls"
contact.zonetransfer.me. 2592000 IN     TXT     "Remember to call or email Pippa on +44 123 4567890 or pippa@zonetransfer.me when making DNS changes"
dc-office.zonetransfer.me. 7200 IN      A       143.228.181.132
deadbeef.zonetransfer.me. 7201  IN      AAAA    dead:beaf::
dr.zonetransfer.me.     300     IN      LOC     53 20 56.558 N 1 38 33.526 W 0.00m 1m 10000m 10m
DZC.zonetransfer.me.    7200    IN      TXT     "AbCdEfG"
email.zonetransfer.me.  2222    IN      NAPTR   1 1 "P" "E2U+email" "" email.zonetransfer.me.zonetransfer.me.
email.zonetransfer.me.  7200    IN      A       74.125.206.26
Hello.zonetransfer.me.  7200    IN      TXT     "Hi to Josh and all his class"
home.zonetransfer.me.   7200    IN      A       127.0.0.1
Info.zonetransfer.me.   7200    IN      TXT     "ZoneTransfer.me service provided by Robin Wood - robin@digi.ninja. See http://digi.ninja/projects/zonetransferme.php for more information."
internal.zonetransfer.me. 300   IN      NS      intns1.zonetransfer.me.
internal.zonetransfer.me. 300   IN      NS      intns2.zonetransfer.me.
intns1.zonetransfer.me. 300     IN      A       81.4.108.41
intns2.zonetransfer.me. 300     IN      A       52.91.28.78
office.zonetransfer.me. 7200    IN      A       4.23.39.254
ipv6actnow.org.zonetransfer.me. 7200 IN AAAA    2001:67c:2e8:11::c100:1332
owa.zonetransfer.me.    7200    IN      A       207.46.197.32
robinwood.zonetransfer.me. 302  IN      TXT     "Robin Wood"
rp.zonetransfer.me.     321     IN      RP      robin.zonetransfer.me. robinwood.zonetransfer.me.
sip.zonetransfer.me.    3333    IN      NAPTR   2 3 "P" "E2U+sip" "!^.*$!sip:customer-service@zonetransfer.me!" .
sqli.zonetransfer.me.   300     IN      TXT     "' or 1=1 --"
sshock.zonetransfer.me. 7200    IN      TXT     "() { :]}; echo ShellShocked"
staging.zonetransfer.me. 7200   IN      CNAME   www.sydneyoperahouse.com.
alltcpportsopen.firewall.test.zonetransfer.me. 301 IN A 127.0.0.1
testing.zonetransfer.me. 301    IN      CNAME   www.zonetransfer.me.
vpn.zonetransfer.me.    4000    IN      A       174.36.59.154
www.zonetransfer.me.    7200    IN      A       5.196.105.14
xss.zonetransfer.me.    300     IN      TXT     "'><script>alert('Boo')</script>"
zonetransfer.me.        7200    IN      SOA     nsztm1.digi.ninja. robin.digi.ninja. 2019100801 172800 900 1209600 3600
```

This time we are using -l option, which is another way to list all DNS records from a domain name—while testing the vulnerable site zonetransfer.me:

```
$ host -l zonetransfer.me nsztm2.digi.ninja
Using domain server:
Name: nsztm2.digi.ninja
Address: 224.0.0.1#53
Aliases:

zonetransfer.me has address 5.196.105.14
zonetransfer.me name server nsztm1.digi.ninja.
zonetransfer.me name server nsztm2.digi.ninja.
14.105.196.5.IN-ADDR.ARPA.zonetransfer.me domain name pointer www.zonetransfer.me.
asfdbbox.zonetransfer.me has address 127.0.0.1
canberra-office.zonetransfer.me has address 202.14.81.230
dc-office.zonetransfer.me has address 143.228.181.132
deadbeef.zonetransfer.me has IPv6 address dead:beaf::
email.zonetransfer.me has address 74.125.206.26
home.zonetransfer.me has address 127.0.0.1
internal.zonetransfer.me name server intns1.zonetransfer.me.
internal.zonetransfer.me name server intns2.zonetransfer.me.
intns1.zonetransfer.me has address 81.4.108.41
intns2.zonetransfer.me has address 52.91.28.78
office.zonetransfer.me has address 4.23.39.254
ipv6actnow.org.zonetransfer.me has IPv6 address 2001:67c:2e8:11::c100:1332
owa.zonetransfer.me has address 207.46.197.32
alltcpportsopen.firewall.test.zonetransfer.me has address 127.0.0.1
vpn.zonetransfer.me has address 174.36.59.154
www.zonetransfer.me has address 5.196.105.14
```

### DNSenum

[DNSEnum](https://github.com/fwaeytens/dnsenum) is a great script specifically designed for DNS recon activities. Written in Perl, it can help you create a full DNS map of any domain name on the Internet.

Available in most distros, including Ubuntu, Fedora, and of course, Kali Linux, it offers an easy syntax for all who are performing reconnaissance tasks.

What can I do with DNSenum?

Fetch NS, MX, AXFR and A records, as well as remote BIND version from the DNS server. Apart from that, it also allows you to perform Google scraping using Google dorks such as allinurl: -www site:domain, launch brute force subdomain reconnaissance attacks using word lists, and get a full list of C class domain network ranges. It also allows WHOIS queries on each one of them and [reverse DNS lookups](https://securitytrails.com/blog/reverse-dns) against netranges.

How does it work?

Let’s look at an example where we’ll be avoiding reverse lookup (–noreverse) and saving the output into a file.xml (-o) while querying zonetransfer.me:

```
$ dnsenum --noreverse -o file.xml zonetransfer.me
dnsenum VERSION:1.2.6

-----   zonetransfer.me   -----


Host's addresses:
__________________

[0mzonetransfer.me.                         6908     IN    A        5.196.105.14


Name Servers:
______________

[0mnsztm2.digi.ninja.                       10066    IN    A        34.225.33.2
nsztm1.digi.ninja.                       10508    IN    A        81.4.108.41


Mail (MX) Servers:
___________________

[0maspmx4.googlemail.com.                   1        IN    A        172.253.113.26
aspmx5.googlemail.com.                   1        IN    A        173.194.77.26
aspmx.l.google.com.                      1        IN    A        142.250.141.26
alt1.aspmx.l.google.com.                 2        IN    A        64.233.171.27
alt2.aspmx.l.google.com.                 2        IN    A        142.250.152.27
aspmx2.googlemail.com.                   1        IN    A        64.233.171.26
aspmx3.googlemail.com.                   1        IN    A        142.250.152.26


Trying Zone Transfers and getting Bind Versions:
_________________________________________________

[0m
Trying Zone Transfer for zonetransfer.me on nsztm2.digi.ninja ... 
zonetransfer.me.                         7200     IN    SOA               (
zonetransfer.me.                         300      IN    HINFO        "Casio
zonetransfer.me.                         301      IN    TXT               (
zonetransfer.me.                         7200     IN    MX                0
zonetransfer.me.                         7200     IN    MX               10
zonetransfer.me.                         7200     IN    MX               10
zonetransfer.me.                         7200     IN    MX               20
zonetransfer.me.                         7200     IN    MX               20
zonetransfer.me.                         7200     IN    MX               20
zonetransfer.me.                         7200     IN    MX               20
zonetransfer.me.                         7200     IN    A        5.196.105.14
zonetransfer.me.                         7200     IN    NS       nsztm1.digi.ninja.
zonetransfer.me.                         7200     IN    NS       nsztm2.digi.ninja.
_acme-challenge.zonetransfer.me.         301      IN    TXT               (
_acme-challenge.zonetransfer.me.         301      IN    TXT               (
_sip._tcp.zonetransfer.me.               14000    IN    SRV               0
14.105.196.5.IN-ADDR.ARPA.zonetransfer.me. 7200     IN    PTR      www.zonetransfer.me.
asfdbauthdns.zonetransfer.me.            7900     IN    AFSDB             1
asfdbbox.zonetransfer.me.                7200     IN    A         127.0.0.1
asfdbvolume.zonetransfer.me.             7800     IN    AFSDB             1
canberra-office.zonetransfer.me.         7200     IN    A        202.14.81.230
cmdexec.zonetransfer.me.                 300      IN    TXT              ";
contact.zonetransfer.me.                 2592000  IN    TXT               (
dc-office.zonetransfer.me.               7200     IN    A        143.228.181.132
deadbeef.zonetransfer.me.                7201     IN    AAAA     dead:beaf::
dr.zonetransfer.me.                      300      IN    LOC              53
DZC.zonetransfer.me.                     7200     IN    TXT         AbCdEfG
email.zonetransfer.me.                   2222     IN    NAPTR             (
email.zonetransfer.me.                   7200     IN    A        74.125.206.26
Hello.zonetransfer.me.                   7200     IN    TXT             "Hi
home.zonetransfer.me.                    7200     IN    A         127.0.0.1
Info.zonetransfer.me.                    7200     IN    TXT               (
internal.zonetransfer.me.                300      IN    NS       intns1.zonetransfer.me.
internal.zonetransfer.me.                300      IN    NS       intns2.zonetransfer.me.
intns1.zonetransfer.me.                  300      IN    A        81.4.108.41
intns2.zonetransfer.me.                  300      IN    A        52.91.28.78
office.zonetransfer.me.                  7200     IN    A        4.23.39.254
ipv6actnow.org.zonetransfer.me.          7200     IN    AAAA     2001:67c:2e8:11::c100:1332
owa.zonetransfer.me.                     7200     IN    A        207.46.197.32
robinwood.zonetransfer.me.               302      IN    TXT          "Robin
rp.zonetransfer.me.                      321      IN    RP                (
sip.zonetransfer.me.                     3333     IN    NAPTR             (
sqli.zonetransfer.me.                    300      IN    TXT              "'
sshock.zonetransfer.me.                  7200     IN    TXT             "()
staging.zonetransfer.me.                 7200     IN    CNAME    www.sydneyoperahouse.com.
alltcpportsopen.firewall.test.zonetransfer.me. 301      IN    A         127.0.0.1
testing.zonetransfer.me.                 301      IN    CNAME    www.zonetransfer.me.
vpn.zonetransfer.me.                     4000     IN    A        174.36.59.154
www.zonetransfer.me.                     7200     IN    A        5.196.105.14
xss.zonetransfer.me.                     300      IN    TXT      "'><script>alert('Boo')</script>"

Trying Zone Transfer for zonetransfer.me on nsztm1.digi.ninja ... 
zonetransfer.me.                         7200     IN    SOA               (
zonetransfer.me.                         300      IN    HINFO        "Casio
zonetransfer.me.                         301      IN    TXT               (
zonetransfer.me.                         7200     IN    MX                0
zonetransfer.me.                         7200     IN    MX               10
zonetransfer.me.                         7200     IN    MX               10
zonetransfer.me.                         7200     IN    MX               20
zonetransfer.me.                         7200     IN    MX               20
zonetransfer.me.                         7200     IN    MX               20
zonetransfer.me.                         7200     IN    MX               20
zonetransfer.me.                         7200     IN    A        5.196.105.14
zonetransfer.me.                         7200     IN    NS       nsztm1.digi.ninja.
zonetransfer.me.                         7200     IN    NS       nsztm2.digi.ninja.
_acme-challenge.zonetransfer.me.         301      IN    TXT               (
_sip._tcp.zonetransfer.me.               14000    IN    SRV               0
14.105.196.5.IN-ADDR.ARPA.zonetransfer.me. 7200     IN    PTR      www.zonetransfer.me.
asfdbauthdns.zonetransfer.me.            7900     IN    AFSDB             1
asfdbbox.zonetransfer.me.                7200     IN    A         127.0.0.1
asfdbvolume.zonetransfer.me.             7800     IN    AFSDB             1
canberra-office.zonetransfer.me.         7200     IN    A        202.14.81.230
cmdexec.zonetransfer.me.                 300      IN    TXT              ";
contact.zonetransfer.me.                 2592000  IN    TXT               (
dc-office.zonetransfer.me.               7200     IN    A        143.228.181.132
deadbeef.zonetransfer.me.                7201     IN    AAAA     dead:beaf::
dr.zonetransfer.me.                      300      IN    LOC              53
DZC.zonetransfer.me.                     7200     IN    TXT         AbCdEfG
email.zonetransfer.me.                   2222     IN    NAPTR             (
email.zonetransfer.me.                   7200     IN    A        74.125.206.26
Hello.zonetransfer.me.                   7200     IN    TXT             "Hi
home.zonetransfer.me.                    7200     IN    A         127.0.0.1
Info.zonetransfer.me.                    7200     IN    TXT               (
internal.zonetransfer.me.                300      IN    NS       intns1.zonetransfer.me.
internal.zonetransfer.me.                300      IN    NS       intns2.zonetransfer.me.
intns1.zonetransfer.me.                  300      IN    A        81.4.108.41
intns2.zonetransfer.me.                  300      IN    A        167.88.42.94
office.zonetransfer.me.                  7200     IN    A        4.23.39.254
ipv6actnow.org.zonetransfer.me.          7200     IN    AAAA     2001:67c:2e8:11::c100:1332
owa.zonetransfer.me.                     7200     IN    A        207.46.197.32
robinwood.zonetransfer.me.               302      IN    TXT          "Robin
rp.zonetransfer.me.                      321      IN    RP                (
sip.zonetransfer.me.                     3333     IN    NAPTR             (
sqli.zonetransfer.me.                    300      IN    TXT              "'
sshock.zonetransfer.me.                  7200     IN    TXT             "()
staging.zonetransfer.me.                 7200     IN    CNAME    www.sydneyoperahouse.com.
alltcpportsopen.firewall.test.zonetransfer.me. 301      IN    A         127.0.0.1
testing.zonetransfer.me.                 301      IN    CNAME    www.zonetransfer.me.
vpn.zonetransfer.me.                     4000     IN    A        174.36.59.154
www.zonetransfer.me.                     7200     IN    A        5.196.105.14
xss.zonetransfer.me.                     300      IN    TXT      "'><script>alert('Boo')</script>"


Brute forcing with /usr/share/dnsenum/dns.txt:
_______________________________________________



zonetransfer.me class C netranges:
___________________________________

[0m 4.23.39.0/24
 5.196.105.0/24
 52.91.28.0/24
 74.125.206.0/24
 81.4.108.0/24
 143.228.181.0/24
 167.88.42.0/24
 174.36.59.0/24
 202.14.81.0/24
 207.46.197.0/24


zonetransfer.me ip blocks:
___________________________

[0m 4.23.39.254/32
 5.196.105.14/32
 52.91.28.78/32
 74.125.206.26/32
 81.4.108.41/32
 143.228.181.132/32
 167.88.42.94/32
 174.36.59.154/32
 202.14.81.230/32
 207.46.197.32/32

done.
```

As shown in the result, DNSenum was able to get A records for the main hostname, as well as NS and MX records, while performing a DNS zone transfer by querying the AXFR record.

DNSenum also allows you to use the Google search engine to “scrape” the results and get a list of subdomains. We’ll now combine this with the “-p” argument, which specifies the number of pages searched on Google that will be processed (by default 5 pages). The “-s” option defines the maximum number of subdomains that will be extracted from Google (default is 15).

```
$ dnsenum github.com -p 10 -s 50
dnsenum VERSION:1.2.6

-----   github.com   -----


Host's addresses:
__________________

github.com.                              41       IN    A        192.30.255.112


Wildcard detection using: pldpzwxolazj
_______________________________________

pldpzwxolazj.github.com.                 3600     IN    CNAME    github.github.io.
github.github.io.                        3600     IN    A        185.199.110.153
github.github.io.                        3600     IN    A        185.199.111.153
github.github.io.                        3600     IN    A        185.199.108.153
github.github.io.                        3600     IN    A        185.199.109.153


!!!!!!!!!!!!!!!!!!!!!!!!!!!!

 Wildcards detected, all subdomains will point to the same IP address
 Omitting results containing 185.199.110.153, 185.199.111.153, 185.199.108.153, 185.199.109.153.
 Maybe you are using OpenDNS servers.

!!!!!!!!!!!!!!!!!!!!!!!!!!!!


Name Servers:
______________

dns1.p08.nsone.net.                      82724    IN    A        198.51.44.8
ns-520.awsdns-01.net.                    22538    IN    A        205.251.194.8
dns4.p08.nsone.net.                      17183    IN    A        198.51.45.72
ns-1707.awsdns-21.co.uk.                 13703    IN    A        205.251.198.171
ns-421.awsdns-52.com.                    172800   IN    A        205.251.193.165
dns3.p08.nsone.net.                      86400    IN    A        198.51.44.72
ns-1283.awsdns-32.org.                   160879   IN    A        205.251.197.3
dns2.p08.nsone.net.                      6765     IN    A        198.51.45.8


Mail (MX) Servers:
___________________

alt3.aspmx.l.google.com.                 293      IN    A        172.253.113.27
alt4.aspmx.l.google.com.                 293      IN    A        173.194.77.27
aspmx.l.google.com.                      293      IN    A        142.250.141.26
alt1.aspmx.l.google.com.                 293      IN    A        64.233.171.26
alt2.aspmx.l.google.com.                 293      IN    A        142.250.152.26


Trying Zone Transfers and getting Bind Versions:
_________________________________________________


Trying Zone Transfer for github.com on dns1.p08.nsone.net ...
AXFR record query failed: NOTIMP

Trying Zone Transfer for github.com on ns-520.awsdns-01.net ...
AXFR record query failed: corrupt packet

Trying Zone Transfer for github.com on dns4.p08.nsone.net ...
AXFR record query failed: NOTIMP

Trying Zone Transfer for github.com on ns-1707.awsdns-21.co.uk ...
AXFR record query failed: corrupt packet

Trying Zone Transfer for github.com on ns-421.awsdns-52.com ...
AXFR record query failed: corrupt packet

Trying Zone Transfer for github.com on dns3.p08.nsone.net ...
AXFR record query failed: NOTIMP

Trying Zone Transfer for github.com on ns-1283.awsdns-32.org ...
AXFR record query failed: corrupt packet

Trying Zone Transfer for github.com on dns2.p08.nsone.net ...
AXFR record query failed: NOTIMP


Scraping github.com subdomains from Google:
____________________________________________

Error GETing http://www.google.com/sorry/index?continue=http://www.google.com/search%3Fhl%3Den%26source%3Dhp%26biw%3D%26bih%3D%26q%3D-www%2Bsite%253Agithub.com%26iflsig%3DALs-wAMAAAAAYecxdxh5UPiPfTqXkEfxvSALRoF9umyU%26gbv%3D1&hl=en&q=EgRZu7mrGOjGnI8GIhDgw-yK6Skttt0y2BHvxn_jMgFy: Too Many Requests at /usr/bin/dnsenum line 977.
```

Google Scrapping is failed. Maybe blocked by google. Above link in browser show robot check page. 

### Nmap

[Nmap](https://securitytrails.com/blog/top-15-nmap-commands-to-scan-remote-hosts) was our #1 choice when we reviewed the [best port scanners](https://securitytrails.com/blog/best-port-scanners), but it’s really more than that. This time it will help us reveal DNS information from a remote domain name.

By using the [dns-brute script](https://nmap.org/nsedoc/scripts/dns-brute.html), Nmap will attempt to enumerate DNS hostnames by brute forcing popular subdomain names. In this case, we did it against microsoft.com and this was the result:

```
$ nmap -T4 -p 53 --script dns-brute microsoft.com
Starting Nmap 7.92 ( https://nmap.org ) at 2022-01-19 05:41
Nmap scan report for microsoft.com (224.0.0.1)
Host is up (0.49s latency).
rDNS record for 224.0.0.1: all-systems.mcast.net

PORT   STATE  SERVICE
53/tcp closed domain

Host script results:
| dns-brute:
|   DNS Brute-force hostnames:
|     admin.microsoft.com - 13.107.6.156
|     admin.microsoft.com - 2620:1ec:a92::156
|     ads.microsoft.com - 23.100.75.192
|     id.microsoft.com - 13.107.42.22
|     id.microsoft.com - 2620:1ec:21::22
|     test.microsoft.com - 52.161.91.67
|     news.microsoft.com - 141.193.213.20
|     news.microsoft.com - 141.193.213.21
|     info.microsoft.com - 104.17.70.206
|     info.microsoft.com - 104.17.71.206
|     info.microsoft.com - 104.17.72.206
|     info.microsoft.com - 104.17.73.206
|     info.microsoft.com - 104.17.74.206
|     alerts.microsoft.com - 40.112.72.205
|     dns.microsoft.com - 104.215.148.63
|     dns.microsoft.com - 13.77.161.179
|     dns.microsoft.com - 40.112.72.205
|     dns.microsoft.com - 40.113.200.201
|     dns.microsoft.com - 40.76.4.15
|     apps.microsoft.com - 23.66.133.245
|     download.microsoft.com - 23.53.252.195
|     download.microsoft.com - 2600:1406:5800:28a::e59
|     download.microsoft.com - 2600:1406:5800:28f::e59
|     download.microsoft.com - 2600:1406:5800:2b8::e59
|     linux.microsoft.com - 13.77.154.182
|     ops.microsoft.com - 13.107.213.70
|     ops.microsoft.com - 13.107.246.70
|     ops.microsoft.com - 2620:1ec:46::70
|     ops.microsoft.com - 2620:1ec:bdf::70
|     local.microsoft.com - 198.61.151.94
|     owa.microsoft.com - 131.107.0.91
|     owa.microsoft.com - 131.107.1.89
|     owa.microsoft.com - 131.107.1.90
|     owa.microsoft.com - 131.107.1.91
|     beta.microsoft.com - 65.55.58.14
|     mail.microsoft.com - 157.58.197.10
|     mail.microsoft.com - 167.220.71.19
|     mail2.microsoft.com - 131.107.115.215
|     cdn.microsoft.com - 23.66.133.115
|     cdn.microsoft.com - 2600:1406:5400:187::20ac
|     cdn.microsoft.com - 2600:1406:5400:1a9::20ac
|     mail3.microsoft.com - 131.107.115.214
|     www.microsoft.com - 23.204.251.223
|     www.microsoft.com - 2600:1406:5400:4a1::356e
|     www.microsoft.com - 2600:1406:5400:4a8::356e
|     shop.microsoft.com - 104.215.148.63
|     shop.microsoft.com - 13.77.161.179
|     shop.microsoft.com - 40.112.72.205
|     shop.microsoft.com - 40.113.200.201
|     shop.microsoft.com - 40.76.4.15
|     ftp.microsoft.com - 134.170.188.232
|     manage.microsoft.com - 20.189.172.161
|     sip.microsoft.com - 52.112.70.139
|     sip.microsoft.com - 2603:1037::17:0:0:0:c
|     sip.microsoft.com - 2603:1037::1:0:0:0:b
|     sip.microsoft.com - 2603:1037::3:0:0:0:b
|     sip.microsoft.com - 2603:1037::4:0:0:0:b
|     sip.microsoft.com - 2603:1037::6:0:0:0:b
|     sip.microsoft.com - 2603:1037::8:0:0:0:b
|     sip.microsoft.com - 2603:1037::b:0:0:0:b
|     sip.microsoft.com - 2603:1037::f:0:0:0:f
|     smtp.microsoft.com - 131.107.115.212
|     smtp.microsoft.com - 131.107.115.214
|     smtp.microsoft.com - 131.107.115.215
|     smtp.microsoft.com - 205.248.106.30
|     smtp.microsoft.com - 205.248.106.32
|     smtp.microsoft.com - 205.248.106.64
|     mobile.microsoft.com - 65.55.186.235
|     help.microsoft.com - 40.112.72.205
|     demo.microsoft.com - 104.215.148.63
|     demo.microsoft.com - 13.77.161.179
|     demo.microsoft.com - 40.112.72.205
|     demo.microsoft.com - 40.113.200.201
|     demo.microsoft.com - 40.76.4.15
|     home.microsoft.com - 13.88.15.24
|_    dev.microsoft.com - 23.66.129.192

Nmap done: 1 IP address (1 host up) scanned in 29.42 seconds
```

While this isn’t the most complete DNS recon option, it does help as an alternative source of information during your data collection process.

### DNS Recon

[DNSRecon](https://github.com/darkoperator/dnsrecon) is another great [script](https://github.com/darkoperator/dnsrecon) that can help you discover DNS data from any given domain name.

It allows you to enumerate all types of DNS records, including A, AAAA, SPF, TXT, SOA, NS and MX, and also includes a brute force technique for grabbing subdomain and host A and AAAA records based on a wordlist.

A cool thing we noticed is that it supports checking for cached A and AAAA DNS records on the DNS servers, as well as local DNS enumeration capabilities.

How can I perform DNS exploration with DNSRecon?

The easiest way is by using the -d parameter, as you see below:

```
dnsrecon -d domain.com
```
Here we performed this dns enumeration against linkedin.com, and this was the result:

```
[*] std: Performing General Enumeration against: linkedin.com...
[-] DNSSEC is not configured for linkedin.com
[*]      SOA ns1.p43.dynect.net 208.78.70.43
[*]      SOA ns1.p43.dynect.net 2001:500:90:1::43
[*]      NS dns3.p09.nsone.net 198.51.44.73
[*]      NS dns3.p09.nsone.net 2620:4d:4000:6259:7:9:0:3
[*]      NS dns4.p09.nsone.net 198.51.45.73
[*]      NS dns4.p09.nsone.net 2a00:edc0:6259:7:9::4
[*]      NS ns1.p43.dynect.net 208.78.70.43
[*]      NS ns1.p43.dynect.net 2001:500:90:1::43
[*]      NS ns2.p43.dynect.net 204.13.250.43
[*]      NS ns3.p43.dynect.net 208.78.71.43
[*]      NS ns3.p43.dynect.net 2001:500:94:1::43
[*]      NS ns4.p43.dynect.net 204.13.251.43
[*]      NS dns1.p09.nsone.net 198.51.44.9
[*]      NS dns1.p09.nsone.net 2620:4d:4000:6259:7:9:0:1
[*]      NS dns2.p09.nsone.net 198.51.45.9
[*]      NS dns2.p09.nsone.net 2a00:edc0:6259:7:9::2
[*]      MX mail-d.linkedin.com 108.174.6.215
[*]      MX mail.linkedin.com 108.174.6.215
[*]      MX mail.linkedin.com 108.174.0.215
[*]      MX mail.linkedin.com 108.174.3.215
[*]      MX mail-a.linkedin.com 108.174.0.215
[*]      MX mail-c.linkedin.com 108.174.3.215
[*]      MX mail-d.linkedin.com 2620:109:c003:104::215
[*]      MX mail-a.linkedin.com 2620:119:50c0:207::215
[*]      MX mail-c.linkedin.com 2620:109:c006:104::215
[*]      A linkedin.com 13.107.42.14
[*]      AAAA linkedin.com 2620:1ec:21::14
[*]      TXT _dmarc.linkedin.com v=DMARC1; p=reject; rua=mailto:d@rua.agari.com,mailto:yfy3q-9359@rua.dmarc.emailanalyst.com; ruf=mailto:d@ruf.agari.com,mailto:yfy3q-9359@ruf.dmarc.emailanalyst.com
[*] Enumerating SRV Records
[+]      SRV _sip._udp.linkedin.com external.linkedin.com 216.52.18.142 5060
[+]      SRV _sips._tcp.linkedin.com external.linkedin.com 216.52.18.142 5061
[+]      SRV _sip._tcp.linkedin.com external.linkedin.com 216.52.18.142 5060
[+]      SRV _sip._tls.linkedin.com sipdir.online.lync.com 52.112.70.139 443
[+]      SRV _sip._tls.linkedin.com sipdir.online.lync.com 2603:1037:0:3::b 443
[+]      SRV _sip._tls.linkedin.com sipdir.online.lync.com 2603:1037:0:4::b 443
[+]      SRV _sip._tls.linkedin.com sipdir.online.lync.com 2603:1037:0:6::b 443
[+]      SRV _sip._tls.linkedin.com sipdir.online.lync.com 2603:1037:0:8::b 443
[+]      SRV _sip._tls.linkedin.com sipdir.online.lync.com 2603:1037:0:b::b 443
[+]      SRV _sip._tls.linkedin.com sipdir.online.lync.com 2603:1037:0:d::f 443
[+]      SRV _sip._tls.linkedin.com sipdir.online.lync.com 2603:1037:0:17::c 443
[+]      SRV _sip._tls.linkedin.com sipdir.online.lync.com 2603:1037:0:1::b 443
[+]      SRV _sipfederationtls._tcp.linkedin.com sipfed.online.lync.com 52.112.65.139 5061
[+]      SRV _sipfederationtls._tcp.linkedin.com sipfed.online.lync.com 2603:1037:0:6::b 5061
[+]      SRV _sipfederationtls._tcp.linkedin.com sipfed.online.lync.com 2603:1037:0:8::b 5061
[+]      SRV _sipfederationtls._tcp.linkedin.com sipfed.online.lync.com 2603:1037:0:b::b 5061
[+]      SRV _sipfederationtls._tcp.linkedin.com sipfed.online.lync.com 2603:1037:0:f::f 5061
[+]      SRV _sipfederationtls._tcp.linkedin.com sipfed.online.lync.com 2603:1037:0:17::c 5061
[+]      SRV _sipfederationtls._tcp.linkedin.com sipfed.online.lync.com 2603:1037:0:1::b 5061
[+]      SRV _sipfederationtls._tcp.linkedin.com sipfed.online.lync.com 2603:1037:0:3::b 5061
[+]      SRV _sipfederationtls._tcp.linkedin.com sipfed.online.lync.com 2603:1037:0:4::b 5061
[+]      SRV _xmpp-client._tcp.linkedin.com external.linkedin.com 216.52.18.142 5222
[+]      SRV _xmpp-server._tcp.linkedin.com external.linkedin.com 216.52.18.142 5269
[+]      SRV _carddavs._tcp.linkedin.com carddav.linkedin.com 108.174.10.14 443
[+]      SRV _carddavs._tcp.linkedin.com carddav.linkedin.com 2620:109:c002::6cae:a0e 443
[+] 25 Records Found
```

---
[1]: https://securitytrails.com/blog/dns-enumeration