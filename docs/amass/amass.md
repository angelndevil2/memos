[help](amass-help.md)

# Run Amass under Passive or Active Configuration

Amass enum can be executed under the context of a passive or an active configuration mode. The passive mode is much quicker, but Amass will not validate DNS information, for example by resolving the subdomains. You can run it passively using the “-passive” flag and you will not be able to enable many techniques or configurations, such as DNS resolution and validation. There are several reasons for choosing passive mode over the active mode at times, for example:

* You need to know all possible subdomains that have been used and may be reused in the future, perhaps because you need to constantly monitor the target’s attack surface for changes or because you are working on a phishing engagement and looking for subdomains.
* Your perimeter’s security testing process validates DNS information at a later stage and need Amass results quickly.
* Due to a security engagement’s constraints or requirements, you can only perform passive information gathering.

# Usage

## subdomain enum
```
amass enum -d owasp.org -active -json amass.enum.`date +%y%m%d`.json -o amass.enum.`date +%y%m%d`.txt
```
out
```
training.owasp.org
calendar.owasp.org
groups.owasp.org
name-virt-host.owasp.org
gapps.owasp.org
sl.owasp.org
brainbreak.owasp.org
www2.owasp.org
calltobattle.owasp.org
owasp.org
austin.owasp.org
www.owasp.org
contact.owasp.org
admin.owasp.org
kerala.owasp.org
ocms.owasp.org
docs.owasp.org
dev.owasp.org
mail.owasp.org
videos.owasp.org
members.owasp.org
cheatsheetseries.owasp.org
wiki.owasp.org
lists.owasp.org
lightning.owasp.org
secureflag.owasp.org
20thanniversary.owasp.org
training-12.owasp.org

OWASP Amass v3.15.2                               https://github.com/OWASP/Amass
--------------------------------------------------------------------------------
28 names discovered - scrape: 5, dns: 1, alt: 1, api: 21
--------------------------------------------------------------------------------
ASN: 13335 - CLOUDFLARENET - Cloudflare, Inc.
        2606:4700:10::/44       28   Subdomain Name(s)
        104.16.0.0/12           54   Subdomain Name(s)
        172.67.0.0/16           27   Subdomain Name(s)
        2606:4700::/32          52   Subdomain Name(s)
ASN: 16509 - AMAZON-02 - Amazon.com, Inc.
        99.84.40.0/21           4    Subdomain Name(s)

The enumeration has finished
Discoveries are being migrated into the local database
```

out txt
```
training.owasp.org
calendar.owasp.org
groups.owasp.org
name-virt-host.owasp.org
gapps.owasp.org
sl.owasp.org
brainbreak.owasp.org
www2.owasp.org
calltobattle.owasp.org
owasp.org
austin.owasp.org
www.owasp.org
contact.owasp.org
admin.owasp.org
kerala.owasp.org
ocms.owasp.org
docs.owasp.org
dev.owasp.org
mail.owasp.org
videos.owasp.org
members.owasp.org
cheatsheetseries.owasp.org
wiki.owasp.org
lists.owasp.org
lightning.owasp.org
secureflag.owasp.org
20thanniversary.owasp.org
training-12.owasp.org
```

