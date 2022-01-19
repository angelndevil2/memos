# OSWAP Amass

The OWASP Amass Project performs network mapping of attack surfaces and external asset discovery using open source information gathering and active reconnaissance techniques.

## --help
```
amass --help


        .+++:.            :                             .+++.
      +W@@@@@@8        &+W@#               o8W8:      +W@@@@@@#.   oW@@@W#+
     &@#+   .o@##.    .@@@o@W.o@@o       :@@#&W8o    .@#:  .:oW+  .@#+++&#&
    +@&        &@&     #@8 +@W@&8@+     :@W.   +@8   +@:          .@8
    8@          @@     8@o  8@8  WW    .@W      W@+  .@W.          o@#:
    WW          &@o    &@:  o@+  o@+   #@.      8@o   +W@#+.        +W@8:
    #@          :@W    &@+  &@+   @8  :@o       o@o     oW@@W+        oW@8
    o@+          @@&   &@+  &@+   #@  &@.      .W@W       .+#@&         o@W.
     WW         +@W@8. &@+  :&    o@+ #@      :@W&@&         &@:  ..     :@o
     :@W:      o@# +Wo &@+        :W: +@W&o++o@W. &@&  8@#o+&@W.  #@:    o@+
      :W@@WWWW@@8       +              :&W@@@@&    &W  .o#@@W&.   :W@WWW@@&
        +o&&&&+.                                                    +oooo.

                                                                     v3.15.2
                                           OWASP Amass Project - @owaspamass
                         In-depth Attack Surface Mapping and Asset Discovery


Usage: amass intel|enum|viz|track|db|dns [options]

  -h    Show the program usage message
  -help
        Show the program usage message
  -version
        Print the version number of this Amass binary


Subcommands:

        amass intel - Discover targets for enumerations
        amass enum  - Perform enumerations and network mapping
        amass viz   - Visualize enumeration results
        amass track - Track differences between enumerations
        amass db    - Manipulate the Amass graph database
        amass dns   - Resolve DNS names at high performance

The user's guide can be found here:
https://github.com/OWASP/Amass/blob/master/doc/user_guide.md

An example configuration file can be found here:
https://github.com/OWASP/Amass/blob/master/examples/config.ini

The Amass tutorial can be found here:
https://github.com/OWASP/Amass/blob/master/doc/tutorial.md
```

## amass intel --help

```

        .+++:.            :                             .+++.
      +W@@@@@@8        &+W@#               o8W8:      +W@@@@@@#.   oW@@@W#+
     &@#+   .o@##.    .@@@o@W.o@@o       :@@#&W8o    .@#:  .:oW+  .@#+++&#&
    +@&        &@&     #@8 +@W@&8@+     :@W.   +@8   +@:          .@8
    8@          @@     8@o  8@8  WW    .@W      W@+  .@W.          o@#:
    WW          &@o    &@:  o@+  o@+   #@.      8@o   +W@#+.        +W@8:
    #@          :@W    &@+  &@+   @8  :@o       o@o     oW@@W+        oW@8
    o@+          @@&   &@+  &@+   #@  &@.      .W@W       .+#@&         o@W.
     WW         +@W@8. &@+  :&    o@+ #@      :@W&@&         &@:  ..     :@o
     :@W:      o@# +Wo &@+        :W: +@W&o++o@W. &@&  8@#o+&@W.  #@:    o@+
      :W@@WWWW@@8       +              :&W@@@@&    &W  .o#@@W&.   :W@WWW@@&
        +o&&&&+.                                                    +oooo.

                                                                     v3.15.2
                                           OWASP Amass Project - @owaspamass
                         In-depth Attack Surface Mapping and Asset Discovery


Usage: amass intel [options] [-whois -d DOMAIN] [-addr ADDR -asn ASN -cidr CIDR]

  -active
        Attempt certificate name grabs
  -addr value
        IPs and ranges (192.168.1.1-254) separated by commas
  -asn value
        ASNs separated by commas (can be used multiple times)
  -cidr value
        CIDRs separated by commas (can be used multiple times)
  -config string
        Path to the INI configuration file. Additional details below
  -d value
        Domain names separated by commas (can be used multiple times)
  -demo
        Censor output to make it suitable for demonstrations
  -df value
        Path to a file providing root domain names
  -dir string
        Path to the directory containing the output files
  -ef string
        Path to a file providing data sources to exclude
  -exclude value
        Data source names separated by commas to be excluded
  -h    Show the program usage message
  -help
        Show the program usage message
  -if string
        Path to a file providing data sources to include
  -include value
        Data source names separated by commas to be included
  -ip
        Show the IP addresses for discovered names
  -ipv4
        Show the IPv4 addresses for discovered names
  -ipv6
        Show the IPv6 addresses for discovered names
  -list
        Print additional information
  -log string
        Path to the log file where errors will be written
  -max-dns-queries int
        Maximum number of concurrent DNS queries
  -o string
        Path to the text file containing terminal stdout/stderr
  -org string
        Search string provided against AS description information
  -p value
        Ports separated by commas (default: 80, 443)
  -r value
        IP addresses of preferred DNS resolvers (can be used multiple times)
  -rf value
        Path to a file providing preferred DNS resolvers
  -src
        Print data sources for the discovered names
  -timeout int
        Number of minutes to let enumeration run before quitting
  -v    Output status / debug / troubleshooting info
  -whois
        All provided domains are run through reverse whois

The user's guide can be found here:
https://github.com/OWASP/Amass/blob/master/doc/user_guide.md

An example configuration file can be found here:
https://github.com/OWASP/Amass/blob/master/examples/config.ini

The Amass tutorial can be found here:
https://github.com/OWASP/Amass/blob/master/doc/tutorial.md
```

