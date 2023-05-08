NOTE: Currently this is copied directly from a file in Obsidian. A bunch of formatting and internal linking is currently broken, but I wanted a way to get this text live to start sharing it. There are still sections being worked on, filler text in some spots, and general improvments to be made. I am by no means an expoert on these topics, but I have spent a lot of time digesting the information from others and feel I have an okay sense coupled with an ability to put things in very understandable terms.

# LifeOS (Working Title)
#tech #decentralize #software #hardware 
### Doomsday Prepping for the Internet Apocalypse
A framework for a personal digital footprint that gives full control to the owner with options to sync, share, and expand as decided by the owner of the data and only the owner of the data.


## Table of Contents
- [Introduction](#introduction)
	- [Overview](#overview)
	- [Reason and "Qualifications"](#reason-and-"rualifications")
	- [Goals](#goals)
- [Core Concepts](#core-concepts)
	- [Private](#private)
	- [Self Hosted](#self-hosted)
	- [Offline](#"offline")
	- [Scalable](#scalable)
	- [As Free As Possible](#as-free-as-possible])
- [Software](#software)
	- [Telegram](#telegram)
		- [Overview](#telegram#overview)
		- [[LifeOS#Telegram#Install|Install]]
	- [[#KeePassXC]]
		- [[LifeOS#KeepassXC#Overview|Overview]]
		- [[LifeOS#KeePassXC#Install|Install]]
	[[#PiHole]]
		[[LifeOS#PiHole#Overview|Overview]]
		[[LifeOS#PiHole#Install|Install]]
	[[#VPN]]
		[[LifeOS#VPN#Overview|Overview]]
		[[LifeOS#VPN#Install|Install]]
	[[#Syncthing]]
		[[LifeOS#Syncthing#Overview|Overview]]
		[[LifeOS#Syncthing#Install|Install]]
	[[#Tailscale]]
		[[LifeOS#Tailscale#Overview|Overview]]
		[[LifeOS#Tailscale#Install|Install]]
	[[#Obsidian]]
		[[LifeOS#Obsidian#Overview|Overview]]
		[[LifeOS#Ovsidian#Install|Install]]
[[#Hardware Overview]]
	[[#Networking Devices]]
		[[LifeOS#Networking Devices#Overview|Overview]]
		[[LifeOS#Networking Devices#Setup|Setup]]
	[[#SBC and Linux]]
		[[LifeOS#SBC and Linux#Overview|Overview]]
		[[LifeOS#SBC and Linux#Setup|Setup]]
	[[#HDD Enclosure]]
		[[LifeOS#HDD Enclosure#Overview|Overview]]
		[[LifeOS#HDD Enclosure#Setup|Setup]]
	[[#Mobile Devices]]
		[[LifeOS#Mobile Devices#Overview|Overview]]
		[[LifeOS#Mobile Devices#Setup|Setup]]
	[[#Desktop Computer]]
		[[LifeOS#Desktop Computer#Overview|Overview]]
		[[LifeOS#Desktop Computer#Setup|Setup]]
	[[#Personal Server]]
		[[LifeOS#Personal Server#Overview|Overview]]
		[[LifeOS#Personal Server#Setup|Setup]]
[[#Beyond]]


***
## Introduction

### Overview
This project, deemed ‘LifeOS’, aims to provide an introduction to various system targeted at minimizing ones public digital footprint while maximizing functionality. That functionality includes replacing preexisting services and providing some ideas for further implementations that explore a future free of corporate data hoarding and commodification.

### Reason and "Qualifications"
Where did this project start? Passwords. However, passwords make up only a small portion of the overall framework. As I began to explore and utilize the World Wide Web I naturally started making accounts with various sites. Fairly early on I made the shift to a password manager. I believe it was 1Password at first. Eventually 1Password moved to a subscription model without any free options, or least not that offered the functionality I wanted. I migrated everything to LastPass, which eventually went a similar way, along with going through a serious data breach. Jumping ship again I found MyKi, which showed great promise as a free, highly featured, cross platform, password manager. Unfortunately MyKi was bought out by some other company and either moved to a subscription model, or was just deleted outright.

This left me with a text file full of passwords, and a strong desire to not keep them in that form for long. I went hunting again for “free open source password manager” and quickly came across KeePassXC, a piece of software meant for Linux systems that checks all the boxes, minus being cross platform to some degree, but that will be covered later. I imported my data and then needed a way to share the KeePass database across my devices. At first I was using standard cloud storage solutions, like GoogleDrive, iCloud, and OneDrive, but this still meant my data was on someone else’s hardware. While the database file is heavily encrypted, should one of those companies have a data breach or other incident, my vault file was right there on their hardware. So began my efforts to find ways to replace companies various services with private, self hosted, and encrypted alternatives.

What makes me particularly suited to present the overall system I have come up with? Honestly not much as far as technological knowledge goes, but I believe I am a fairly good teacher, and am good at converting technical jargon into language the majority of people can follow and understand. I firmly believe these tools more accessible to folks outside of the tech world and I aim to help bridge that gap and allow more people to be in control of their data. The system I will present can be adopted in parts, can be scaled for your uses, and can be shared with exactly the people you want. It most definitely takes a bit more effort to set up and maintain than some of the alternatives, but the resulting system is one I find incredibly robust in the face of more subscription models and data mongering companies.

### Goals
The goals of this project will be explored in a bit more detail in the next [[#Core Concepts]] section, but an overall looks will be presented here. At the most base level I wanted something secure. A way to get all the functionality I associate with the services Apple, Google, Microsoft, and others provide, without committing my data to someone else’s hardware, aka cloud, where it can be scraped and sold. That goal ends up having fairly complex implications as I explore the different systems I want to replace, but I have finally landed on a core set of software that tackles what I want.

***
## Core Concepts

### Private
Mine and mine alone, unless specified by me. This means I want my data to only ever exist on my hardware. That could be my phone or tablet, as well as desktop or laptop computers. Even when transferring data it should never sit on another person’s device unless I have included that device in my network of data sharing. This will make more sense when discussing [[#Syncthing]] later. On top of this, data should be encrypted whenever possible even when only going directly between my devices.

### Self Hosted
To be honest I’m not the most knowledgeable of the wide world of “self hosted” services, and the systems I discuss here might not truly qualify, but for my purposes they are self hosted. Meaning, one of my own devices is the source of the system or service’s core functionality. In some cases that functionality is decentralized across my devices and they are all contributing to the hosting and sharing of my data among themselves. I’m avoiding the phrase “roll your own”, which is often used in conjunction with “self hosted”. Most of the software used just takes running an installer to get working, rather than having to compile and tweak software to your specific needs and system, most of the software works “out of the box”.

### "Offline"
Very little works truly offline these days, but as many parts of this system as possible maintain functionality when not connected to The Internet, capital T, capital I. They still utilize protocols that would maybe qualify as “online” but can do so without ever exposing their traffic to the World Wide Web should they be configured to do so. This takes three primary forms. The first is just outright offline functionality. The software doesn’t depend on any sort of internet connection to function at it’s most base level. Secondly is LAN functionality. LAN, or Local Area Network, would be what you get if you power up a router but do not supply it with say an ethernet connection from your modem. The router still broadcasts a WiFi network, that network just doesn’t provide access to The Internet. Some of these tools, specified in their own sections, maintain functionality over LAN, meaning they don’t have to ever touch The Internet to function. Finally is encrypted tunneling. This references systems that still utilize The Internet and the connections it provides, but route all your traffic through encrypted pathways, therefor not exposing it, or at least not exposing any usable form of it, to would be bad actors.

### Scalable
I wanted the core functionality of this system to be deployable on any scale. From firing it up on your phone to setting up a personal server dedicated to hosting and running this system, this is meant to get as much functionality as accessibly as possible. If you already have a phone, most of this can be used. If you have a spare single board computer, like a RaspberryPi laying around then you can setup even more with that, and so on.

### As Free as Possible
A big reason I was motivated to figure all this out was to avoid subscriptions. Notice how I did not say paying in general. Good software is good, and good developers are rare, so I fully support BUYING good software. Not borrowing, not renting, not agreeing to have to buy it again when the next version comes out. Buying single, lifetime, licenses to software is something I fully support, but where possible free is better. I am fairly willing to purchase software when it checks all my boxes, but I know that is not the case for all people. I don’t believe there is a single part of this that REQUIRES paying, and where I prefer a paid product I will do my best to provide free alternatives. The biggest “feature” I worked to avoid was subscription models, as these mean you don’t really own the software at all, you are at the whims of the company that is clearly trying to siphon as much money as they can out of you.


***
***
## Software
This is where I get into detail on each of the pieces of software I use and consider part of this digital footprint framework. I would say there’s a few more that are part of my particular setup, but these comprise the core and cover most functionality that I got from often paid services from large data hungry corporations.

### Telegram
#### Overview
Telegram is an end to end encrypted messaging service. That means messages and other data you send are never broadcasted in a readable form to anyone that might intercept that data in transit. This makes it, and other similar services, favorites of protest organizers, cyber-sec enthusiasts, and generally anyone looking to communicate without big brother seeing. This does mean you need to tread a little lightly while using the app as it has understandably become a haven for hackers, scammers, and other nefarious individuals, but simply keeping your profile private and only adding users you have direct knowledge of has kept my experience very pleasant for years.

I personally picked Telegram because at the time of me adopting an encrypted messager it offered the best feature set. Telegram also boasts some potentially very attractive features including “unlimited” cloud storage. I know what you’re saying. “Aren’t we trying to avoid clouds?” My answer is yes, but the protections Telegram provides means I do use it for less sensitive storage and file transfers. For example: Let’s say I have a document I need to print and I am not at my computer. I can send that document to my Telegram saved messages, their interface for your cloud storage, and then go to a public library, sign into the web interface for the app, print my file, then sign out. Similarly Telegram is at the core of my note taking and link saving system. I have what is called a channel with myself as the only user and whenever I come across a link I want to save, I send it to this channel and can access it later on any device.

There’s a slew of other features, but those few alone have placed the app at the core of a lot of my day to day technology usage. Later we will discuss setting up a private cloud of whatever size your hardware allows, but if you want to simply stop here I think this app offers a lot of secure, cross platform functionality as is. The next evolution of this would be a peer to peer messaging app, but due to the nature of a system like that many of the other features would probably suffer. Basically for now Telegram is good enough, but I do have some small reservations with what data I entrust to the platform.

#### Install
Very easy, simply visit the [website](https://telegram.org/), click on your platform of choice and either be directed to the corresponding App Store, or get a download of the installer. Alternatively visit the [web interface](https://web.telegram.org/z/) to setup the app from say a public computer. The app needs only a phone number to setup and then you are good to go.

##### Recommended Apps
KJHGFKJBASJKBFDJKBSDKJBN

##### Alternatives
[Signal](https://signal.org/en/)
[WhatsApp](https://www.whatsapp.com/) (Owned by Meta/Facebook)


***
### KeePassXC
#### Overview
The solution to my password woes. KeePassXC is a wonderful piece of software. Totally free, totally open source, highly featured, and with some work, cross platform. There are browser extensions for auto fill, mobile apps and with a bit more work syncing of your encrypted database between any instance of the software. I use this software to generate passwords, save login data, and even store some notes containing sensitive information I want access to anywhere. I have it set to unlock with a master password on my desktop and the mobile app I happen to use makes me use my master password every 2 weeks, otherwise my vault is locked behind biometric authentication and a PIN.

As far as mobile apps go they all basically just are interfaces for reading the database file. I am an iOS user and have found the app Strongbox to do what I want, but it is a paid app. Strongbox has a subscription option, but also offers a single lifetime purchase. I valued the feature set of Strongbox enough for how often I use it that that purchase made sense. There is a truly free alternative provided below, but from what I can tell it doesn’t offer quite the same features. For Android I have provided what seems to be the standard app, and I will test it myself soon.


#### Install
For desktop operating systems install is quite easy. Visit the [website](https://keepassxc.org/), download the installer for your platform of choice and run it. On launching the application your will be prompted to either open a database or make a new one. Make a new one and start adding passwords.

For the iOS apps linked below setup is similar. Simply install, lunch, and make a database. Choose somewhere to save it and begin adding passwords.

Android I assume is similar, but I have not actually tested it yet.

Migration to this app can be a mixed bag. Coming from other password managers should be as simple as finding the export option in your previous manager, selecting export to CSV, and then slecting import from CSV in KeePass, but this is only doable in the desktop app. Make sure to delete the CSV file after import as it has all your passwords in plaintext within it. Migrating from iCloud passwords is worse, as there is no option to export your saved passwords, they must be manually copy pasted. While an absolute pain, I took that process as an opportunity to prune my saved passwords and run a bit of an audit on passwords I used across multiple sites, and removing accounts for websites and services I hadn’t used in years. Migrating from a browser’s password manager, like Chrome or Edge, follows similar steps as other password managers. Export your passwords and import into KeePass. Each users system is going to be slightly different so providing an explicit step by step is a challenge.

##### Recommended Apps
- iOS (App Store links)
	- [Strongbox](https://apps.apple.com/us/app/strongbox-password-manager/id897283731) (Paid)
		- [Website](https://strongboxsafe.com/)
	- [KeePassMini](https://apps.apple.com/us/app/keepassmini/id6446373282) (Free)
		- [GitHub Project](https://github.com/FrankHausmann/KeePassMini) 
- Android (Play Store links)
	- [Keepass2Android](https://play.google.com/store/apps/details?id=keepass2android.keepass2android&hl=en_US&gl=US) (Free)
		- [F-Droid mirror](https://f-droid.org/en/packages/com.android.keepass/) (To avoid using Google services)
		- [GitHub](https://github.com/PhilippC/keepass2android)

##### Alternatives
I have yet to find any piece of software that achieves what KeePassXC does.


***
### Syncthing
#### Overview
To put it plainly [Syncthing](https://syncthing.net/) is magic. Yes it takes some setup, and there’s definitely a learning curve, but once you have it running it does what it is designed to do so well. The main goal of Syncthing is to keep folders and files synchronized across devices. Sounds very simple. Sounds a lot like Google drive, or iCloud, and other servies. However, Syncthing has 3 major differences that set it apart. It is peer to peer, encrypted, and scalable. Oh, and it is totally free, so I guess that is 4.

The first is that it is peer to peer (P2P). This term was mentioned previously and it means that each device running the software acts as a host or server for that software. In other words there is no need to rely on a single centralized computer that is running the majority of the services functionality. Each device can essentially function on it’s own and act at the central server for any other device looking to connect to it, which can then each also function as a central server of their own and so on. This is often referred to as decentralized networking and is the same premise that torrent file sharing operates on.

How Syncthing puts this technology to use is quite simple. You fire up the software on 2 or more devices, select a folder from one to share with others, select where you want that folder’s contents to be saved on the other device, and then whenever a change happens on either device Syncthing initiates an update between devices using that P2P connection, meaning no data ever sits on a tech company’s servers like it would for Google Drive or iCloud.

The second big perk of Syncthing is that it it encrypted. Even though your data is never landing on someone else’s hardware it is still using internet protocols to connect devices. Due to this a bad actor could in theory snoop that data as it transfers, but Syncthing prevents this by encrypting data before it transfers and decrypting it once it has arrived at the destination device. Basically anyone,like your ISP or someone after your data, would just see gibberish as your data is transferred.

The final big perk relates to the “offline” and scalable concepts outlined earlier. Syncthing can work without a true internet connection. In fact by default Syncthing checks for the devices it is configured between on the local network first. For example I could power a small portable router off my car. That router would be broadcasting a WiFi network that wouldn’t provide access to The Internet. I could then connect my various devices to that ad hoc network and Syncthing would function. Later I will get into [[#Obsidian]] and propose a sort of new model for An Internet, not The Internet, that combines Syncthing and this local sharing concept.

#### Install
Actually getting the software on a device is fairly easy. For desktops simply visit the website and download the installer. For mobile platforms visit the links provided below. It is worth noting that the only available version for iOS is bundled and maintained by a 3rd party, not the Syncthing Foundation, but as the software is open source this is technically allowed. As such the full version costs a couple dollars for iOS, but again, good software is good, so I think it is very worth it. Otherwise all other versions of the software are totally free. Everything I use is linked below.

After installation setup can be a bit finicky. You start by adding devices to each other’s lists of connections. I like using my phone as a sort of hub for doing this, as you can view devices IDs as QR codes, allowing you to simply scan the screen of other devices to add them. There is also a setting once a device is added to make it an ‘Introducer’ so any devices it has a connection to get populated to other devices. Again I like having my phone with this enabled for all my other devices so whenever I add a new device to my network I only need to add it on my phone and the new device will show up everywhere else.

Sharing files is the next step. Unlike Google Drive and iCloud, Syncthing is not limited to a single folder that you have to structure all your shared files within. The whole point is to add folders from anywhere on a device and share to any location on another device. This gets a bit finicky with iOS, but works as intended in my experience thus far. Basically you press ‘add folder’ in Syncthing, select the folder you wish to share the contents of then select the devices from your network you want to share it with. On the receiving device you will see essentially an invite to the folder, simply specify a folder on that device you would like the contents to land in and Syncthing will start syncing those folders right away. I use this to share the folder holding my KeePass database across my devices allowing me to access my passwords from anywhere.

When first setting things up I approached Syncthing like I would Google Drive or iCloud. I made a single folder that I dumped everything I might want to share into and synced it to all my devices. However I quickly realized this was both inefficient and even problematic. Syncthing does a good job resolving file difference conflicts where they arise, but by compartmentalizing my sharing more I could avoid most of those conflicts while also only sharing the data relevant to each device with that device. In a later section I will provide a real world example of how I mesh all the systems outlined here together, and Syncthing sits at the core of that.

##### Recommended Apps
- iOS (App Store links)
	- [Mobius Sync](https://apps.apple.com/us/app/m%C3%B6bius-sync/id1539203216) (Paid to get unlimited shared folders)
- Android (Play Store links)
	- [Syncthing Fork](https://play.google.com/store/apps/details?id=com.github.catfriend1.syncthingandroid&hl=en_US&gl=US#) (Free)
		- [F-Droid mirror](https://f-droid.org/en/packages/com.github.catfriend1.syncthingandroid/) (To avoid using Google services)
		- [GitHub](https://github.com/Catfriend1/syncthing-android)

##### Alternatives
I have yet to find any piece of software that achieves what Syncthing does.


***
### PiHole
#### Overview
This is the first piece of software that is also, unfortunately, hardware dependent, and takes some more “intense” configuration. Especially when coupled with [[#Tailscale]], which will be discussed later, [PiHole](https://pi-hole.net/) is an effective way to clean up your browsing experience across any device on your home network and beyond.

A little background on how networking functions is necessary to grasp the power of PiHole. Whenever a device on a network tries to visit a webpage, say google.com, it needs to actually get a set of numbers, called an IP address, based on the more readable URL of the website. These number are stored in what are called DNS records. Most often your Internet Service Provider (ISP) keeps these records and when a device on your network attempts to visit a URL it checks with your provider to get the IP address and then can resolve the URL to said IP. Now let’s say you visit CNN’s website, one that is notorious for having lots of ads. When the webpages loads on your device each spot an ad will display makes a similar DNS check to go get that ad from the company providing it.

PiHole sits in the middle of this device-ISP interaction. It acts as a sinkhole for a set list of IPs and Domains so when your ISP attempts to resolve say an ad that a website you are loading is requesting, that request never makes it to your ISP and the ad never gets loaded. This serves as a network wide ad block, effectively turning the browsing experience of any device on the network a PiHole is configured on into a much cleaner and faster experience.

In order to function PiHole needs a device to run on. This is most often a RaspberryPi Single Board Computer (SBC), hence the name PiHole. There are plenty other ways it can be setup and configured, but the standard, easiest, and in my opinion most functional, is through a SBC of some sort. I am currently running PiHole on a RPi, but I plan to upgrade to a more powerful SBC so I can run other services on it without impacting performance much.

My biggest reason to recommend PiHole is that ad blocking on mobile platforms, particularly iOS, is very poor. For desktop browsers uBlock Origin will generally be good enough, but PiHole ads some other features with blocking data gathering and tracking services, and generally makes your home network experience much more pleasant.


#### Install
This is a tough one to really provide clear instructions for as individual setups can vary. The PiHole documentation generally does a great job, and the installer, once running, is very good. I do have a few recommendations. First is the operating system for whatever SBC you choose. I personally landed on [DietPi](https://dietpi.com/), a stripped down version of the default PiOS that still offers a desktop user interface if I want it. Long term I will probably shift to a headless OS, one that only provides a terminal interface, to make load on the SBC even lighter. Installation will require a bit of fiddling in a terminal and a little networking setup. I’ll provide a rundown on my particular setup, but everyone’s will probably look a little different.

- Flash micro-SD card with DietPi
	- There’s lots of software to do this, I personally use [Balena Etcher](https://www.balena.io/etcher)
- Insert micro-SD card into RPi
- Connect RPi micro-USB to USB port on back of router to supply power
- Connect ethernet cord from router to RPi
- Visit router configuration page (should be on a sticker on the back of your router)
- Look at connected devices to get IP address of RPi
- Open terminal and connect to RPi over SSH using default login found on DietPi website
- Change RPi login credentials (and save them to previously mentioned password manager)
- Run PiHole setup according to the [documentation](https://github.com/pi-hole/pi-hole/#one-step-automated-install)
- Configure router to use PiHole as the DNS resolver so all traffic goes through PiHole
	- NOTE: I like to set Cloudflare’s 1.1.1.1 as my backup DNS in case the PiHole goes down for some reason
- Start browsing, particularly on a mobile device, and see if ads load
	- NOTE: You can also visit the PiHole dashboard and see if it is successfully blocking requests


***
### VPN
#### Overview
This will likely be one of the shortest sections. VPNs are fairly straight forward. I’m sure plenty of people have seen their favorite YouTube face doing an ad read for a VPN service. The short version is that a VPN makes it look like all your internet traffic is coming from a device in some location other than your home network. A good VPN does not log any of this data or traffic, so in the event of say a government subpoena there is no record of the browsing that anyone using the VPN did. VPNs are a very effective way to maintain anonymity on the internet as well as get around region locks. Canadian Netflix is almost worth it on it’s own.

Some VPNs offer free plans, usually limited in speeds, or devices, or other ways, but this is another case of good software being good and worth the money. My VPN is one of the only subscription services I pay for. After some research I chose ProtonVPN for a few reasons, but I am considering making the jump to Mullvad and possibly their browser too. The main reason I have not swapped to Mullvad is that in an incredibly noble effort to maintain as much customer anonymity as possible, their payment options are a bit fringe, but this just speaks to their commitment to not storing any of your data. Mullvad also has some very good articles on privacy in general that I recommend reading.


#### Install
Pick your VPN of choice, and to be honest, most of the ones you see ads for are distinctly passable. There’s better options out there, but just picking something is a good first step. Visit the website, download the installer and start the app up. For mobile devices download from your App Store or manager of choice and start the app. For iOS you will need to do some additional step to allow the app to configure your VPN connection, but the apps walk you through this pretty well.

##### Recommended Apps
- iOS (App Store links)
	- [Proton VPN](https://apps.apple.com/us/app/proton-vpn-fast-secure/id1437005085) (Paid auto renewing)
		- [Website](https://protonvpn.com/)
		- [GitHub](https://github.com/ProtonVPN/ios-mac-app)
	- [Mullvad VPN](https://apps.apple.com/us/app/mullvad-vpn/id1488466513) (Paid manual renewing)
		- [Website](https://mullvad.net/en)
		- [GitHub](https://github.com/mullvad/mullvadvpn-app)
- Android (Play Store links)
	- [Proton VPN](https://play.google.com/store/apps/details?id=ch.protonvpn.android&hl=en_US&gl=US) (Paid auto renewing)
		- [Website](https://protonvpn.com/)
		- [GitHub](https://github.com/ProtonVPN/android-app)
	- [Mullvad VPN](https://play.google.com/store/apps/details?id=net.mullvad.mullvadvpn&hl=en_US&gl=US) (Paid manual renewing)
		- [F-Droid mirror](https://f-droid.org/en/packages/net.mullvad.mullvadvpn/) (To avoid using Google services)
		- [Website](https://mullvad.net/en)
		- [GitHub](https://github.com/mullvad/mullvadvpn-app)

##### Alternatives
As mentioned, there are lots of options for VPNs. The two suggested here have good track records and work well. I’ve tried a few others and didn’t find them worth suggesting. They aren’t outright bad, but these are the two I have my eye on nowadays.


***
### Tailscale
#### Overview
This is where things start to get a bit more convoluted and more optional. [Tailscale](https://tailscale.com/), to some degree, isn’t that different from a VPN, but instead of devices provided to you by a company that your device can assume the location of, Tailscale has only the devices you add to your network. On top of that this isn’t meant for location spoofing, it is for securely providing connections between your devices without ever revealing your traffic to other user. Basically Tailscale allows you to easily connect devices wither services you would normally access via LAN or that you don’t want to reveal to WAN connections.

To put it in other words, let’s say I’m running a Minecraft server on a computer at my house. Opening up the necessary connections to play on that server from anywhere would compromise portions of my home network. Tailscale would give me a separate IP address that can only be used by devices I have added to my Tailscale network, and would allow me to connect to the Minecraft server. Now replace the Minecraft server with any service, for instance the PiHole I have running on my home network. With a little bit more configuration this provides any device I have connected to my Tailscale network with the ad blocking power of the PiHole.

That same thing would go for any service. I can set up Syncthing to go through Tailscale, even though that is largely unnecessary with the security Syncthing already has. The way I plan to use Tailscale is to setup my own private Netflix. There is software that is designed to stream media stored on devices connected to you home network to other devices, and by connecting those services to Tailscale I can then steam that same content even when I am not on my home network. An additional feature of Tailscale is inviting others to your network and managing their permissions. This would allow me to open the device hosting media to other users, allowing them to stream the media as well.

Other uses worth noting are Remote Desktop from mobile devices and remote SSH connections without exposing parts of my home network to the World Wide Web.


#### Install
Tailscale is somewhat system dependent. It can be installed on Mac, Windows, Linux, and mobile operating systems. Generally it’s as easy as installing on your platforms of choice, logging in with your account, and you’re pretty much good to go. For mobile platform you’ll need to follow some prompts to get Tailscale working in place of a VPN, which means you cannot run Tailscale and a standard VPN at the same time. Generally I would suggest simply visiting the [website](https://tailscale.com/) and follow the get started guide. Tailscale has paid plans, but these are more geared towards enterprise customers, the experience for single users is perfectly functional.


***
### Obsidian
#### Overview
We are in the realm of very optional parts of this whole system, but still worth noting as this section begins to show how all these systems paint a picture of an overall digital footprint that puts the user in control of their data. [Obsidian](https://obsidian.md/) has quickly taken over my note taking, information storing, link saving, and general data organization. At it’s core Obsidian is a note taking app. It uses a formatting language called Markdown that provides simple “commands” to organize text within a file. This is a case of simple rules powerful implications. Your obsidian notes are organized in folders and files and the interface provides very powerful ways of sorting, searching, tagging, and linking notes together.

As I have used Obsidian more and more I have started to think of it as my own personal internet. A collection of pages linked together that is searchable, and navigable via those links and searches. I use this internet to store and track many aspects of my life, ranging from reviews and notes of books I have read to lists of products I intend to buy when I can get around to it. It has to some degree revolutionized how I sort and manage my interests to allow me to find connections between them, establish overarching concepts, and visualize how any data I choose to store is interrelated.

The phrase “data I choose to store” is where Obsidian begins to mesh into the rest of this system. With Obsidian and Syncthing I could meet someone and let them browse my Obsidian vault, maybe they find a file or whole folder they like the contents of and want to include it in their personal Obsidian vault as well. We both fire up Syncthing, share info, select the folders we want to swap and move on. From there 2 possible options exist. We remove each other’s devices from Syncthing, keeping our personal lists clean, and our shared files diverge, allowing new unique evolutions of that data to form. The other option would be we keep our files synced in order to receive updates from each other’s respective vaults and continue to see changes over time. We could then pass folders we copied from someone else to other users, effectively creating a decentralized internet of data each individual curates for themselves. Each user can choose exactly the data they carry with them and therefore are capable of passing on to others.


#### Install
Obsidian is another easy one. Visit the website, download the installer and go. It is on every App Store and works right out of the box. I do encourage users to browse the community plugins for some additional functionality tailored to your needs. Obsidian does offer a paid service to keep your vault synced across devices, but we now have Syncthing on our side. So by selecting your Obsidian vault as a synced folder you can easily share our vault to your other devices.

***
***
## Hardware
While software solutions can take you very far towards a private and functional digital life, there is a point where hardware begins to have a drastic impact. That being said if you want to avoid the financial impact and labor incorporating hardware will entail, by all means, stop reading now and enjoy the software solutions outlined above.

### Networking Devices
#### Overview
To some degree fairly simple, but there is still a lot of room for customization. These can range from the router that your ISP rented to you, or full scale rack mounted enterprise solutions. Personally I am in fact using the router Verizon supplied me. I don’t love it, and I plan on swapping it out, but by supplementing it with some of the hardware outlined below I’m happy enough with my current system.

This document is not meant to be a detailed rundown on home networking, but I have done a bit of research on the matter and have some suggestions.

#### Setup
Router configuration pages are very, shall we say…diverse. Navigating them can range from a joy to total nightmare. Often times the config pages of routers provided by an ISP are designed to hide the more “advanced” settings, which translates into making it harder to configure the more privacy focused settings. Even so with enough googling most routers can be configured to most situations, my clunky Verizon one included. 

Some of my first steps when getting a new router are listed here.
- Power on
- Plug into modem via ethernet/coax/fiber etc.
- Connect a computer to the router through ethernet or WiFi using the default credentials on the back of the router
- Check the back for the config page URL and enter it in a browser
- Change my network name and password
- Enable advanced settings
- Change DNS to 1.1.1.1 or a PiHole’s IP if using one

Much beyond that is honestly a tad out of my comfort zone or at the very least my “expertise”. I rely a lot on the existing work of others, as so much of home networking solutions have been covered in depth by other folks on The Internet.

### SBC and Linux
#### Overview
I’m not going to provide a full rundown on the wide world on Linux, or even single board computers, but the two coupled together are incredibly useful and deserve some coverage. As mentioned in the [[#PiHole]] sections a single board computer is a small piece of hardware, usually able to fit in you hand, that is capable of running a “full blown” operating system. This give it the ability to interact with other devices, networks, displays and more. With all that connectivity a SBC can be used for many things. PiHoles are a perfect example, so are web servers to say host your own website, or a personal VPN like Tailscale. The options are vast, and having one of these small computers connected to your home network can make for fun and functional hacking.

#### Setup
Select a SBC and plug it in. Okay, it’s not quite that simple, but almost. As mentioned in the [[#PiHole]] section you will need to get an SD card with an operating system on it. These can actually be purchased preinstalled with PiOS when buying a Raspberry Pi, or you can flash your own as mentioned above. For a slightly cleaner mess of wires I have elected to power my RPi off my router and mount it to the outside of my router’s enclosure. Software wise I have PiHole and Tailscale currently running and plan to add Syncthing once I connect external storage to the RPi, which will be covered in the next section.

### HDD Enclosure
#### Overview
This is simply referring to products that provide connectivity for higher capacity hard drives without having to build them into a whole computer. The potential use cases here are wide, but almost all worth it. From setting up backups of your devices, so self hosting file share solutions, having the ability to store files en masse is incredibly helpful. These products come in many shapes and sizes, from all metal construction to bare PCBs, single slot to more than 8. These devices can be plugged into computers, some mobile devices, and even network devices to provide them with additional storage space.

#### Setup
These are largely plug and play. Buy an enclosure and hard drive to populate it. Slot the drive into the enclosure and power the enclosure. Connect it to a device. A laptop or desktop computer would probably make setup the easiest as drives might need to be formatted. Some systems will do this automatically upon plugging the drives in, but I’d it’s inconsistent. Personally I will eventually be adding drives to the RPi connected to my router to add storage options to my network and through all the other systems outlined here be able to access it from any of my devices.

### Mobile Devices
#### Overview
This section has the potential to be the longest by far. Mobile devices are probably the most diverse collection of hardware out there.To some degree it comes down to two categories, iOS and Android, but actual hardware wise there is incredible diversity. If we are talking from a privacy perspective almost no stock phones really pass the bar. Apple supposedly promises high degrees of security, but with their operating system being closed source there is really no way to know. Android, while based on Linux which is open source, often comes customized and preinstalled with all sorts of things on flagship phones, meaning it’s hard to say just how private they actually are. 

#### Setup


### Desktop Computer
#### Overview

#### Setup


### Personal Server
#### Overview

#### Setup




***
## Beyond
### Welcome to The Intra-Net





***
## Word Spew
- Personal os
- Carry your digital footprint
- Connect/merge with others
- Broadcast exactly the portion you want
- Choose how much of the “bionet” (working title) you want to carry
- Portions can be kept updated via “internet” or LAN
	- This traffic is still very secure
- Same protocols work on any scale
	- Phones
	- Home networks
	- Portable routers
- 
