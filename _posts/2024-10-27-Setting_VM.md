---
layout: post
title: "Setting Up a VM Without Built-In Support"
feature_image: /assets/images/posts/2024-10-27-Setting_VM/post_title.png
categories: misc
---

I’ve been knocking my head over microprocessors and IoT lately for a school project. This project involves a DHT11 temperature and humidity sensor using an ESP32 board. In order to install the IDE to actually develop the code that will show the outputs on a web server I have to be working on a linux environment - I like windows for other reasons not related to programming, and I’m looking for alternatives that do not include dual-booting my machine. First thing that came to mind was WSL and VM’s. The first option is great but I wanted a more encapsulated environment, something that I could play with and mess around a little bit. Like an isolated environment where I could respond quickly to any changes and requirements my projects could present. VM’s were, then, the best option.

What are VM’s (virtual machines)? They’re simply a compute resource that uses software to run other OS and programs. For example: let’s say you have Windows as your host OS but you want to give it a try with Linux, what would you do? I would say you have three options: wipe your current OS and install a Linux distro, dual-boot your machine so it has two OS installed under the same hardware, or you could use a VM and install your desired Linux distro. The history of Virtual Machines dates to the late 60’s, when IBM invested a lot of time and effort in developing robust time-sharing solutions. We are talking about a time where computers were huge and expensive. A 7030 Engineering Console (IBM Stretch) was 67 in x 64 in x 29 1/2 in and cost $8M each, for example. So the need for a system with time sharing and file management features was a priority - which became a reality with the development of the UNIX operating system by Kenneth Thompson and Dennis Ritchie.

<br>

<!-- ![Image of a computer around the year of 1960](/assets/images/posts/2024-10-27-Setting_VM/ibm.jpg){: style="display: block; margin: 0 auto; height: 300px;"} -->

![Image of a computer around the year of 1960]({{site.url}}/assets/images/posts/2024-10-27-Setting_VM/ibm.jpg){: style="display: block; margin: 0 auto; height: 200px;"}

<br>

The reasons behind the use of VM’s in the industry today are mostly the same as the urge for time sharing systems back in the day: resource optimization. Virtual machines create an isolated environment on host hardware, behaving like detached work stations. Many of today’s technological advancements, like cloud computing and AI, are based on the concept of virtual machines. For example, in cloud computing, VM’s are used to virtualize the resources of cloud service provider’s servers.

And what are hypervisors? They are the most essential components in the virtualization stack. Hypevisors, also called Virtual Machine Monitor (VMM) are the ones responsible for creating the virtual platform on the host computer, on top of which the guest OS is monitored and executed. They are usually classified as Bare Metal (Type 1) and Hosted (Type 2). Bare metal is a software that runs directly on the hardware, without any layer between the VMM and the host. Hosted hypervisors, on the other hand add a layer of software on top of the current OS.

<br>

<!-- ![Illustration of the types of Virtual Machines](/assets/images/posts/2024-10-27-Setting_VM/VMs.png){: style="display: block; margin: 0 auto; height: 300px;"} -->

![Illustration of the types of Virtual Machines]({{site.url}}/assets/images/posts/2024-10-27-Setting_VM/VMs.png){: style="display: block; margin: 0 auto; height: 200px;" class="responsive-image"}

<br>

I’ve played with Virtualbox before (which is considered a type 2 hypervisor) and wanted to try something new. Influenced by <a href="https://www.linkedin.com/in/otaviof/" class="custom-link" >Otávio Fernandes</a> and <a href="https://www.linkedin.com/company/linuxtips/" class="custom-link">LINUXtips</a> I decided to go ahead with Proxmox, which is an open-source bare-metal VM - for what it is worth it seemed a good starting tool for my first homelab. I was expecting to spend less to none on my first home lab so I went looking for some Raspberry PI’s. Was almost closing a deal on Ebay for a second-hand Pi 4 when I remembered my wife has an old laptop that has been catching nothing but dust in the closet. It is a Dell Inspiron 11z, 13’’ U4100 @1.30GHz with Windows 7 and 2GB RAM. Proxmox has extensive documentation, but you can find quick installation tutorials all over.

Proxmox provides a web-based interface for managing your virtual environments, which became pretty handy for someone like me who’s just starting in the game. All right, all was good so far: I’ve started my first home lab and spent $0 making use of a laptop that would probably be thrown away once we remembered it was still around after 10 years.

<br>
<!-- 
![Picture of my working laptop and the laptop I used to install Proxmox](/assets/images/posts/2024-10-27-Setting_VM/both_laptops.jpg){: style="display: block; margin: 0 auto; height: 300px;"} -->

![Picture of my working laptop and the laptop I used to install Proxmox]({{site.url}}/assets/images/posts/2024-10-27-Setting_VM/both_laptops.jpg){: style="display: block; margin: 0 auto; height: 200px;"}

<br>

But then came the first bump - of course it would. The gracious laptop I’ve decided to use as a host for my first home lab does not have support for VM’s ( !!! ), I never thought of that possibility. After some research I found out that indeed many laptops and computers lack support for virtualization in their BIOS, which prevented me from using Ubuntu ISO to create a VM on Proxmox.

<br>

<!-- ![Screenshot of the error in Proxmox](/assets/images/posts/2024-10-27-Setting_VM/VM_not_supported.png){: style="display: block; margin: 0 auto;"} -->

![Screenshot of the error in Proxmox]({{site.url}}/assets/images/posts/2024-10-27-Setting_VM/VM_not_supported.png){: style="display: block; margin: 0 auto;"}

<br>

A couple days of more research went by until I found a “workaround”. Other than VM’s, Proxmox has support for LXC (Linux Containers) as a lightweight alternative to Virtual Machines. I’ve had experience with containerization before, and I never thought I could use it for anything other than developing applications. Okay, let’s take a step back and understand where I am: I started this project with the idea of building my first home lab primarily using virtualization so I could go on with the school project I’ve been working on and find another solution other than VirtualBox, especially due to my growing interest in Linux. However, given the circumstances, I now need to shift strategies and build the same home lab using containerization instead of virtualization. While virtualization uses a hypervisor to emulate hardware, containers run directly on the operating system, which is why Linux containers can only be used on Linux OS. These are two different concepts, and I might never have encountered them if it weren’t for my first home lab. This is so great! It’s mind-blowing how a simple project has taught me so much.

Okay, wrapping it up now… The LXC templates in Proxmox (also referred to as templates) are provided by Proxmox VE in a list. All I had to do was browse through their list, download the Ubuntu template I wanted to use as my server, and install it. Easy peasy! Now I have a fully functional server running on an LXC available 24/7. Awesome, isn’t it? I won’t be able to run Ubuntu as I originally thought for the school project, but that’s okay. I eventually used VirtualBox for that while learning exciting concepts about infrastructure and containerization for my own Linux server.

<br>

<!-- ![Screenshot of the error in Proxmox](/assets/images/posts/2024-10-27-Setting_VM/ubuntu_server1.png){: style="display: block; margin: 0 auto;"} -->

![Screenshot of the error in Proxmox]({{site.url}}/assets/images/posts/2024-10-27-Setting_VM/ubuntu_server1.png){: style="display: block; margin: 0 auto;"}

<br>
