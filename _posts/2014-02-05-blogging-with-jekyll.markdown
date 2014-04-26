---
layout: post
title:  "Blogging with Jekyll"
date:   2014-02-05 18:55:41
categories: jekyll blog githubpages markdown
image:
 feature: jekyll_bg.png
---

Instead of using a premade site or writing a blog using html, I was introduced to a much better alternative of a static site generator called [Jekyll].  The advantages of blogging using Jekyll are: 


1. It utilizes [markdown] while still supporting css, html, and liquid.
		By incorporating markdown, Jekyll makes it easier to write posts and content really easily with having to know all the html for formatting or laying out the content.  It also makes posts easier to read, add to, or update.

2. It generates a static site.  
		This means that the webpage is displayed exactly as stored and there are no other web application needed to generate it.  Its great for blogs since much of the content doesn't need to updated constantly.  Also, it leads to less security issues as well.

##Getting Started
Jekyll isn't the easiest tool to learn or use but its worth it!  To get started, make sure you have ruby already installed.  If you have the Fedora ruby, check out [rbnev].  Then all you need to do is follow the Quick-start Instructions on [Jekyll] and you are almost there!

##Creating a Post
Now all you need to do is create a plain text file in your _posts folder with the extension .markdown (so that Jekyll knows to parse the markdown into html).  Make sure to follow the given naming convention of the posts:

 yyyy-mm-dd-title-of-blog-here.markdown

Fill in the content with the yml header and your blog post content written with markdown syntax.

##Viewing Static Site
Now that you have created a post, navigate to your blog directory and run the command:

	{% highlight bash linenos %}
	[username@localhost Jekyll-Blog]$ jekyll serve
	Configuration file: /home/username/Work/Jekyll-Blog/_config.yml
	            Source: /home/username/Work/Jekyll-Blog
	       Destination: /home/username/Work/Jekyll-Blog/_site
	      Generating... done.
	 Auto-regeneration: enabled
	    Server address: http://0.0.0.0:4000
	  Server running... press ctrl-c to stop.
	  {% endhighlight %}

As you can see, all you need to do is open a browser to the server address and there you have it! Your own site powered by jekyll. 

If you want even more details, you can check out [Jekyll's Documentation] or [Yes We Jekyll].


[markdown]: http://seikochan.github.io/markdown/redcarpet/writing-in-markdown/
[Jekyll]: http://jekyllrb.com/
[Jekyll's Documentation]: http://jekyllrb.com/docs/home/
[themes]: http://jekyllthemes.org/
[Yes We Jekyll]: http://yeswejekyll.com/

