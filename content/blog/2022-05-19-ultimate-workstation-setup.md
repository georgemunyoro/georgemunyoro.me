---
title: "Ultimate Workstation Setup"
date: 2022-05-19T18:05:07+02:00
draft: false
---
**Why I run 3 operating systems at the same time**

This is a tale of how I, the best programmer ever, built the greatest computing experience know to mankind. Please contact me to organise the delivery of my Nobel prize.

**ssh, that’s a little iCloud**

If you’re familiar with South Africa’s power provider Eskom, you’ll know they’re about as reliable as a stock iPhone charger after 12-15 months, it works at that one angle but if you so much as breathe wrong the power goes out, so I needed something fairly powerful and efficient that I could work on during these outages, with the most important factor being battery life. It was not an agonising decision. At the time I found no Windows laptops in the same price range that could match the MacBook’s performance while also being extremely portable, quiet, or cool. When it came to battery life Apple was just in a league of their own, there was nothing to compare to, and having eyed the impressive battery life on the M1 computer, I found myself unwilling to compromise. So I went to the local iStore, and financially ruined myself.

Now that I have the MacBook, it plays a major role as the main computer for anything work related. I keep local builds, repos, databases, and configs on my laptop. Since I use vim as my main editor, I can ssh into my laptop from my desktop PC and run things this way, with the necessary ports forwarded on my router so I can access everything on localhost.

Setting it up this way affords me a bunch of advantages:
- When the power goes out, I can just continue on my laptop as though nothing happened
- Enables me to safely experiment with my Linux and Windows machines without worrying about losing my work
- I’ve found MacOS to be the most stable operating system of all 3**
- The M1 processor is crazy fast, and awesome for programming workloads

**While linux in general is obviously more stable than MacOS, I run Arch, and I don’t have any safeguards in place because that’s why I run Arch, I value the ability to be dangerous  

**Linux is the window to my heart**

This Is the really fun part, where I run multiple operating systems on the same system. You might think this is incredibly complex to set up, but in recent times the technology that enables you to do this has come a long way, it’s way easier than you think.

Instead of running a full heavy desktop operating system like Windows or MacOS on my PC, I run Proxmox, a hypervisor OS made for running virtual machines. It’s extremely lightweight and efficient, allowing me to take full advantage of my hardware resources without giving up too much to run the VMs themselves. To understand how my desktop system works, you need to know a little bit about the hardware:

- CPU: i5 11400F (F means this CPU is incapable of video output, a dedicated GPU is required)
- GPU(s): - NVIDIA RTX 3080 10GB
- AMD HD7950 3GB
-   RAM: 2 * 16GB = 32GB DDR4 4000MHz
-   Storage: 2 * 2TB HDDs + 2 * 120GB SSDs

Those two graphics cards are what make this setup possible (and so very cool). The VMs running in Proxmox are no ordinary VMs. Using a cool piece of VM tech called KVM, I can make use of an awesome feature called PCI passthrough to give full unfettered control of each GPU to each of the two VMs.

But… why?

You know how every time you’ve tried running a VM in VirtualBox on your computer it’s always been laggy and choppy? That’s why. By giving the VM a whole GPU to do whatever with, I don’t need to deal with crappy hardware acceleration performance because now the VM is being accelerated by actual hardware, and the guest OSs don’t have to battle for resources with the host OS.

I’ve passed through the most powerful GPU to the Windows VM and connected it to the right-most monitor of my triple monitor setup. Using barrier, a virtual KVM software, I can use the same mouse and keyboard on both VMs and the laptop at the same time, so I can move my mouse into my Windows install from the 2 left Linux monitors like it’s just another monitor on the side, and Barrier switches control to Windows.

My current Windows install is incredibly dumb, and that’s by design. Dumb in the sense that it’s not really a power user install, but rather a glorified xbox. When working, I use it to control my Spotify and I open a second browser window there so I can look at documentation and whatnot while I work. When I’m done working, I make use of my game pass subscription to kill time and have some fun. My headphones use a 2.4GHz wireless dongle, so they have really good range. I keep the dongle passed through to Windows, so I can listen to my Spotify/Tidal on there and control Spotify from my laptop while in the next room. I also have parsec installed so I can play my Windows games from anywhere around the house on my phone or laptop. It also comes in super handy when I’m out and about and need access to my home system. I prefer it over opening up my local network to the internet.

My Linux setup is my opinion  very simple, but gets out of my way and is super powerful. I use a tiling window manager called bspwm, this allows me to control how windows are displayed and positioned with incredible precision using only my keyboard (again, I’m a vim user).

-   My terminal of choice is Alacritty, a cross-platform GPU accelerated terminal. I actually use it on all 3 environments, not just Linux.
-   sxhkd for managing and configuring system-wide keybindings.
-   Picom as my compositor
-   rofi as my menu and application runner
-   yay is my AUR helper
-   Neovim is my editor of choice across the board
-   zathura for reading pdfs and other documents
-   vlc is my media player  
    
There’s a ton of other software running on my Linux machine, but it’s small minute stuff that isn’t really relevant to this article, maybe another time.

I run Linux for both work and play. It’s my primary work environment on my desktop machine, and my main environment for working on lower level personal projects using C/C++ as I am more familiar with the LVM backend on x86 intel processors as opposed to Apple’s ARM based M1 SOC and it’s quirks.

I’ve found compatibility to be the greatest comfort and advantage afforded to me by my almighty setup. I don’t need to ask a friend who has a Mac for something or spend hours searching for an alternative to some random software because it doesn’t target my OS of choice. My setup embodies my desire to not have to chose, to have everything, because I can.


```text
There was once a programmer who was attached to the court of the warlord of Wu.

The warlord asked the programmer: "Which is easier to design: an accounting package
or an operating system?"

"An operating system," replied the programmer.

The warlord uttered an exclamation of disbelief. "Surely an accounting package
is trivial next to the complexity of an operating system," he said.

"Not so," said the programmer,
"When designing an accounting package, the programmer operates as a mediator
between people having different ideas: how it must operate, how its reports
must appear, and how it must conform to the tax laws. By contrast, an operating
system is not limited by outside appearances. When designing an operating system,
the programmer seeks the simplest harmony between machine and ideas. This is
why an operating system is easier to design."

The warlord of Wu nodded and smiled. "That is all good and well, but which is easier
to debug?"

The programmer made no reply.
```
