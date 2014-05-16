---
layout: post
title:  "Transifex"
date:   2014-03-26 12:29:57
categories: transifex, translations
image:
 feature: transifex_bg.jpeg
---

[Transifex] provides a service of easy translation management.  It also provides version control, translation history, and most important to us, continuous localization.  With this, we were able to upload the locale files so that there is community provided translation help.

If the project is open-source, Transifex is free to use.  There has to be proof by providing a link to something like a Github Repository and then Transifex will allow you to use their servers.  Although Transifex comes with Fedora (as in you can 'yum install' it), you would need to have your own server to host it if you don't have an open-source project or are not willing to pay Transifex for their service.  Also, it is nice to know that Transifex price scales with the size of the project so if your project is small, it might not be that bad.  Another added plus is that Transifex has paid transilators who will work on your translations if you do pay for their services.  Transifex also supports many translations files, but the most common one is po/pots.  Unfortunately for us, we use yaml files and although it is supported, there was difficulty finding documentation for it.  

For our project, [litecoin.org on Transifex], it is free since its open-source so we rely on the community for our translations.  Its very simple to become a translator and I have a brief description on my [litecointalk post].  

## Getting Started: Downloading Transifex Command Line Tool
Although you can use the UI on Transifex to use its services, they also kindly provide a command line tool that you can choose to use instead.  Here I will talk about how to get that tool installed on a Fedora system and how to use it.  

1. First try a 'yum search transifex'.  From this you will see that indeed Fedora does have the transifex tool.  
{% highlight bash lineos %}
[username@localhost ~]$ yum search transifex
Loaded plugins: auto-update-debuginfo, langpacks, refresh-packagekit
adobe-linux-x86_64                                                                                                                                2/2
google-chrome                                                                                                                                     3/3
google-talkplugin                                                                                                                                 1/1
=============================================================== N/S matched: transifex ===============================================================
transifex-client.noarch : Command line tool for Transifex translation management
create-tx-configuration.noarch : An easy way to create Transifex client configuration files
transifex.noarch : A system for distributed translation submissions

  Name and summary matches only, use "search all" for everything.
{% endhighlight %}  

2. Next do a 'yum install transifex-client'.  

3. To see if its installed, use 'tx --version'.  
{% highlight bash lineos %}
[username@localhost ~]$ tx --version
0.10
{% endhighlight %}


