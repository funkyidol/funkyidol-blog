---
title: "Dual booting Ubuntu Budgie on Windows laptop"
date: 2019-07-10
summary: "My thoughts on the process of installing Ubuntu Budgie in parallel to Windows 10 on a Dell Inspiron 1..."
draft: false
tags: ["linux", "ubuntu"]
canonicalURL: "https://dev.to/funkyidol/dual-boosting-ubuntu-budgie-on-windows-laptop-4a55"
---
My thoughts on the process of installing Ubuntu Budgie in parallel to Windows 10 on a Dell Inspiron 15 7000 series laptop.

Preconfigured Dell windows machine don't make it easy for you to dual boot Linux. I really had to mess around in BIOS to make it work.

Steps that I followed:
1. Disable secure boot.
2. Change boot order
3. Change SSD config from RAID to AHCI (https://www.youtube.com/watch?v=9ngnIKqPOc4)

All of this creates a lot of friction and had to Google around a lot to get to this point which is not really idle for new users and experienced people alike.

My inbuilt nVidia GPU gave me a very hard time with the whole install process. My machine went blank everytime I logged into Linux. I initially couldn't understand what was happening & reinstalled Linux multiple times just to make sure the installation was fine.

Again after a lot of googling I figured out that its a nVidia driver issue so I had to
1. Go to command-line before login
2. Setup my wifi from CLI
3. Add the repo for drivers, Install & configure the drivers from CLI
And all this on a 4k display without font scaling, so literally reading ants there.

And this whole situation can only be fixed if distros ignore nVidia hardware unless drivers are installed bcoz Distros can't bundle the proprietary drivers due to licensing issues.

After successfully installed and working, few things I'm missing from windows in Ubuntu Budgie
1. Factional display scaling. It's either 100% or 200%. Nothing in between
2. Native apps for Notion, Google Drive backup & sync. 
But this list used to a lot longer 4-5 yrs ago so thats a very good sign of how much the ecosystem has evolved over the years.

All this is just the initial thoughts. They will evolve I'm sure. Overall things are fine. What my expectation out of this move is a secure & a dev friendly work environment and better compilation speeds. I'm still not holding my breath for improved battery life though.

Edit:
Received some help from my twitter friends which shared the following links to help out with some of the issues
https://www.omgubuntu.co.uk/2019/06/enable-fractional-scaling-ubuntu-19-04
https://www.omgubuntu.co.uk/2019/02/odrive-google-drive-linux-client
https://www.omgubuntu.co.uk/2019/05/slimbook-battery-optimizer-ubuntu

A helpful link I found: https://medium.com/@pwaterz/how-to-dual-boot-windows-10-and-ubuntu-18-04-on-the-15-inch-dell-xps-9570-with-nvidia-1050ti-gpu-4b9a2901493d
