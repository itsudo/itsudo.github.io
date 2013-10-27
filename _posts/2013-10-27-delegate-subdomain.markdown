---
layout: post
title:  "Howto delegate a subdomain to another nameserver"
date:   2013-10-27 11:28:31
categories: dns
---

My main dns hosting is [Zerigo](http://www.zerigo.com). As my servers are on digitalocean and they host PTR records for those servers, for consistency I wanted to host A records for my servers there too. It was ages ago when I last played with subdomain delegation, so had to spent couple of minutes digging on what to set on zerigo, to enable that. Hope, that it helps somebody

Set NS records for your subdomain (in my case servers.itsudo.com) and in DATA field put a nameserver

	servers.itsudo.com NS ns1.digitalocean.com
	servers.itsudo.com NS ns2.digitalocean.com
	servers.itsudo.com NS ns3.digitalocean.com


Then create a new zone servers.itsudo.com on digital ocean and you can start adding A records for your new subdomain, like:

	server1.servers.itsudo.com
