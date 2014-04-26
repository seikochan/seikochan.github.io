---
layout: post
title:  "GitHub and Git: Basics"
date:   2014-02-13 08:55:24
categories: github git 
image:
 feature: octocat_bg.jpeg
---

As a programmer, this is one of the best tools to get to know.  It helps to facilitate workflows and make it faster as well as easier to collaborate.  Before GitHub, the common way to collaborate would be by sending code back and forth through emails.  This was hard to deal with and often took too much time to correctly setup and verify which files were changed and which were not.  Much of a programmer's time would be spent on just trying to collaborate on code instead of improving and working on it.

With GitHub, we are now able to collaborate in a very convenient way.  Basically GitHub provides a platform for many programmers to colloborate and offer advice on other people's programs.  It is basically a social network for programmers!  While some projects may be made private, much of the focus of GitHub is open-source social coding.  This allows people to look at other people's code and learn from it or even suggest better alternatives that the owner may incorporate to make their code more effective or efficient.  GitHub also comes with many other tools, such as versioning, commit history of what exactly changes in each commit, a place for people to submit issues they find, and much, much [more].

##Getting Started  
Although getting started with using GitHub is quite daunting, it will be worth it in the end.  It does have a huge learning curve to it and will take a lot of practice and repetition to start to get the hang of it.  Although GitHub has a UI to do the git commands in, we will be doing the old fashion way of using Git through the terminal/command line.  But don't worry, Git provides many tools to help along the way!

To begin, just go to [GitHub] and create an account.  Make sure to use a main email account since a lot of the notifications will go there.  After, follow the [walkthrough] that GitHub provides to download Git and connect your local Git to your account on GitHub.

##Basic Workflow 
1. 'git init'  
First, create a local directory where you would like all your files to be located.  Then do the command 'git init', which will initialize git in the directory for that project.  To verify that 'git init' worked, make sure that the .git file was created.

{% highlight bash linenos %}
[seikochan@localhost sample_test]$ git init
Initialized empty Git repository in /home/seikochan/Work/sample_test/.git/
[seikochan@localhost sample_test]$ ls -al
total 12
drwxrwxr-x.  3 seikochan seikochan 4096 Mar 25 12:09 .
drwxrwxr-x. 12 seikochan seikochan 4096 Mar 25 12:09 ..
drwxrwxr-x.  7 seikochan seikochan 4096 Mar 25 12:09 .git
{% endhighlight %}

2. add/modify content  
Next, you want to just add some content or, if you already have files setup, make some modifications.  In this case I will just make a simple readme.

{% highlight bash linenos %}
[seikochan@localhost sample_test]$ vim README.md
[seikochan@localhost sample_test]$ cat README.md 
This a sample test project to show the basic workflow of git and github.
[seikochan@localhost sample_test]$ ls
README.md
{% endhighlight %}


3. git status  
Now that we have made changes, we can use 'git status' to see what has changed.  By using this command, we can see the tracked files (files that have changed and will be added to the commit) and untracked files (files that have changed that will not be added to the commit and ignored by git).  Looking below, we can see that the readme file is currently not being tracked and so it prompts us to use 'git add' to add it to the tracked files.

{% highlight bash linenos %}
[seikochan@localhost sample_test]$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	README.md

nothing added to commit but untracked files present (use "git add" to track)
{% endhighlight %}

3. 'git add'
{% highlight bash linenos %}
[seikochan@localhost sample_test]$ git add README.md 
[seikochan@localhost sample_test]$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   README.md

[seikochan@localhost sample_test]$ vim junkfile
[seikochan@localhost sample_test]$ cat junkfile 
this is junk
[seikochan@localhost sample_test]$ git add junkfile 
[seikochan@localhost sample_test]$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   README.md
	new file:   junkfile
{% endhighlight %}

6. git commit -m 'description'  
Now that we have made some modifications and 'added' all the changes we want to keep track of, we can now 'commit' these changes to the history of this project.  Imagine each commit as a breakpoint in a project, where Github allows us to see the changes from one commit to the next.

