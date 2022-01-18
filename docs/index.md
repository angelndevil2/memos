[OSNT](osint.md) | [dns enumeration](dnsenumeration.md)

# [Where automation should stop, and end][1]

Automation is another highly misunderstood rabbit hole of bug bounties. If your automation consists of running popular [ethical hacking tools](https://securitytrails.com/blog/best-ethical-hacking-tools) and looking for what everybody else is (such as default subdomain takeovers), your returns are going to be low and you’ll experience a high number of duplicates. Even as recently as two years ago, automation would show value anywhere that you pointed it; these days, however, most common vulnerabilities are claimed within minutes, not hours.

That’s not to say automation doesn’t have value—it most certainly does. However, when it comes to automation today, unless you’re already well established and have a depth of knowledge to draw upon, it should be used to track points of change and identify new attack surfaces. Given that speed is important, it’s also important to understand what is touching a target (active), and what isn’t (passive).

## Active recon

Active recon consists of running tools where your own IP (or VPS IP) will make a request to the target. This takes many forms, ranging from directory brute forcing, crawling the website, or DNS brute forcing. The challenge with this type of recon is that you’ll often be unable to perform it as regularly as you’d like and catch points of change. It’s more important to throttle and time targeted requests (a tailored wordlist of 50 items is far superior to one of 100k+ items) and use those to expand upon your hunting. If you want to track more regular change, monitoring of passive sources should be where you put your focus.

## Passive recon

Passive recon is where you use data sources that monitor asset spaces for you. Performing these queries is extremely flexible, ranging from [Subfinder](https://github.com/projectdiscovery/subfinder), [AMASS](https://github.com/OWASP/Amass), [Microsubs](https://github.com/codingo/microsubs), and more.

The key benefit of monitoring targets in this manner is that you’re not risking a program ban or escalation that could see you receiving penalties from a bounty platform.


# Tools

* [subfinder](subfinder.md) - subdomain finder
* [amass](amass/amass.md) - open source network mapping and attack surface discovery tool

---

[1]:https://securitytrails.com/blog/the-most-misunderstood-element-recon (The Most Misunderstood Element: Recon)