## amass enum --help


```

        .+++:.            :                             .+++.
      +W@@@@@@8        &+W@#               o8W8:      +W@@@@@@#.   oW@@@W#+
     &@#+   .o@##.    .@@@o@W.o@@o       :@@#&W8o    .@#:  .:oW+  .@#+++&#&
    +@&        &@&     #@8 +@W@&8@+     :@W.   +@8   +@:          .@8
    8@          @@     8@o  8@8  WW    .@W      W@+  .@W.          o@#:
    WW          &@o    &@:  o@+  o@+   #@.      8@o   +W@#+.        +W@8:
    #@          :@W    &@+  &@+   @8  :@o       o@o     oW@@W+        oW@8
    o@+          @@&   &@+  &@+   #@  &@.      .W@W       .+#@&         o@W.
     WW         +@W@8. &@+  :&    o@+ #@      :@W&@&         &@:  ..     :@o
     :@W:      o@# +Wo &@+        :W: +@W&o++o@W. &@&  8@#o+&@W.  #@:    o@+
      :W@@WWWW@@8       +              :&W@@@@&    &W  .o#@@W&.   :W@WWW@@&
        +o&&&&+.                                                    +oooo.

                                                                     v3.15.2
                                           OWASP Amass Project - @owaspamass
                         In-depth Attack Surface Mapping and Asset Discovery


Usage: amass enum [options] -d DOMAIN

  -active
        Attempt zone transfers and certificate name grabs
  -addr value
        IPs and ranges (192.168.1.1-254) separated by commas
  -asn value
        ASNs separated by commas (can be used multiple times)
  -aw value
        Path to a different wordlist file for alterations
  -awm value
        "hashcat-style" wordlist masks for name alterations
  -bl value
        Blacklist of subdomain names that will not be investigated
  -blf string
        Path to a file providing blacklisted subdomains
  -brute
        Execute brute forcing after searches
  -cidr value
        CIDRs separated by commas (can be used multiple times)
  -config string
        Path to the INI configuration file. Additional details below
  -d value
        Domain names separated by commas (can be used multiple times)
  -demo
        Censor output to make it suitable for demonstrations
  -df value
        Path to a file providing root domain names
  -dir string
        Path to the directory containing the output files
  -ef string
        Path to a file providing data sources to exclude
  -exclude value
        Data source names separated by commas to be excluded
  -h    Show the program usage message
  -help
        Show the program usage message
  -if string
        Path to a file providing data sources to include
  -iface string
        Provide the network interface to send traffic through
  -include value
        Data source names separated by commas to be included
  -ip
        Show the IP addresses for discovered names
  -ipv4
        Show the IPv4 addresses for discovered names
  -ipv6
        Show the IPv6 addresses for discovered names
  -json string
        Path to the JSON output file
  -list
        Print the names of all available data sources
  -log string
        Path to the log file where errors will be written
  -max-depth int
        Maximum number of subdomain labels for brute forcing
  -max-dns-queries int
        Maximum number of DNS queries per second
  -min-for-recursive int
        Subdomain labels seen before recursive brute forcing (Default: 1) (default 1)
  -nf value
        Path to a file providing already known subdomain names (from other tools/sources)
  -noalts
        Disable generation of altered names
  -nocolor
        Disable colorized output
  -nolocaldb
        Disable saving data into a local database
  -norecursive
        Turn off recursive brute forcing
  -o string
        Path to the text file containing terminal stdout/stderr
  -oA string
        Path prefix used for naming all output files
  -p value
        Ports separated by commas (default: 80, 443)
  -passive
        Disable DNS resolution of names and dependent features
  -r value
        IP addresses of preferred DNS resolvers (can be used multiple times)
  -rf value
        Path to a file providing preferred DNS resolvers
  -scripts string
        Path to a directory containing ADS scripts
  -share
        Share findings with data source providers
  -silent
        Disable all output during execution
  -src
        Print data sources for the discovered names
  -timeout int
        Number of minutes to let enumeration run before quitting
  -v    Output status / debug / troubleshooting info
  -w value
        Path to a different wordlist file for brute forcing
  -wm value
        "hashcat-style" wordlist masks for DNS brute forcing

The user's guide can be found here:
https://github.com/OWASP/Amass/blob/master/doc/user_guide.md

An example configuration file can be found here:
https://github.com/OWASP/Amass/blob/master/examples/config.ini

The Amass tutorial can be found here:
https://github.com/OWASP/Amass/blob/master/doc/tutorial.md
```

