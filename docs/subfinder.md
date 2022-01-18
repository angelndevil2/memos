# Subfinder

```
subfinder --help

Usage of subfinder:
  -cd
        Upload results to the Chaos API (api-key required)
  -config string
        Configuration file for API Keys, etc (default "$HOME/.config/subfinder/config.yaml")
  -d string
        Domain to find subdomains for
  -dL string
        File containing list of domains to enumerate
  -exclude-sources string
        List of sources to exclude from enumeration
  -ls
        List all available sources
  -max-time int
        Minutes to wait for enumeration results (default 10)
  -nC
        Don't Use colors in output
  -nW
        Remove Wildcard & Dead Subdomains from output
  -o string
        File to write output to (optional)
  -oD string
        Directory to write enumeration results to (optional)
  -oI
        Write output in Host,IP format
  -oJ
        Write output in JSON lines Format
  -r string
        Comma-separated list of resolvers to use
  -rL string
        Text file containing list of resolvers to use
  -silent
        Show only subdomains in output
  -sources string
        Comma separated list of sources to use
  -t int
        Number of concurrent goroutines for resolving (default 10)
  -timeout int
        Seconds to wait before timing out (default 30)
  -v    Show Verbose output
  -version
        Show version of subfinder
```

## list of source

```
subfinder -ls


        _     __ _         _
____  _| |__ / _(_)_ _  __| |___ _ _
(_-< || | '_ \  _| | ' \/ _  / -_) '_|
/__/\_,_|_.__/_| |_|_||_\__,_\___|_| v2

                projectdiscovery.io

[WRN] Use with caution. You are responsible for your actions
[WRN] Developers assume no liability and are not responsible for any misuse or damage.
[WRN] By using subfinder, you also agree to the terms of the APIs used.

[INF] Configuration file saved to $HOME/.config/subfinder/config.yaml
[INF] Current list of available sources. [29]
[INF] Sources marked with an * needs key or token in order to work.
[INF] You can modify $HOME/.config/subfinder/config.yaml to configure your keys / tokens.

alienvault
archiveis
binaryedge *
bufferover
censys
certspotter *
certspotterold
commoncrawl
crtsh
dnsdumpster
dnsdb *
entrust
github *
hackertarget
ipv4info
intelx
passivetotal
rapiddns
securitytrails *
shodan *
sitedossier
spyse *
sublist3r
threatcrowd
threatminer
urlscan *
virustotal *
waybackarchive
zoomeye
```

## Examples

### simple use

```
subfinder -d projectdiscovery.io
```

```

        _     __ _         _
____  _| |__ / _(_)_ _  __| |___ _ _
(_-< || | '_ \  _| | ' \/ _  / -_) '_|
/__/\_,_|_.__/_| |_|_||_\__,_\___|_| v2

                projectdiscovery.io

[WRN] Use with caution. You are responsible for your actions
[WRN] Developers assume no liability and are not responsible for any misuse or damage.
[WRN] By using subfinder, you also agree to the terms of the APIs used.

[INF] Enumerating subdomains for projectdiscovery.io
blog.projectdiscovery.io
apollo.projectdiscovery.io
chaos.projectdiscovery.io
careers.projectdiscovery.io
nexus.projectdiscovery.io
chaos-data.projectdiscovery.io
dns.projectdiscovery.io
interact.projectdiscovery.io
nuclei.projectdiscovery.io
www-api.projectdiscovery.io
cdn.projectdiscovery.io
```

### result to json file

```
subfinder -d projectdiscovery.io -nW -oJ filename.json
```

```
{"host":"nexus.projectdiscovery.io","ip":"104.26.6.152"}
{"host":"dns.projectdiscovery.io","ip":"104.26.7.152"}
{"host":"cdn.projectdiscovery.io","ip":"104.26.7.152"}
{"host":"www.projectdiscovery.io","ip":"185.199.108.153"}
{"host":"careers.projectdiscovery.io","ip":"172.67.74.214"}
{"host":"nuclei.projectdiscovery.io","ip":"104.26.7.152"}
{"host":"interact.projectdiscovery.io","ip":"172.67.74.214"}
{"host":"blog.projectdiscovery.io","ip":"151.101.3.7"}
{"host":"projectdiscovery.io","ip":"172.67.74.214"}
{"host":"chaos-data.projectdiscovery.io","ip":"104.26.7.152"}
{"host":"www-api.projectdiscovery.io","ip":"172.67.74.214"}
{"host":"chaos.projectdiscovery.io","ip":"172.67.74.214"}
{"host":"apollo.projectdiscovery.io","ip":"104.26.6.152"}
```

## Home
https://projectdiscovery.io

## Github
https://github.com/projectdiscovery/subfinder