out json
```
{"name":"training.owasp.org","domain":"owasp.org","addresses":[{"ip":"2606:4700:10::ac43:a27","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.26.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"172.67.10.39","cidr":"172.67.0.0/16","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1a4d","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.27.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."}],"tag":"api","sources":["BufferOver"]}
{"name":"calendar.owasp.org","domain":"owasp.org","addresses":[{"ip":"2606:4700:10::ac43:a27","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1a4d","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.27.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.26.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1b4d","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"172.67.10.39","cidr":"172.67.0.0/16","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."}],"tag":"scrape","sources":["AbuseIPDB"]}
{"name":"groups.owasp.org","domain":"owasp.org","addresses":[{"ip":"2606:4700:10::ac43:a27","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1b4d","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.27.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"172.67.10.39","cidr":"172.67.0.0/16","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1a4d","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.26.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."}],"tag":"scrape","sources":["AbuseIPDB"]}
{"name":"name-virt-host.owasp.org","domain":"owasp.org","addresses":[{"ip":"104.22.26.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"172.67.10.39","cidr":"172.67.0.0/16","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1b4d","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::ac43:a27","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.27.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1a4d","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."}],"tag":"api","sources":["BufferOver"]}
{"name":"gapps.owasp.org","domain":"owasp.org","addresses":[{"ip":"104.22.27.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"172.67.10.39","cidr":"172.67.0.0/16","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.26.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1a4d","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1b4d","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::ac43:a27","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."}],"tag":"api","sources":["BufferOver"]}
{"name":"sl.owasp.org","domain":"owasp.org","addresses":[{"ip":"104.22.27.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1a4d","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::ac43:a27","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"172.67.10.39","cidr":"172.67.0.0/16","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1b4d","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.26.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."}],"tag":"api","sources":["BufferOver"]}
{"name":"brainbreak.owasp.org","domain":"owasp.org","addresses":[{"ip":"172.67.10.39","cidr":"172.67.0.0/16","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.27.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::ac43:a27","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.26.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1b4d","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1a4d","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."}],"tag":"api","sources":["BufferOver"]}
{"name":"www2.owasp.org","domain":"owasp.org","addresses":[{"ip":"104.22.26.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.27.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1b4d","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1a4d","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"172.67.10.39","cidr":"172.67.0.0/16","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::ac43:a27","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."}],"tag":"api","sources":["BufferOver"]}
{"name":"calltobattle.owasp.org","domain":"owasp.org","addresses":[{"ip":"2606:4700:10::ac43:a27","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"172.67.10.39","cidr":"172.67.0.0/16","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1a4d","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.27.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.26.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1b4d","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."}],"tag":"api","sources":["BufferOver"]}
{"name":"owasp.org","domain":"owasp.org","addresses":[{"ip":"172.67.10.39","cidr":"172.67.0.0/16","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.26.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1b4d","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::ac43:a27","cidr":"2606:4700:10::/44","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.27.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1a4d","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."}],"tag":"dns","sources":["DNS","BufferOver","AbuseIPDB","Riddler"]}
{"name":"austin.owasp.org","domain":"owasp.org","addresses":[{"ip":"104.22.27.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.26.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1a4d","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::ac43:a27","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1b4d","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"172.67.10.39","cidr":"172.67.0.0/16","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."}],"tag":"api","sources":["BufferOver"]}
{"name":"www.owasp.org","domain":"owasp.org","addresses":[{"ip":"2606:4700:10::6816:1b4d","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::ac43:a27","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.27.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.26.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1a4d","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"172.67.10.39","cidr":"172.67.0.0/16","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."}],"tag":"api","sources":["BufferOver"]}
{"name":"contact.owasp.org","domain":"owasp.org","addresses":[{"ip":"104.22.27.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"172.67.10.39","cidr":"172.67.0.0/16","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1b4d","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.26.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1a4d","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::ac43:a27","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."}],"tag":"api","sources":["BufferOver"]}
{"name":"admin.owasp.org","domain":"owasp.org","addresses":[{"ip":"104.22.27.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::ac43:a27","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"172.67.10.39","cidr":"172.67.0.0/16","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1b4d","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1a4d","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.26.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."}],"tag":"scrape","sources":["Riddler"]}
{"name":"kerala.owasp.org","domain":"owasp.org","addresses":[{"ip":"2606:4700:10::ac43:a27","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.27.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.26.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1b4d","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1a4d","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"172.67.10.39","cidr":"172.67.0.0/16","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."}],"tag":"api","sources":["BufferOver"]}
{"name":"ocms.owasp.org","domain":"owasp.org","addresses":[{"ip":"2606:4700:10::6816:1b4d","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"172.67.10.39","cidr":"172.67.0.0/16","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.26.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.27.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::ac43:a27","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1a4d","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."}],"tag":"api","sources":["BufferOver"]}
{"name":"docs.owasp.org","domain":"owasp.org","addresses":[{"ip":"2606:4700:10::6816:1a4d","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::ac43:a27","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.26.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"172.67.10.39","cidr":"172.67.0.0/16","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.27.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1b4d","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."}],"tag":"scrape","sources":["AbuseIPDB"]}
{"name":"dev.owasp.org","domain":"owasp.org","addresses":[{"ip":"2606:4700:10::ac43:a27","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.27.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"104.22.26.77","cidr":"104.16.0.0/12","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1a4d","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"172.67.10.39","cidr":"172.67.0.0/16","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."},{"ip":"2606:4700:10::6816:1b4d","cidr":"2606:4700::/32","asn":13335,"desc":"CLOUDFLARENET - Cloudflare, Inc."}],"tag":"api","sources":["BufferOver"]}
```