# Subcommands

* amass intel -- Discover targets for enumerations
* amass enum -- Perform enumerations and network mapping
* amass viz -- Visualize enumeration results
* amass track -- Track differences between enumerations
* amass db -- Manipulate the Amass graph database

# Run Amass under Passive or Active Configuration

Amass enum can be executed under the context of a passive or an active configuration mode. The passive mode is much quicker, but Amass will not validate DNS information, for example by resolving the subdomains. You can run it passively using the “-passive” flag and you will not be able to enable many techniques or configurations, such as DNS resolution and validation. There are several reasons for choosing passive mode over the active mode at times, for example:

* You need to know all possible subdomains that have been used and may be reused in the future, perhaps because you need to constantly monitor the target’s attack surface for changes or because you are working on a phishing engagement and looking for subdomains.
* Your perimeter’s security testing process validates DNS information at a later stage and need Amass results quickly.
* Due to a security engagement’s constraints or requirements, you can only perform passive information gathering.

---
<https://github.com/OWASP/Amass/blob/master/doc/tutorial.md>