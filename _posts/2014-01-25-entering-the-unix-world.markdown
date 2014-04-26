---
layout: post
title:  "Entering the Linux World: Fedora 20"
date:   2014-01-25 13:04:47
categories: fedora linux OS
image:
 feature: fedora_bg.jpg
---

For most of my life I have been only a Windows user, content with the capabilities that Windows provides.  But as I continued into the field of Computer Science,  Windows Operating System just provided more and more trouble to deal with.  Finally I had the opportunity to make the switch from Windows to a linux operating system, in this case Fedora.

With a massive amount of help from [Warren Togami], the founder of the Fedora Operating System, I was able to completely redo my computer setup and have Fedora 20 installed as main OS.

##Handy Shortcuts
Now that I've entered the Linux World I've found that knowing shortcuts is almost expected.  

[Here] and [here] I found some extremely convinient and helpful shortcuts to use.

##Installing Programs via Fedora
Another amazing capability that linux systems have is that they provide their own versions of software package managers.  Fedora uses [yum].  So if you want to install a certain program you should actually check yum to see if it has it first!

For example if you wanted to install clisp you would:

1. check if it is already installed on your system: 

	{% highlight bash linenos %}
    [root@localhost ~]# rpm -qa | grep 'clisp*'
    {% endhighlight %}
   
   NOTE: The [rpm] is the Red Hat Package Manager and the -qa means to query all installed rpm packages.

   OR you could also use

	{% highlight bash linenos %}
    [root@localhost ~]# yum list installed | grep 'clisp*'
    {% endhighlight %}  


2. check if yum has it:  
	{% highlight bash linenos %}
	[root@localhost ~]# yum search clisp
	Loaded plugins: langpacks, refresh-packagekit
	================================================================= N/S matched: clisp =================================================================
	clisp-devel.i686 : Development files for CLISP
	clisp-devel.x86_64 : Development files for CLISP
	maxima-runtime-clisp.x86_64 : Maxima compiled with clisp
	clisp.i686 : ANSI Common Lisp implementation
	clisp.x86_64 : ANSI Common Lisp implementation

  	Name and summary matches only, use "search all" for everything.
  	{% endhighlight %}
  	

  We can see that yum found the following packages with the name 'clisp' in it.  

 3. install it using yum: 
 	{% highlight bash linenos %}
	[root@localhost ~]# yum install clisp
	Loaded plugins: langpacks, refresh-packagekit
	Resolving Dependencies
	--> Running transaction check
	---> Package clisp.x86_64 0:2.49-12.20130208hg.fc20 will be installed
	--> Finished Dependency Resolution

	Dependencies Resolved	

	======================================================================================================================================================
 	Package                       Arch                           Version                                            Repository                      Size
	======================================================================================================================================================
	Installing:
 	clisp                         x86_64                         2.49-12.20130208hg.fc20                            fedora                         3.3 M

	Transaction Summary
	======================================================================================================================================================
	Install  1 Package

	Total download size: 3.3 M
	Installed size: 18 M
	Is this ok [y/d/N]: y
	Downloading packages:
	clisp-2.49-12.20130208hg.fc20. FAILED                                          
	http://ftp.ussg.iu.edu/linux/fedora/linux/releases/20/Everything/x86_64/os/Packages/c/clisp-2.49-12.20130208hg.fc20.x86_64.rpm: [Errno 14] curl#6 - "Could not resolve host: ftp.ussg.iu.edu"
	Trying other mirror.
	clisp-2.49-12.20130208hg.fc20.x86_64.rpm                                                                                       | 3.3 MB  00:00:50     
	Running transaction check
	Running transaction test
	Transaction test succeeded
	Running transaction
	  Installing : clisp-2.49-12.20130208hg.fc20.x86_64                                                                                               1/1 
	  Verifying  : clisp-2.49-12.20130208hg.fc20.x86_64                                                                                               1/1 

	Installed:
 	 clisp.x86_64 0:2.49-12.20130208hg.fc20                                                                                                              

	Complete!
	{% endhighlight %}

   NOTE: You don't have to worry about telling yum which version to download!  It will automatically download the correct one corresponding to your computer specs.  As you can see, yum installed the 64-bit version of clisp for me since my computer is 64-bits. 
    

##Manually Installing Programs: Using /opt/bin/
Unfortunately if yum does not have the program, you will have to manually download it from the server itself.  But do not fear, there is a way to make your programs work system-wide, or if you want, make it user-dependent!  The basic idea is to place it in your `/opt` directory and make a sym-link (symbolic link) to the program in your `usr/local/bin/`.

For example if you wanted to install sublime2:

<!-- 1. download the program and unzip it into your /opt directory:
 -->	
	{% highlight bash linenos %}
	[root@localhost ~]# cd /opt
	[root@localhost opt]# tar xfv /home/username/Downloads/Sublime Text 2.0.2 x64.tar.bz2
	[root@localhost opt]# cd Sublime\ Text\ 2/
	[root@localhost Sublime Text 2]# ls
	Icon  lib  PackageSetup.py  Pristine Packages  sublime_plugin.py  sublime_text
	{% endhighlight %}

2. make a symlink in your /usr/local/bin

	{% highlight bash linenos %}
	[root@localhost ~]# cd /usr/local/bin
	[root@localhost bin]# ls
	[root@localhost bin]# ln -s /opt/Sublime\ Text\ 2/sublime_text
	[root@localhost bin]# ls -l
	total 0
	lrwxrwxrwx. 1 root root 32 Jan 17 17:31 sublime_text -> /opt/Sublime Text 2/sublime_text
	{% endhighlight %}
	
   NOTE: the ls -l shows that the command 'sublime\_text' is actually a symbolic link to '/opt/Sublime Text 2/sublime\_text'.

3. test it from anywhere!

	{% highlight html linenos %}
	[root@localhost ~]$ sublime_text .
	{% endhighlight %}




[Warren Togami]: https://plus.google.com/111016575583263172224/about
[Here]:http://www.tomshardware.com/reviews/fedora-16-gnome-3-review,3155-10.html
[here]:https://wiki.gnome.org/Projects/GnomeShell/CheatSheet
[yum]:https://fedoraproject.org/wiki/Yum
[rpm]:http://www.thegeekstuff.com/2010/07/rpm-command-examples/



