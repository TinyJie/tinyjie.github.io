---
layout: post
title: Use squid3 to establish muti-stage proxy
categories:
- blog
---
We have a cluster with 7 nodes but only one of these nodes has a visible IP address to outer networks. We call this node "main node" to discriminate from ohter nodes. The main node can access internet through a system wide proxy by setting up the "http_proxy" and "https_proxy" env. The http proxy server runs on my mac which can be accessed by the main node. But the rest of the nodes can not use this http proxy directly for they are hidden from my mac pc. To tackle this problem we establish a squid3 proxy server on main node to redirect all packages from other nodes to the proxy server on my mac. You can refer to this [post](http://soad1982.blogspot.com/2010/02/squid-redirect-to-another-proxy.html) for more details.  

## Basic commands
start squid3

> $ squid3

restart squid3

> $ sudo service squid3 restart

## Configure squid3
Add the following lines to `\etc\squid3\squid3.conf` to redirect parent prxoy server.

>cache_peer YOURPROXY  parent PROXY-PORT 0 no-digest\\
 never_direct allow all

Just replace YOURPROXY with the ip address and the PROXY-PORT for the port number.

