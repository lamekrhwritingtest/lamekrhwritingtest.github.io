---
layout: quickstart
title: About
permalink: /about/
---
I included the following supplemental information to help provide context for reviewers as they evaluate some of the decisions I made while working on this writing test.

# My approach to this writing test
The bullets below capture the steps I followed while working through this writing test.

* Understand ownCloud
  * Read through the Digital Ocean guide on deploying ownCloud on Ubuntu 16.04
  * Read through the ownCloud docs (Admin and User manuals)
  * Read through the Digital Ocean guide on deploying ownCloud on Ubuntu 18.04
  * Watched a YouTube video on adding users to an ownCloud instance
* Practice installing and using ownCloud
  * Followed the DO guide on deploying ownCloud for Ubuntu 16.04
    * I got stuck accessing the site. I suspect the Apache server configuration doesn’t point the url to the ownCloud folder, but I couldn’t resolve this.
  * Followed the DO guide on deploying ownCloud for Ubuntu 18.04
    * This worked for me the first time. I had some trouble connecting to the site using the desktop client, but resolved the issue by changing the user’s password immediately after creation.
* Write the procedure
  * I used my notes from my research and testing, and drafted the procedure in Google Docs
* Brush up on Jekyll
  * Read through the Jekyll docs
  * Practiced the Jekyll quickstart
    * To accomplish this I had to set up a Ruby dev environment. This involved a number of false starts. I was unable to get Jekyll to install on my laptop (some issue with commonmark I could not resolve). After 2 failed attempts, I decided to spin up a Ruby dev environment using pre-baked instances on Google Cloud Platform.
* Set up my Github Pages / Jekyll site
  * I started by following the Jekyll quickstart
  * I added a theme, and tweaked a few things (logo, nav)
  * I finished by adding my procedure to the site, and polishing up things like the copyright date and the theme colors.

# Notes on the content I chose to include/exclude
ownCloud runs on a number of different platforms, but documenting them all was outside the scope of this exercse. As well, the exercise prompts covered different types of usage (administration tasks and user tasks). Because of this, I decided to focuse on one specific OS (Ubuntu 18.04).

ownCloud is also highly customizable. Instead of trying to provide a complete reference of all available options, again I focused on what I deemed to be the easiest path for the user to get up and running with ownCloud. I think if this guide were to serve an audience that wanted to install ownCloud in production, more content on security would need to be added.

# Notes on additional accounts
To complete this exercise, I set up additional Github and Gmail accounts.

I set up an additional Github account for two reasons:
* I didn’t want to overwrite or add to my existing github pages site.
* On the off chance that anyone at my current company was checking out my GH account, I didn’t want to trigger any suspicions about interviewing.

I set up an additional Gmail account to verify my Github account, but also so I could use the associated free GCP trial for my Ruby dev environment.