{% highlight bash linenos %}
[seikochan@localhost sample_test]$ git commit -m 'Initial Commit'
[master (root-commit) 153a770] Initial Commit
 2 files changed, 3 insertions(+)
 create mode 100644 README.md
 create mode 100644 junkfile
[seikochan@localhost sample_test]$ git status
On branch master
nothing to commit, working directory clean
{% endhighlight %}  

NOTE:  This commit is only locally saved, so you will not see any changes to a project on the Github website!


6. 'git push'   
Now that we have local commit(s), we want to 'push' it up to Github so that we have a non-local commit history.  But as you can see if we try to push now we get an error.  Git is trying to tell you "Hey I don't know where to push this!".  

{% highlight bash lineos %}
[seikochan@localhost sample_test]$ git push
fatal: No configured push destination.
Either specify the URL from the command-line or configure a remote repository using

    git remote add <name> <url>

and then push using the remote name

    git push <name>
{% endhighlight %}  

So we need to create a matching account on Github first and "connect" the two to each other.  The local copy we call the master (by convention).  The github copy is called origin (by convention).  So navigate to your Github account (github.com/username), click "Repository" (circled in yellow), and then click "New +" (also circled in yellow).    
![new-github-repo]  

You will then see the below page.  By convention, you should name your repo the same as your local copy.  Make sure that the "Initialize repository with a README" is unchecked, since we have already started the project locally and made changes.   
![git-new-repo]  

Now you have to "connect" this github repository with your local on.  This mean setting your online github repository as the remote to which you want to push to.  Thankfully, Github knows you need to do this and will provide you with the commands to do it! 
![github-simple-instructions]  

You can just copy paste all those into your terminal and you're good to go!  Since we created the repo locally first, we will use the "Push an existing repository from the command line" commands.  As you can see below, you can first use git remote -v (the -v means verbose) to see if there is any remotes connected.  There isn't so we add a remote and after we can see that any 'fetch' or 'push' we do from this project will be from and to the same git repo on Github.  

{% highlight bash lineos %}
[seikochan@localhost sample_test]$ git remote -v
[seikochan@localhost sample_test]$ git remote add origin git@github.com:seikochan/sample_test.git
[seikochan@localhost sample_test]$ git remote -v
origin	git@github.com:seikochan/sample_test.git (fetch)
origin	git@github.com:seikochan/sample_test.git (push)
{% endhighlight %}


Now we can finally git push!  Using the below command, we are saying "Push my local repository and its commits (master) to my Github.com repository (origin)".

{% highlight bash lineos %}
[seikochan@localhost sample_test]$ git push -u origin master
Counting objects: 4, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 336 bytes | 0 bytes/s, done.
Total 4 (delta 0), reused 0 (delta 0)
To git@github.com:seikochan/sample_test.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
{% endhighlight %}  


Now if you refresh your Github repository, you should see something like this.  It has your latest commit that you have just put up and if you navigate through it, it will show you what you have changed in each file.  
![github-complete]  


5. 'git pull'  
Remember that GitHub change also have changes done via the site as well.  Also, if you are collaborating, changes from other may occur to your online repository.  So a very important thing to do before working on one the projects is to do a 'git pull'.  This means "pull any changes that have been added to the GitHub repo".  

{% highlight bash lineos %}
[seikochan@localhost sample_test]$ git pull
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Unpacking objects: 100% (3/3), done.
From github.com:seikochan/sample_test
   153a770..bd9c045  master     -> origin/master
Updating 153a770..bd9c045
Fast-forward
 junkfile | 3 +++
 1 file changed, 3 insertions(+)
[seikochan@localhost sample_test]$ git pull
Already up-to-date.
{% endhighlight %}    

NOTE: If you make local changes that conflict with changes from the GitHub repo you may run into issues and may no longer be able to push or pull any changes!!  MAKE SURE TO ALWAYS 'git pull' before anything!  


##Additional Convenient Commands

4. 'git add -u'  
Sometimes you might have to completely remove or delete certain files. But when you try to 'add' the files to be commited, you might run into the problem that 'git add' no longer does what you want!  To add any "deleted" files to you commits, you need to use 'git add -u'.

