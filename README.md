# Hostscan Bypass
Generate an OpenConnect Cisco Secure Desktop [(CSD)](http://www.infradead.org/openconnect/csd.html) file that bypasses AnyConnect hostscan requirements.

This script parses an AnyConnect client connection and outputs a CSD file that can be used with OpenConnect. The CSD file will perform a POST request to the AnyConnect server, giving the illusion a hostscan took place. Even if the AnyConnect server does not publish binaries for your Operating System (OS), you will still be able to connect. This is due to the fact that OpenConnect allows you to specify which OS you are connecting from. This means you can be on a Linux box and pretend to be a Windows client! 

**WARNING:** Doing this will bypass the checks hostscan performs. This may be against your company's policy. By using this script and the resulting CSD file, you are using these files at your own risk. This script is for educational purposes only.

# Using MacOS with the Hostscan Bypass
The hostscan bypass was originally coded and tested against a Windows machine running AnyConnect. I do not personally have the resources to troubleshoot issues on MacOS. However,  [@cjbirk](https://github.com/cjbirk) did a bit of troubleshooting and successfully generated a CSD file using the bypass on MacOS. Please see [this issue](https://github.com/Gilks/hostscan-bypass/issues/4#issuecomment-461288105) for suggestions on troubleshooting any mac related issues. 

# Blog
You can find the associated blog for this tool [here](https://gilks.github.io/post/cisco-hostscan-bypass).

# Quick Start
Note: You will need to install go. That process won't be covered here.

1. `sudo go run hostscan-bypass.go -l <YOUR IP> -p 443 -r <TARGET VPN URL>:443 -s`
2. Use AnyConnect and connect to `<YOUR IP>`
3. Wait. You do not need to enter in any credentials for hostscan to start. By default, the CSD file will be named `hostscan-bypass.sh`.
4. Make the CSD file executable (otherwise OpenConnect can't use it): `chmod +x hostscan-bypass.sh`
5. Finally, connect: `sudo openconnect --csd-wrapper=hostscan-bypass.sh <VPN URL> --os=win`

# Shout Outs
1. `hostscan-bypass.go` was hacked off of [tcpprox](https://github.com/staaldraad/tcpprox). Thanks [@staaldraad](https://github.com/staaldraad)!
2. Fromzy, who posted the most [simple CSD](http://lists.infradead.org/pipermail/openconnect-devel/2015-January/002544.html) example
3. [@bmaddy](https://github.com/bmaddy), who [posted examples](https://gist.github.com/bmaddy/dc720f494fa4de28ffc03cc6a472e965) and resources that aided in the completion of this project
4. [@cjbirk](https://github.com/cjbirk) for taking the time to figure out how to successfully intercept AnyConnect on MacOS!