### amass viz --help

```

        .+++:.            :                             .+++.
      +W@@@@@@8        &+W@#               o8W8:      +W@@@@@@#.   oW@@@W#+
     &@#+   .o@##.    .@@@o@W.o@@o       :@@#&W8o    .@#:  .:oW+  .@#+++&#&
    +@&        &@&     #@8 +@W@&8@+     :@W.   +@8   +@:          .@8
    8@          @@     8@o  8@8  WW    .@W      W@+  .@W.          o@#:
    WW          &@o    &@:  o@+  o@+   #@.      8@o   +W@#+.        +W@8:
    #@          :@W    &@+  &@+   @8  :@o       o@o     oW@@W+        oW@8
    o@+          @@&   &@+  &@+   #@  &@.      .W@W       .+#@&         o@W.
     WW         +@W@8. &@+  :&    o@+ #@      :@W&@&         &@:  ..     :@o
     :@W:      o@# +Wo &@+        :W: +@W&o++o@W. &@&  8@#o+&@W.  #@:    o@+
      :W@@WWWW@@8       +              :&W@@@@&    &W  .o#@@W&.   :W@WWW@@&
        +o&&&&+.                                                    +oooo.

                                                                     v3.15.2
                                           OWASP Amass Project - @owaspamass
                         In-depth Attack Surface Mapping and Asset Discovery


Usage: amass viz -d3|-dot||-gexf|-graphistry|-maltego [options]

  -config string
        Path to the INI configuration file. Additional details below
  -d value
        Domain names separated by commas (can be used multiple times)
  -d3
        Generate the D3 v4 force simulation HTML file
  -df string
        Path to a file providing root domain names
  -dir string
        Path to the directory containing the graph database
  -dot
        Generate the DOT output file
  -enum int
        Identify an enumeration via an index from the listing
  -gexf
        Generate the Gephi Graph Exchange XML Format (GEXF) file
  -graphistry
        Generate the Graphistry JSON file
  -h    Show the program usage message
  -help
        Show the program usage message
  -i string
        The Amass data operations JSON file
  -maltego
        Generate the Maltego csv file
  -nocolor
        Disable colorized output
  -o string
        Path to the directory for output files being generated
  -silent
        Disable all output during execution

The user's guide can be found here:
https://github.com/OWASP/Amass/blob/master/doc/user_guide.md

An example configuration file can be found here:
https://github.com/OWASP/Amass/blob/master/examples/config.ini

The Amass tutorial can be found here:
https://github.com/OWASP/Amass/blob/master/doc/tutorial.md
```

