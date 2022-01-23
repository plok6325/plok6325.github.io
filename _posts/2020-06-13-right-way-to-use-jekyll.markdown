---
title: The right way to use jekyll
date: 2020-06-13 00:00:00
categories: tutorial
--- 



# The right way to use jekyll
1. Install a full Ruby development environment.
2. Install Jekyll and bundler gems.
		
		gem install jekyll bundler
		bundle add webrick **windows** 
		sudo apt-get install ruby-full build-essential zlib1g-dev **ubuntu**
3. Create a new Jekyll site at ./myblog.
	
		jekyll new myblog
4. Change into your new directory.
	
		cd myblog
5. Build the site and make it available on a local server.
	
		jekyll serve

6. Browse to http://localhost:4000


# Github 