## Getting Started: Using the Transifex Command Line Tool  
You can check out [Transifex's docs][transifex docs] and their [overview][transifex overview] for more information.  Below I just go over some simple commands and some of the useful solutions we ran into to solve some of our issues.  If you prefer a different guide, another good one about using the transifex command line tool with yaml files is [here][translation process].

1. Now that you have transifex command line tool installed, you can use it in your terminal.  Transifex command is 'tx'.  To see all the possible commands you can use, just type 'tx --help'.   
{% highlight bash lineos %}  
[username@localhost ~]$ tx --help
Usage: tx [options] command [cmd_options]

This is the Transifex command line client which allows you to manage your
translations locally and sync them with the master Transifex server. If you'd
like to check the available commands issue `tx help` or if you just want help
with a specific command issue `tx help command`

Options:
  --version             show program's version number and exit
  -h, --help            show this help message and exit
  -d, --debug           enable debug messages
  -q, --quiet           don't print status messages to stdout
  -r ROOT_DIR, --root=ROOT_DIR
                        change root directory (default is cwd)
  --traceback           print full traceback on exceptions
  --disable-colors      disable colors in the output of commands
{% endhighlight %}

2. Like git, you need to do a 'tx init' in the directory of your project.  Follow the instructions [here][tx init].  Make sure to first create a Transifex account and project.  Then for the prompt 'Transifex instance [https://www.transifex.com]:', you will provide the url of your project.  

3. Although you can follow the instructions by [Transifex's documentation][transifex docs] of using 'tx set' to set up your file mappings, I found it much easier to just modify the tx .config file itself.  It does the same thing and you no long have to specify it with so many option flags using 'tx set'.  You can view the litecoin.org [config file] to get a little understanding of what could be added to the config file.  The .config file is located in the .tx file of your project.  (If you haven't done 'tx init' you won't find the .tx directory!)  Of course, there are other things you can add to the config file as well!  

{% highlight bash lineos %}  
[username@localhost litecoin.org]$ ls -al
total 44
drwxrwxr-x.  7 username username 4096 Mar 25 18:02 .
drwxrwxr-x. 17 username username 4096 Apr 18 14:30 ..
drwxrwxr-x. 16 username username 4096 Mar 16 17:42 build
-rw-rw-r--.  1 username username 1505 Mar 25 16:43 config.rb
-rw-rw-r--.  1 username username  312 Feb 15 17:44 Gemfile
-rw-rw-r--.  1 username username 2248 Feb 15 17:44 Gemfile.lock
drwxrwxr-x.  8 username username 4096 Mar 25 18:11 .git
-rw-rw-r--.  1 username username  428 Feb 15 17:44 .gitignore
drwxrwxr-x.  2 username username 4096 Mar 25 18:12 locales
-rw-rw-r--.  1 username username   0 Feb 15 17:44 README.md
drwxrwxr-x.  7 username username 4096 Feb 28 09:34 source
drwxrwxr-x.  2 username username 4096 Mar 16 20:29 .tx
[username@localhost litecoin.org]$ cd .tx
[username@localhost .tx]$ ls
config
[username@localhost .tx]$ cat config 
[main]
host = https://www.transifex.com

[litecoinorg.master]
file\_filter = locales/<lang>.yml
source\_file = locales/en.yml
source\_lang = en
type = YAML
{% endhighlight %}  

NOTES: 
host - means that we are using transifex's server instead of hosting it ourselves.   
file\_filter - tells transifex that we only want it to look at the files that follow the specified format in the specific folder 'locales'.  
source\_file - tells transifex that from now on, when we say source file, we are refering to locales/en.yml.  
source\_lang - tells transifex that the source language for our project is en (english).  
type - tells transifex that the type of language files we are using are yaml (files may use either .yaml or .yml)  

4. Now you can use 'tx push'.   
To push up your initial source file or update your source file, just type in 'tx push -s'.  Since you specified the source file in the config file for tx, it knows which file to push up.  If you have set it up correctly, you will see the changes reflected on transifex.com.  
{% highlight bash lineos %}
[username@localhost litecoin.org]$ tx push -s
Pushing translations for resource litecoinorg.master:
Pushing souce file (locales/en.yml)
Done.
{% endhighlight %}  

To push any of your translations files that you would like for people to translate for you, make a local copy, and use 'tx push -t'.  This will push up any new language file if it passes the file\_filter.  In this case, all new yml files created in the locales files other than en.yml will get pushed up.  

{% highlight bash lineos %}
[username@localhost litecoin.org]$ tx push -t
Pushing translations for resource litecoinorg.master:
Pushing 'el' translations (file: locales/en.yml)
Pushing 'fr' translations (file: locales/fr.yml)
Pushing 'nl' translations (file: locales/nl.yml)
Pushing 'pt' translations (file: locales/pt.yml)
Pushing 'de' translations (file: locales/de.yml)
Pushing 'it' translations (file: locales/it.yml)
Done.
{% endhighlight %}  


5. Finally everything is set up nicely and all you have to do is a 'tx pull' just like a git pull to get any changes to your translation files!  

NOTE:  If new languages are added to Transifex via the website (meaning no local instance of the file), tx pull will not pull those files unless specifically pulled with language name (ie. 'tx pull --language=pl).



<!--
#TRANSIFEX
----------
yum install transifex-client  (command line tool)
tx --help
http://support.transifex.com/customer/portal/articles/960804-overview
can host via fedora
need own server tho
VCS=version control system
FIGURED IT OUT
	-set config file
	-use tx push -s     (source)  
	-use tx -push -t    (translations)
watch recording: 3/16/14 (pt2)
*if new languages added to transifex via site (meaning no local instace of the file), tx pull will not pull it unless specifically pull language with (tx pull --language=pl)

http://middlemanapp.com/advanced/localization/index.html
in config file of middleman, get rid of :langs (<- ignores all other languages that were in locales unless specified here)  this will make all languages in locales file now work (first language found in locales will be default)
use :mount_at_root => :es

i18n is a ruby gem :D

not sane to do it yourself
free for open-soure projects, pay scales with project
transifex has paid translators working on it as well
-->


[Transifex]: https://www.transifex.com/features/translation-management/
[litecointalk post]: https://litecointalk.org/index.php?topic=17395.0
[litecoin.org on Transifex]: https://www.transifex.com/projects/p/litecoinorg/
[config file]: https://github.com/litecoin-project/litecoin.org/blob/master/.tx/config
[translation process]: http://docs.silverstripe.org/framework/en/trunk/misc/translation-process
[transifex docs]: http://support.transifex.com/customer/portal/topics/440187-transifex-client/articles
[transifex overview]: http://support.transifex.com/customer/portal/articles/960804-overview
[tx init]: http://support.transifex.com/customer/portal/articles/995852-project-initialization