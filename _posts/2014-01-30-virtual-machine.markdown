---
layout: post
title:  "Fedora's Virtual Machine Manager: libvirt"
date:   2014-01-30 15:05:58
categories: kvm, virt, virtual manager 
image:
 feature: libvirt_bg.png
---

Now that I have fully converted my machine over to Fedora 20, I still need a way to use Windows 7.  Luckily, Fedora comes with a virtual machine, [libvirt] using KVM.  Yum install libvirt.  Download a Windows 7 iso and the virtio iso from RedHat.  Open the "Virtual Machine Manager" and create a new virtual machine.  Run though the install process of Windows 7.  After thats done, make sure to check in the virtual machine manager settings and details under networking and disk, and change them to user virtio.  This native virtio created by RedHat will make your virtual machine run faster. 

![virtual_machine_details](/images/virt_machine_details.png) 

[libvirt]: libvirt.org

