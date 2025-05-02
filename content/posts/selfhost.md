+++
date = '2025-05-02T14:52:51-04:00'
title = 'My Homelab'
+++

For a few years now, I've been self-hosting a media server so I can stream my media collection.

## Why?

The power consumption of running my own media server is minimal compared to the savings of cancelling Netflix, Max, Disney+, and Hulu. Also I like tinkering.

## Hardware

Years ago, I bought a used Dell Optiplex from the local university's surplus store. It cost less than $100, and has been running for nearly a decade now. A hard drive was not included, so I bought a 1TB hard disk from the same place for an additional $15.

After a couple years, that hard drive started making noises, which is the sign of immanent hard drive failure. I can't remember where I bought the replacement hard drive, but I found a 4TB for cheap on some website or other. Dell did a really nice job of making Optiplex machines easy to work on. The hard drive mount is nicely accessible, and it was laughably simple to install the replacement.

A couple years ago, I ~~stole~~ acquired a used uninterruptible power supply (UPS) from my workplace. For some reason this three-employee small office had a Dell R760 server in the closet that was serving absolutely no purpose whatsoever except drawing a lot of power and making a lot of noise. The only thing running on it was a DHCP server, which was silly since the router it was plugged into had DHCP built in! I unplugged the server and the UPS somehow found its way into my car. My apartment loses power a lot, so this UPS has been a lifesaver.

The Optiplex doesn't have a wifi chip, and I really don't care about wireless. I have an Ethernet cable running from my apartment's router to a TP-Link unmanaged switch, and cables running from the switch to my smart TV (I hate smart TVs but you can't hardly get dumb ones anymore), Optiplex, and two different desktops.

Soon I'll add a proper hardware firewall running pfSense, but hardware is expensive, and a raspberry pi running OpenWrt will do for now.

## Software

### Operating System

For the first couple of years, I was running Ubuntu Server. I have some philosophical disagreements with Canonical, though, so I switched to Debian and forced myself to learn how to copy my SSH key over and disable password authentication, which is really the only advantage Ubuntu had for my use-case. I installed `unattended-upgrades` so my system won't fall behind on critical security patches. Lately, I've been considering trying to switch to [ucore](https://github.com/ublue-os/ucore), but that's going to require a whole lot of extra work and learning.

### Packages

For a while, I was using Plex to serve media from the Optiplex to my TV. However, I found the ads annoying and generally prefer open-source software. I switched to [Jellyfin](https://jellyfin.org/) as soon as I heard about it. Jellyfin is missing a couple of obscure features that Plex has, but I didn't use any of them.

I have dabbled in pihole and Adguard Home, but the other people in my apartment complained that my filters were blocking something or other, so I just configure my own devices to point to [Mullvad's public DNS server](https://mullvad.net/en/help/dns-over-https-and-dns-over-tls).

For many years, Jellyfin alone was enough to satisfy my needs. Thankfully, around the end of last year, Spotify started to get bad. I don't use Spotify, but my partner depends on it for music, podcasts, and audiobooks, despite my many attempts to convert him to open-source replacements. He likes the recommendations and auto-generated playlists and stuff.

I seized the opportunity to look into ways of making the homelab accessible from outside the house, as well as expand its functionality beyond a mere media server. Since I'm a grad student now, something that was simple to set up was also ideal. I would love to run everything through [podman](https://podman.io/), but I just don't have the time to learn it.

I considered using [Tailscale](https://tailscale.com/) to solve the remote access problem. This would work great to establish an encrypted connection between my partner's device and the server, but it would be less than ideal for me. I use Mullvad VPN on my phone, and I would either have to annoyingly switch between VPNs or pay for Tailscale's Mullvad integration, and neither of those options sounded very good.

For automatic software management, I looked into [CasaOS](https://casaos.zimaspace.com/) and [umbrelOS](https://umbrel.com/umbrelos), both of which offer one-click installation of docker containers. Both are, however, developed specifically to sell their own hardware, so functionality on third party devices is somewhat limited, and this business model reminds me too much of Apple and leaves a bad taste in my mouth.

In the end, I settled on [YunoHost](https://yunohost.org/), which is built on Debian Stable. It offers one-click installation and has a massive application catalog. It deploys native packages instead of docker containers, which I consider a slight downside, but it does have one standout feature that other options I considered lacked: built-in dynamic DNS. So long as I use one of their provided subdomains, the remote access problem is no longer a problem. Let's Encrypt integration works out of the box, too. I just had to open ports 80 and 443 on my firewall to allow web traffic.

I rather painlessly installed Jellyfin, [audiobookshelf](https://www.audiobookshelf.org/), and [Nextcloud](https://nextcloud.com/) (my partner is always running out of storage on his phone), and everything has been running perfectly for a whole 24+ hours now. Huzzah.

Of course, if you decide to use YunoHost, make sure to follow the security recommendations, beef up your firewall, and use encryption. Exposing your homelab to the public Internet carries additional risk.

## Conclusion

I have some ideas kicking around in my head for homelab improvements, but most of them require more money, space, and time than I'm willing to spend right now. The current setup is functional, but far from ideal. I'm not really much of a tech girlie, though. I consider tinkering more of a brain puzzle than a passion, like doing sudoku on the toilet to keep your mind sharp. So this will do for now.