# OSINT (Open source intelligence)

## What is OSINT? How can I make use of it?

https://securitytrails.com/blog/what-is-osint-how-can-i-make-use-of-it

The hacking techniques commonly referred to as ***"Google Dorks"*** are simple yet effective ways to use the most popular search engine on earth for OSINT purposes.

Therefore, the only thing we need is to begin querying Google with a few basic search operators. For example if we use "`site:anysite.com`", we'll find all the results related to a specific website. If we use "`filetype:`", it will show only the results from specific types of files.

You can also combine both searches. To search for .sql databases, for example, use this:

`filetype:sql site:anysite.com`

## how to search for sensitive information on Google

[Google Dorks](https://securitytrails.com/blog/google-hacking-techniques)

Some popular operators used to perform Google Dorking:

* ***Filetype***: you can use this dork to find any kind of filetypes.
* ***Ext***: can help you to find files with specific extensions (eg. .txt, .log, etc).
* ***Intext***: can perform queries helps to search for specific text inside any page.
* ***Intitle***: it will search for any specific words inside the page title.
* ***Inurl***: will look out for mentioned words inside the URL of any website.


What other OSINT apps and scripts can you use? Literally hundreds of utilities, including:

* Personal data collection tools like ~~~[That’s Them](https://thatsthem.com/)~~~, which can reveal a lot of information about individuals, all in one place
* The [Wayback Machine](https://archive.org/web/), a site that explores old versions of websites to reveal important information
* ~~~[GeoCreepy](https://www.geocreepy.com/)~~~, which tracks down geographic location information to provide a clear picture of users' current locations
* Automated OSINT apps for retrieving information, like [Spiderfoot](https://securitytrails.com/blog/spiderfoot-osint-automation-tool) or [the Phantom + SecurityTrails integration](https://securitytrails.com/blog/phantom-app-integration)
* [AMASS](https://securitytrails.com/blog/owasp-amass) is another great tool for information gathering and network mapping that you should keep in mind.
* ~~~[Popular OSINT browser extensions](https://securitytrails.com/blog/top-osint-web-browser-extensions) that include useful sources.~~~
* ~~~OSINT tools like [Shodan](https://www.shodan.io/), to search for internet-connected devices used by your target~~~

# TODO

* [Google Dorks](https://securitytrails.com/blog/google-hacking-techniques)
* [Wayback Machine](https://archive.org/web/)
* [HaveIbeenPwned](https://haveibeenpwned.com/) - personal email breach check
* [AMASS](https://securitytrails.com/blog/owasp-amass) Originally written by our friend Jeff Foley, OWASP Amass is probably one of the best reconnaissance and network mapping tools in the market. It's widely used for network discovery, DNS enumeration, and general attack surface mapping tasks with a varied set of techniques, with a heavy focus on intel gathering and data scrapping on HTTP, SSL/TLS, and DNS protocols.

And if that’s not enough, it also provides API integrations with popular cybersecurity data services, such as our own SecurityTrails API.

* [Recon-ng](https://github.com/lanmaster53/recon-ng) comes already built in the Kali Linux distribution and is another great tool used to perform quickly and thoroughly reconnaissance on remote targets. This web reconnaissance framework was written in Python and includes many modules, convenience functions and interactive help to guide you on how to use it properly.

The simple command-based interface allows you to run common operations like interacting with a database, run web requests, manage API keys or standardizing output content.

Fetching information about any target is pretty easy and can be done within seconds after installing. It includes interesting modules like google_site_web and bing_domain_web that can be used to find valuable information about the target domains.

While some recon-ng modules are pretty passive as they never hit the target network, others can launch interesting stuff right against the remote host.

* [theHarvester](https://securitytrails.com/blog/theharvester-tool) is another great alternative to fetch valuable information about any subdomain names, virtual hosts, open ports and email address of any company/website.

This is especially useful when you are in the first steps of a penetration test against your own local network, or against 3rd party authorized networks. Same as previous tools, theHarvester is included inside Kali Linux distro.

theHarvester uses many resources to fetch the data like PGP key servers, Bing, Baidu, Yahoo and Google search engine, and also social networks like Linkedin, Twitter and Google Plus.

It can also be used to launch active penetration test like DNS brute force based on dictionary attack, rDNS lookups and DNS TLD expansion using dictionary brute force enumeration.

* [Jigsaw](https://www.jigsawsecurityenterprise.com/) is used to gather information about any company employees. This tool works perfectly for companies like Google, Linkedin, or Microsoft, where we can just pick up one of their domain names (like google.com), and then gather all their employee's emails on the different company departments.

The only drawback is that these queries are launched against Jigsaw database located at jigsaw.com, so, we depend entirely on what information they allow us to explore inside their database. You will be able to find information about big companies, but if you are exploring a not so famous startup then you may be out of luck.

* [Nmap](https://nmap.org/) is one of the most popular and widely used security auditing tools, its name means "Network Mapper". Is a free and open source utility utilized for security auditing and network exploration across local and remote hosts.

Some of the main features include:

    Host detection: Nmap has the ability to identify hosts inside any network that have certain ports open, or that can send a response to ICMP and TCP packets.
    IP and DNS information detection: including device type, Mac addresses and even reverse DNS names.
    Port detection: Nmap can detect any port open on the target network, and let you know the possible running services on it.
    OS detection: get full OS version detection and hardware specifications of any host connected.
    Version detection: Nmap is also able to get application name and version number.

* [WebShag](https://github.com/wereallfeds/webshag) is a great server auditing tool used to scan HTTP and HTTPS protocols. Same as other tools, it's part of Kali Linux and can help you a lot in your IT security research & penetration testing.

You will be able to launch a simple scan, or use advanced methods like through a proxy, or over HTTP authentication.

Written in Python, it can be one of your best allies while auditing systems.

Main features include:

    Port Scan
    URL scanning
    File fuzzing
    Website crawling

In order to avoid getting blocked by remote server security systems, it uses an intelligent IDS evasion system by launching random requests per HTTP proxy server, so you can keep auditing the server without being banned.

* [OpenVAS](http://www.openvas.org/) (Open Vulnerability Assessment System) is a security framework that includes particular services and tools for infosec professionals.

This is an open source vulnerability scanner & security manager that was built after the famous Nessus switched from open source to private source. Then, the original developers of the Nessus vulnerability scanner decided to fork the original project and create OpenVAS.

While it is a little bit more difficult to setup than the old Nessus, it's quite effective while working with it to analyze the security of remote hosts.

The main tool included in OpenVAS is OpenVAS Scanner, a highly efficient agent that executes all the network vulnerability tests over the target machine.

On the other hand, another main component is called OpenVAS Manager, which is basically vulnerability management solution that allows you to store scanned data into an SQLite database, so then you can search, filter and order the scan results in a fancy and easy way.

* [Fierce](https://github.com/mschwager/fierce) is an IP and DNS recon tool written in PERL, famous for helping IT sec professionals to find target IPs associated with domain names.

It was written originally by RSnake along with other members of the old http://ha.ckers.org/. It's used mostly targetting local and remote corporate networks.

Once you have defined your target network, it will launch several scans against the selected domains and then it will try to find misconfigured networks and vulnerable points that can later leak private and valuable data.

The results will be ready within a few minutes, a little bit more than when you perform any other scan with similar tools like Nessus, Nikto, Unicornscan, etc.

* [Unicornscan](https://github.com/dneufeld/unicornscan) is one of the top intel gathering tools for security research. It has also a built-in correlation engine that aims to be efficient, flexible and scalable at the same time.

Main features include:

    Full TCP/IP device/network scan.
    Asynchronous stateless TCP scanning (including all TCP Flags variations).
    Asynchronous TCP banner detection.
    UDP Protocol scanning.
    A/P OS identification.
    Application and component detection.
    Support for SQL Relational Output

* [FOCA](https://www.elevenpaths.com/innovation-labs/technologies/foca) (Fingerprinting Organizations with Collected Archives) is a tool written by ElevenPaths that can be used to scan, analyze, extract and classify information from remote web servers and their hidden information.

Foca has the ability to analyze and collect valuable data from MS Office suite, OpenOffice, PDF, as well as Adobe InDesign and SVG and GIF files. This security tool also works actively with Google, Bing and DuckDuckGo search engines to collect additional data from those files. Once you have the full file list, it starts extracting information to attempt to identify more valuable data from the files.

* [IVRE](https://doc.ivre.rocks/en/latest/) This infosec tool is frequently overlooked, but it has great potential in boosting your infosec discovery and analysis processes. IVRE is an open source tool that's built on a base of popular projects like Nmap, Masscan, ZDNS, and ZGrab2.

Its framework uses these popular tools to gather network intelligence on any host, then uses a MongoDB database to store the data.

Its web-based interface makes it easy for both beginning and advanced infosec users to perform the following actions:

    Passive reconnaissance by flow analysis (from Zeek, Argus or nfdump)
    Active reconnaissance by using Zmap and Nmap
    Fingerprinting analysis
    Import data from other 3rd party infosec apps, such as Masscan/Nmap

IVRE can be installed by fetching the source from their official Github repo, or from 3rd-party repositories such as Kali Linux repo.

* [Metagoofil](https://tools.kali.org/information-gathering/metagoofil) is another great intel-reconnaissance tool that aims to help infosec researchers, IT managers, and red teams to extract metadata from different types of files, such as:

    doc
    docx
    pdf
    xls
    xlsx
    ppt
    pptx

How does it work? This app performs a deep search on search engines like Google, focusing on these types of files. Once it detects such a file, it will download it to your local storage, then proceed to extract all of its valuable data.

Once the extraction is complete, you'll see a full report with usernames, software banners, app versions, hostnames and more, a valuable resource for your recon phase.

Metagoofil also includes a number of options to help you filter the types of files to search for, refine the results and tweak the output, among many other useful features.

* [Exiftool](https://exiftool.org/)

While a lot of OSINT tools focus on data found on public files such as PDF, .DOC, HTML, .SQL, etc., there are other tools that are specifically designed to extract critical Open Source Intelligence data from image, video and audio files.

Exiftool reads, writes and extracts metadata from the following types of files:

    EXIF
    IPTC
    GPS
    XMP
    JFIF
    And many others

It also supports native files from a wide range of cameras, such as: Canon, Casio, FujiFilm, Kodak, Sony, and many others. It's also conveniently available on multiple platforms including Linux, Windows and MacOS.