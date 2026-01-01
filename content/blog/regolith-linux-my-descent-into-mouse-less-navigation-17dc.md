---
title: "Regolith Linux - My descent into Mouse-less navigation"
date: 2020-04-20
summary: "What got me interested?   I like to keep things simple and stick to the defaults as much as..."
draft: false
tags: ["linux", "gnome", "i3wm", "ubuntu"]
canonicalURL: "https://dev.to/funkyidol/regolith-linux-my-descent-into-mouse-less-navigation-17dc"
---
## What got me interested?

I like to keep things simple and stick to the defaults as much as possible (as much as I would love to customize the hell out of things, sadly I don't have that kind of time nowadays) and after distro-hopping for a while, I was happy to use stock Ubuntu. 

I stuck to the non-LTS release starting from 19.04 and then upgraded to 19.10, but all this while one thing that bothered me a lot was the amount of RAM being consumed by the Gnome Window Manager. It's always fine after a fresh start or reboot at the beginning of the day with around 500-600 MB of usage but by sunset, my usage generally climbs upwards of 1.1 GB. On a 16 GB that's a huge amount especially when my Android IDE, Emulator, Browser and 5 other things are all fighting each other for the already vanishing sweet piece of RAM pie. And also there is this nagging feeling as a developer that there has to be some sort of a memory leak somewhere, because of which this process keeps increasing in size every few hours. At one point I was considering buying more RAM for my laptop just because this was becoming a daily nuisance for me.

I then started to look for a lightweight Window Managers (WM's) to replace Gnome with something more stable and easy on the memory. There are a lot of excellent options like XFCE and some others, but all of them seemed very outdated in terms of their underlying technology for 2020 (though being more stable at the same time, from what people shared on forums). 

A good friend of mine (and a huge Linux advocate) had suggested me to try out i3wm (a Tiling WM - more on that later) some time back and I quickly dismissed that option at that time because I wasn't convinced about having a keyboard-driven WM. But this time around I gave it a more serious look as I was pretty pissed at Gnome and couldn't wait for the Ubuntu 20.04 update to land.

## And I discovered Regolith Linux

While giving i3wm a more dedicated research time I found [Regolith Linux](https://regolith-linux.org/), which instead of creating a new DE (Desktop Environment) chose to create a collection of open source components bundled in a way to make transition and usage of i3wm easier. Looking at there [Github Page](https://github.com/regolith-linux/regolith-desktop), its just a meta package which just holds the issue tracker and release files. It very thoughtfully combines various independent components like i3-gaps WM, Rofi application launcher and notification system, i3bar etc. to create an easy to adopt package, which otherwise takes a lot of time to setup when starting with i3wm. 

### Tiling Window Manager ###

All this combined makes up for a fairly easy to use [***Tiling Window Manager***](https://en.wikipedia.org/wiki/Tiling_window_manager). A Tiling WM is a very unconventional kind of a WM where multiple applications or windows when opened together do not float or overlap each other. They only open beside each other, oriented either vertically or horizontally. No more floating windows, no hidden windows behind one another, no need for a mouse to move windows around. Everything is laid out like Tetris tiles alongside each other. And what do you do when you have too many things open at the same time or you want one of the windows to be full screen, you simply move it to a different 'workspace'. In the following sections, I will talk in more detail about how to get more comfortable with this fundamental shift in the way we use our desktop environment all the while using **just the keyboard**.

## Installation

Regolith is [available](https://regolith-linux.org/download/) as both a pre-bundled ISO and a standalone installable PPA. I chose to install it over my current setup as a PPA. 

Use the following commands to install Regolith via PPA.

```shell
$ sudo add-apt-repository ppa:regolith-linux/release
$ sudo apt install regolith-desktop
```

And once installed, restart and Regolith will appear as a desktop session on the login screen.

![](https://regolith-linux.org/regolith-screenshot-login.png)

When you login, you are welcome to this screen with the quick list of keyboard shortcuts to help you start your journey on adopting Regolith. This helper overlay is what makes it so easy to start using the i3wm.

![](https://regolith-linux.org/screenshot-remontoire.png)

## Getting Familiar

`Super` key is your best friend in this desktop environment. Everything that you wish to do all starts with the `Super` key. To show or hide this keymap overlay just press `Super + Shift + ?`
To launch an application, just press `Super + Space` to start the launcher app

I won't list all the keyboard shortcuts here which are readily available in the help menu. Rather I would talk about some common usage patterns and how to quickly get into the habit of using those patterns.

But before that, let's get a little more familiar with the environment itself.

### Workspaces

On the bottom left is our workspace indicators. The workspaces are how we spread our windows around in this system instead of stacking them over each other. You start with only one workspace when you login but as you move windows around to the workspaces, they become active. The workspaces might be numbered but it's not required to use them in sequential order. You can use whichever workspaces at any given point as per your comfort. The highlighted workspace indicator will tell you which workspace is currently active.

### App Launcher

Regolith bundles the 'Rofi Application Launcher' which is a type-to-search type of a launcher. Just start typing what you are looking for and it will immediately filter results based on the text. And as you use this launcher more and more it starts remembering your choices and starts showing them on first like in the image below 

![Alt Text](/blog/regolith-linux-my-descent-into-mouse-less-navigation-17dc/xsrktufqm5w32ms7ppt2.png)

> One thing to remember here is that 'restart' is actually 'reboot' here so it might be something to look for when starting out.

### Notifications

Notifications is probably the most not-so-obvious feature in Regolith. Regolith bundles with the [Rofication Notification System](https://regolith-linux.org/docs/interface/notifications/) which takes a very bold decision of never showing an alert for your notifications, making the setup distraction-free. All new notifications received go on to incrementing a counter near the bottom right of the i3bar. There is still a notification sound but no visible UI alerts. To see the notification you press `Super + n` to open a rofi window showing all  the notifications. This is something I like a lot since it helps alleviate visual distractions while I'm doing deep work.

Now the other big thing with these notifications is that they are non-actionable. You cannot click or select this notification to open the respective app which furnished the notification. For me, this needed getting used to as with the traditional notifications system we are in the habit of taking actions directly on the notification to open the respective application. But on a personal level, I am fine with it since most of the notification I receive are from Slack or Android Studio. 
To delete these notifications simply press `Delete` to remove individual notifications or `Shift + Delete` to delete all notifications from a particular app.

![Alt Text](/blog/regolith-linux-my-descent-into-mouse-less-navigation-17dc/0bur9hlikf0h0d9hd2b8.png)

### Traditional Gnome Settings

One good thing about Regolith, which is not available in the standard i3wm setup is the availability of the traditional gnome settings manager to allow you easy access to system settings without the need of relearning anything here. Its implemented as normal floating windows easy to interact with using a mouse.

### Navigation  and Usage Patterns

* **Working with non-tillable windows**
    There are a few applications which work well in the tiling paradigm and can lead to some weird window placements and artifacts. This happens for me notably with the Android Emulator.
![Alt Text](/blog/regolith-linux-my-descent-into-mouse-less-navigation-17dc/a874rgeq91btz0mhoymy.png)
    Luckily we do have an option to make any window a floating window. Pressing `Super + Shift + F` on the currently selected window makes if a floating one which then overlaps the rest of the environment.
![Alt Text](/blog/regolith-linux-my-descent-into-mouse-less-navigation-17dc/2qcx29ltnw3dc7d6l0k2.png)
    But we can't simply move this window around with the mouse. Here once again we have to take help from our friend the `Super` key and keep it pressed to enable window dragging behavior while you move the window around using the mouse.

* **Setting up a workflow**
    The AHA moment truly came to me when I created a workflow for myself and realized how easy it is to do pretty much everything with just the keyboard. To start setting up a workflow first we have to understand that all the applications that we will be using will live on separate workspaces. So basically you have to plan your workspaces depending on the **priority and frequency** of the apps which are in play. 
    For me the browser is the go-to app, so Firefox lives in the Workspace-1. Next is Android Studio which goes in Workspace-3 and next Slack which goes in Workspace-5. I chose Workspace-3&5 because that way my most important apps are all on odd workspace numbers. On Workspace-2, I have my Notion app and Gitlab app in vertical split mode. All music players go on Workspace-4 and anything extra goes in Workspace-6. I have had to rarely use more than 6 workspaces at a given time. In the customization section, I will talk about how to automatically move windows to these workspaces at launch.

* **Working parallelly in multiple apps**

    As I mentioned earlier, in this tiling desktop environment, apps open along with each other. 
![Alt Text](/blog/regolith-linux-my-descent-into-mouse-less-navigation-17dc/7mixho0vpbia8jpu93sw.png)
When more than one app are open, they always show up dividing the currently available space in half either vertically or horizontally. By default, the apps always open split vertically side-by-side. 
![Alt Text](/blog/regolith-linux-my-descent-into-mouse-less-navigation-17dc/gi2r9clrctfkfb0pz9g4.png)
So the first window shows of full screen, second split it in half, the third app will split the screen in one-thirds and so on. 
![Alt Text](/blog/regolith-linux-my-descent-into-mouse-less-navigation-17dc/qfxg6emoan9mw23af9bw.png)
    But instead, if I wish to open the third app split in the lower half of the right side split horizontally, I will just press the orientation modifier i.e. `Super + Backspace` before opening the third app. And not when I open the third app its shown like in the image below.
![Alt Text](/blog/regolith-linux-my-descent-into-mouse-less-navigation-17dc/7s8evy2in8a8qyu1q69g.png)
    The power of Regolith shines especially when you have multiple apps open in the same workspace aligned in the grid pattern of your choice. To move focus between the various windows, instead of moving the mouse, you can very quickly press `Super + <arrow keys>` to focus on the app depending on the window layout. 

* **Moving windows between workspaces**
    This point is more about adopting a new habit more than anything else. To move the currently selected window to a different workspace we press `Super + Shift + <workspace number>`. This moves the current window to the desired workspace while keeping you on the workspace you were on. So if I wanted to move my terminal window from Workspace-1 to 2 but while remaining on Workspace-1 then I press `Super + Shift + 2`. But If I want to 'take' the terminal window 'with me' to Workspace-2 then I press `Super + Alt +2`, This moves the terminal window to Workspace-2 and also makes it the active workspace.

* **Resizing windows**
    One behavior I was not expecting to be this easy to do without a mouse was resizing windows. Pressing `Super + r` starts the window edit mode where pressing 'left' or 'right' resizes the split of horizontal windows and 'up' or 'down' resizes the split for vertical windows. You can also press '+' or '-' to increase or decrease margin between the windows. With a contrasting wallpaper, it looks pretty cool. Press `Esc` or `Super + r` again to exit the edit mode.

## Customization

Though I was pretty happy with the default configuration that Regolith provides for i3, there were a few things I still wanted to change to help make things easier.

But before starting any customization we first have to setup the i3 config file to modify it. Best way to do so is to  follow the steps in [this link](https://regolith-linux.org/docs/howto/stage-configs/)

* **Auto open apps in specific workspaces**
    After you have staged the i3 config files in the path `/home/<user>/.config/regolith/i3` modify the config file and append the following in the end.

    ```python
    for_window [class="Slack"] move to workspace $ws5
    for_window [class="jetbrains-studio"] move to workspace $ws3
    for_window [class="ICE-SSB-notion"] move to workspace $ws2
    for_window [class="ICE-SSB-gitlab"] move to workspace $ws2
    for_window [class="Rhythmbox"] move to workspace $ws4
    ```

    The above code will always move my Slack window to Workspace-5, Android Studio to Workspace-3 and so on. 
    *Hot Tip:* If you want to find the name of the window to be included in the above code, just open a terminal and type `xprop` and then click with your mouse on the desired window. It will print a lot of window-related internal details in the terminal and you can pick up the window name from there.

* **Show RAM usage in bottom bar**
    By default the bottom i3 bar shows everything except the RAM usage which is still super awesome because most desktop environments don't show resource usage by default and you have to go hunting for an extension or app to do so. So to enable the RAM usage indicator, go to `/home/<user>/.config/regolith/i3xrocks` and open the config file and uncomment the following lines 

    ```python
    [memory]
    interval=10
    ```

    Now just type `regolith-look refresh` in the terminal to show the small pie chart of the total RAM with the available RAM amount.

* **Add a "Clipboard Manager"**
    This was the **most** tricky thing to get working in Regolith. As a daily user of Gpaste, clipboard manager is part of my regular flow of working when copy-pasting code from Stack Overflow on to my project and because there is no default support for traditional pop-up window systems, Gpaste didn't work. After a lot of Googling and hit and trials, I landed on [Greenclip](https://github.com/erebe/greenclip). This a rofi based clipboard manager which integrates which shows the previous selections similarly to how the notifications are shown.

    To install, just download the executable from the github page and add the following file to the Regolith config file

    ```python
    # Greenclip
    set $greenclip /path/to/file/greenclip
    bindsym $mod+Shift+v exec rofi -modi "clipboard:$greenclip print" -show clipboard
    exec --no-startup-id $greenclip daemon
    ```

    You can check out the video linked in the Greenclip Github page readme for detailed step by step instructions.

## Not everything is perfect

Frankly, I don't have much to write in this section apart from the fact that using Regolith definitely had its own learning curve but not as much as a vanilla i3wm setup would be. It's obviously about what clicks for whom and putting in just the little bit of effort to becoming more productive and feel like a "Hacker Man". 
![](/blog/regolith-linux-my-descent-into-mouse-less-navigation-17dc/giphy.gif)
Though I'm still learning the ropes of using more keyboard shortcuts to get a better window layout, but all that I feel will come with time as its need would move up from good-to-have to must-have

## Future

Though I'm super happy with my setup right now, I find the [Pop Shell](https://www.omgubuntu.co.uk/2020/03/pop-shell-wants-to-bring-proper-tiling-window-features-to-gnome-shell) extension from System76 to be really interesting. This extension will bring the goodness of tiling WM to the standard Gnome setup which will make it further easier to use for first time adopters. But I still can't shake the feeling that using Gnome will still be a lot more resource hungry compared to the minimalistic i3wm via Regolith. None the less I'm also looking forward to the new developments and releases of Regolith Linux and if possible consider a donation to the developers.