{% highlight bash lineos %}
[seikochan@localhost sample_test]$ ls
junkfile  README.md
[seikochan@localhost sample_test]$ rm -f junkfile 
[seikochan@localhost sample_test]$ ls
README.md
[seikochan@localhost sample_test]$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	deleted:    junkfile

no changes added to commit (use "git add" and/or "git commit -a")
[seikochan@localhost sample_test]$ git add junkfile 
warning: You ran 'git add' with neither '-A (--all)' or '--ignore-removal',
whose behaviour will change in Git 2.0 with respect to paths you removed.
Paths like 'junkfile' that are
removed from your working tree are ignored with this version of Git.

* 'git add --ignore-removal <pathspec>', which is the current default,
  ignores paths you removed from your working tree.

* 'git add --all <pathspec>' will let you also record the removals.

Run 'git status' to check the paths you removed from your working tree.

[seikochan@localhost sample_test]$ git add -u junkfile 
[seikochan@localhost sample_test]$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	deleted:    junkfile
{% endhighlight %}


7. 'git log' and 'git diff'
Similar to 'git status', but each with their own unique functionalites, there is 'git log' and 'git diff'.    

'git log' will show you your local commit history, its address, who committed it, when it was committed, and what the commit description was.

{% highlight bash lineos %}
[seikochan@localhost sample_test]$ git log
commit bd9c0459fe40cb6684954aed3d00076f19722c53
Author: seikochan <j.s.ishigami@gmail.com>
Date:   Thu Apr 3 00:12:13 2014 -1000

    Update junkfile

commit 153a770675eb8a88cc750c8ae9d5d78b0daddf7b
Author: seikochan <j.s.ishigami@gmail.com>
Date:   Tue Mar 25 13:03:51 2014 -1000

    Initial Commit
{% endhighlight %}  

On the other hand, 'git diff' will show the changes, or differences, between different commits.  If 'git diff' is entered with no specifications, it will just show specifically what has been changed compared to the most recent commit.  You may also specify which commits to show the differences between.  For example, 'git diff HEAD~1..HEAD' means to compare and show the differences between right now (HEAD) and 1 commit ago (HEAD~1).

{% highlight bash lineos %}
[seikochan@localhost sample_test]$ git diff
diff --git a/junkfile b/junkfile
index 17d0324..da185dc 100644
--- a/junkfile
+++ b/junkfile
@@ -2,3 +2,5 @@ this is junk
 
 These are the lines that I have added via Github.com
 :D
+
+These are lines I have just modified locally but not yet commited!
[seikochan@localhost sample_test]$ git diff HEAD~1..HEAD
diff --git a/junkfile b/junkfile
index 811d575..da185dc 100644
--- a/junkfile
+++ b/junkfile
@@ -1 +1,6 @@
 this is junk
+
+These are the lines that I have added via Github.com
+:D
+
+These are lines I have just modified locally but not yet commited!
{% endhighlight %}    

NOTE: 'git diff' will detail exactly which files where changed and what lines where added, deleted, or modified.  In the above file, you can see that 

8.  gitk/gitg  
But for some of us, even with git status, git log, and git diff, its still too difficult to visualized the changes!  Don't worry!  You can install (with yum) gitk or gitg.  This will provide a decent user interface to view the commit history, the changes in each commit, and more.  Below are 2 images of gitk and gitg for the current sample_project.  

![gitk-sample]  ![gitg-sample]



[more]: https://github.com/features
[Github]: https://github.com
[walkthough]: https://help.github.com/articles/set-up-git
[new-github-repo]: /images/new_github_repo.png  "How to create new github repo."
[git-new-repo]: /images/Git_new_repo.png "How to set up new repo."
[github-simple-instructions]: /images/github_simple_instructions.png "How to setup github repo as remote for local repository to push to."
[github-complete]: /images/complete_github.png "Github repository with the first commit pushed up."
[gitk-sample]: /images/gitk.png "Gitk for the sample_project."
[gitg-sample]: /images/gitg.png "Gitg for the sample_project."