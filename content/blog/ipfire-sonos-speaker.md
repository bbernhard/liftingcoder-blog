+++
title = "Ipfire, Unifi and Sonos speakers"
date = "2026-03-10T13:01:25+02:00"

#
# description is optional
#
# description = "An optional description for SEO. If not provided, an automatically created summary will be used."

thumbnail = "/images/ipfire-tux.png"
tags = ["projects",]
+++

I don't like Sonos Speaker. In my opinion they are overpriced and their App is buggy. However, my girlfriend owns three Sonos Speaker and when we moved together I had to integrate them into my home network. Initially I just connected them via WiFi. That was working fine for several months. However, at one point the Sonos App couldn't find the speakers anymore. No matter how often I did reset the speakers, they just didn't show up in the app anymore. I did a bit of research and it turned out that it could be related to the Wifi Settings. I am using Unifi Access Points and Sonos seems to be a bit picky when it comes to the Wireless Radio settings. I tried to play with the Wifi Settings for several hours, but no matter what I did, I couldn't reliably connect the speakers.

After wasting a whole afternoon, I got frustrated and ordered a bunch of network cables to connect them all via cable. I was pretty confident that this would finally solve the connection problems once and for all.The more I was surprised when I still couldn't find the Sonos speakers in the Sonos App. What is going on here? That doesn't make any sense.

At this point you must know that I am using Ipfire - a zone based firewall - which per default uses different zones (=subnets) for wired and wireless connections. One of their core principles is, that devices in the `BLUE` zone (the zone for wireless devices) per default can't reach the devices in the `GREEN` zone (the zone for wired devices). But although I've created a firewall rule to allow traffic from the Sonos App on my smartphone to the Sonos Speakers, the Sonos App still didn't find any devices. That was weird. What's going on here?

After a bit more research it turned out that Sonos uses mDNS for the device discovery. The problem was, that the mDNS messages aren't broadcasted across interfaces. However, this can easily be solved by installing the [mdns-repeater](https://www.ipfire.org/docs/addons/mdns-repeater) Addon from the Ipfire Package manager. This package re-broadcasts mDNS messages from one interface to another. After installing this package everything is finally working again.