### amass track --help

```

        .+++:.            :                             .+++.
      +W@@@@@@8        &+W@#               o8W8:      +W@@@@@@#.   oW@@@W#+
     &@#+   .o@##.    .@@@o@W.o@@o       :@@#&W8o    .@#:  .:oW+  .@#+++&#&
    +@&        &@&     #@8 +@W@&8@+     :@W.   +@8   +@:          .@8
    8@          @@     8@o  8@8  WW    .@W      W@+  .@W.          o@#:
    WW          &@o    &@:  o@+  o@+   #@.      8@o   +W@#+.        +W@8:
    #@          :@W    &@+  &@+   @8  :@o       o@o     oW@@W+        oW@8
    o@+          @@&   &@+  &@+   #@  &@.      .W@W       .+#@&         o@W.
     WW         +@W@8. &@+  :&    o@+ #@      :@W&@&         &@:  ..     :@o
     :@W:      o@# +Wo &@+        :W: +@W&o++o@W. &@&  8@#o+&@W.  #@:    o@+
      :W@@WWWW@@8       +              :&W@@@@&    &W  .o#@@W&.   :W@WWW@@&
        +o&&&&+.                                                    +oooo.

                                                                     v3.15.2
                                           OWASP Amass Project - @owaspamass
                         In-depth Attack Surface Mapping and Asset Discovery


Usage: amass track [options] -d domain

  -config string
        Path to the INI configuration file. Additional details below
  -d value
        Domain names separated by commas (can be used multiple times)
  -df string
        Path to a file providing root domain names
  -dir string
        Path to the directory containing the graph database
  -h    Show the program usage message
  -help
        Show the program usage message
  -history
        Show the difference between all enumeration pairs
  -last int
        The number of recent enumerations to include in the tracking
  -nocolor
        Disable colorized output
  -silent
        Disable all output during execution
  -since string
        Exclude all enumerations before (format: 01/02 15:04:05 2006 MST)

The user's guide can be found here:
https://github.com/OWASP/Amass/blob/master/doc/user_guide.md

An example configuration file can be found here:
https://github.com/OWASP/Amass/blob/master/examples/config.ini

The Amass tutorial can be found here:
https://github.com/OWASP/Amass/blob/master/doc/tutorial.md
```

### amass db --help

```

        .+++:.            :                             .+++.
      +W@@@@@@8        &+W@#               o8W8:      +W@@@@@@#.   oW@@@W#+
     &@#+   .o@##.    .@@@o@W.o@@o       :@@#&W8o    .@#:  .:oW+  .@#+++&#&
    +@&        &@&     #@8 +@W@&8@+     :@W.   +@8   +@:          .@8
    8@          @@     8@o  8@8  WW    .@W      W@+  .@W.          o@#:
    WW          &@o    &@:  o@+  o@+   #@.      8@o   +W@#+.        +W@8:
    #@          :@W    &@+  &@+   @8  :@o       o@o     oW@@W+        oW@8
    o@+          @@&   &@+  &@+   #@  &@.      .W@W       .+#@&         o@W.
     WW         +@W@8. &@+  :&    o@+ #@      :@W&@&         &@:  ..     :@o
     :@W:      o@# +Wo &@+        :W: +@W&o++o@W. &@&  8@#o+&@W.  #@:    o@+
      :W@@WWWW@@8       +              :&W@@@@&    &W  .o#@@W&.   :W@WWW@@&
        +o&&&&+.                                                    +oooo.

                                                                     v3.15.2
                                           OWASP Amass Project - @owaspamass
                         In-depth Attack Surface Mapping and Asset Discovery


Usage: amass db [options]

  -config string
        Path to the INI configuration file. Additional details below
  -d value
        Domain names separated by commas (can be used multiple times)
  -demo
        Censor output to make it suitable for demonstrations
  -df string
        Path to a file providing root domain names
  -dir string
        Path to the directory containing the graph database
  -enum int
        Identify an enumeration via an index from the listing
  -h    Show the program usage message
  -help
        Show the program usage message
  -ip
        Show the IP addresses for discovered names
  -ipv4
        Show the IPv4 addresses for discovered names
  -ipv6
        Show the IPv6 addresses for discovered names
  -json string
        Path to the JSON output file
  -list
        Numbered list of enums filtered on provided domains
  -names
        Print Just Discovered Names
  -nocolor
        Disable colorized output
  -o string
        Path to the text file containing terminal stdout/stderr
  -show
        Print the results for the enumeration index + domains provided
  -silent
        Disable all output during execution
  -src
        Print data sources for the discovered names
  -summary
        Print Just ASN Table Summary

The user's guide can be found here:
https://github.com/OWASP/Amass/blob/master/doc/user_guide.md

An example configuration file can be found here:
https://github.com/OWASP/Amass/blob/master/examples/config.ini

The Amass tutorial can be found here:
https://github.com/OWASP/Amass/blob/master/doc/tutorial.md
```

