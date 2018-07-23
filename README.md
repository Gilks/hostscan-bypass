# hostscan-bypass
Generate an OpenConnect Cisco Secure Desktop [(CSD)](http://www.infradead.org/openconnect/csd.html) file that bypasses AnyConnect hostscan requirements.

This script parses an AnyConnect client connection and outputs a CSD file that can be used with OpenConnect. The CSD file will perform a POST request to the AnyConnect server, giving the illusion a hostscan took place. Even if the AnyConnect server does not publish binaries for your Operating System (OS), you will still be able to connect. This is due to the fact that OpenConnect allows you to specify which OS you are connecting from. This means you can be on a Linux and pretend to be a Windows client! 

WARNING: Doing this will bypass the checks hostscan performs. This may be against your companies policy. By using this script and the resulting CSD file, you are releasing me of any liability. This script is for educational purposes only.


# Quick Start
*Note: You will need to install go. That process won't be covered here.

1. `sudo go run hostscan-bypass.go -l <YOUR IP> -p 443 -r <TARGET VPN URL>:443 -s`
2. Use AnyConnect and connect to `<YOUR IP>`
3. Wait. You do not need to enter in any credentials for hostscan to start. By default, the CSD file will be named `hostscan-bypass.sh`.
4. Make the CSD file executable (otherwise OpenConnect can't use it): `chmod +x hostscan-bypass.sh`
5. Finally, connect: `sudo openconnect --csd-wrapper=hostscan-bypass.sh <VPN URL> --os=win`

# Shout Outs
1. `hostscan-bypass.go` was hacked off of [tcpprox](https://github.com/staaldraad/tcpprox). Thanks [@staaldraad](https://github.com/staaldraad)!
2. Fromzy, who happened to posted the most [simple CSD](http://lists.infradead.org/pipermail/openconnect-devel/2015-January/002544.html) example
3. [@bmaddy](https://gist.github.com/bmaddy), who [posted examples](https://gist.github.com/bmaddy/dc720f494fa4de28ffc03cc6a472e965) and resources that aided in the completion of this project