### amass dns --help

```

        .+++:.            :                             .+++.
      +W@@@@@@8        &+W@#               o8W8:      +W@@@@@@#.   oW@@@W#+
     &@#+   .o@##.    .@@@o@W.o@@o       :@@#&W8o    .@#:  .:oW+  .@#+++&#&
    +@&        &@&     #@8 +@W@&8@+     :@W.   +@8   +@:          .@8
    8@          @@     8@o  8@8  WW    .@W      W@+  .@W.          o@#:
    WW          &@o    &@:  o@+  o@+   #@.      8@o   +W@#+.        +W@8:
    #@          :@W    &@+  &@+   @8  :@o       o@o     oW@@W+        oW@8
    o@+          @@&   &@+  &@+   #@  &@.      .W@W       .+#@&         o@W.
     WW         +@W@8. &@+  :&    o@+ #@      :@W&@&         &@:  ..     :@o
     :@W:      o@# +Wo &@+        :W: +@W&o++o@W. &@&  8@#o+&@W.  #@:    o@+
      :W@@WWWW@@8       +              :&W@@@@&    &W  .o#@@W&.   :W@WWW@@&
        +o&&&&+.                                                    +oooo.

                                                                     v3.15.2
                                           OWASP Amass Project - @owaspamass
                         In-depth Attack Surface Mapping and Asset Discovery


Usage: amass dns [options]

  -bl value
        Blacklist of subdomain names that will not be investigated
  -blf string
        Path to a file providing blacklisted subdomains
  -config string
        Path to the INI configuration file. Additional details below
  -d value
        Domain names separated by commas (can be used multiple times)
  -demo
        Censor output to make it suitable for demonstrations
  -df value
        Path to a file providing root domain names
  -dir string
        Path to the directory containing the output files
  -h    Show the program usage message
  -help
        Show the program usage message
  -ip
        Show the IP addresses for discovered names
  -ipv4
        Show the IPv4 addresses for discovered names
  -ipv6
        Show the IPv6 addresses for discovered names
  -json string
        Path to the JSON output file
  -log string
        Path to the log file where errors will be written
  -max-dns-queries int
        Maximum number of concurrent DNS queries
  -nf value
        Path to a file providing already known subdomain names (from other tools/sources)
  -o string
        Path to the text file containing terminal stdout/stderr
  -oA string
        Path prefix used for naming all output files
  -r value
        IP addresses of preferred DNS resolvers (can be used multiple times)
  -rf value
        Path to a file providing preferred DNS resolvers
  -t value
        DNS record types to be queried for (can be used multiple times)
  -timeout int
        Number of minutes to let enumeration run before quitting
  -v    Output status / debug / troubleshooting info

The user's guide can be found here:
https://github.com/OWASP/Amass/blob/master/doc/user_guide.md

An example configuration file can be found here:
https://github.com/OWASP/Amass/blob/master/examples/config.ini

The Amass tutorial can be found here:
https://github.com/OWASP/Amass/blob/master/doc/tutorial.md
```


# Github
https://github.com/OWASP/Amass