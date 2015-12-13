---
layout: post
title:  "Changing Author Info On Previous Git Commits"
date:   2015-11-17 20:40:00
author: James L
categories: git github
image: /assets/git-github-header.png
imageAlt: I'm James - Changing Author Info On Previous Git Commits
---

I recently picked up a new MacBook Pro & was a little too eager to continue working on a project; after getting the Xcode command line tools installed & cloning my repository, I got to work. Upon pushing my commits I realised I made the somewhat silly (& easy to make) mistake of not setting my author name & email address in the Git config.

By default, if you haven't set any preferences in your git config file then git will use your Mac's username for your git username & computer name for your git email. Naturally you don't want to be using this for your commits & these commits are anonymous when they hit GitHub. You won't get any marks on your profiles 'Contributions' and the commit won't get any profile information either - less than ideal.

After some browsing around the web & looking for solutions, I used a mix of answers to come up with method of renaming previous commits. It's worth noting GitHub to [offer a way](https://help.github.com/articles/changing-author-info/) of doing this but in my case I didn't have any luck with it.

**Note** There are several methods of renaming previous commits & you must be error on the side of caution as your changing history (pretty cool, right?). The script below should not be using on public repositories. This worked perfectly for me as its only myself that commits to it, therefore I wouldn't be overriding anyone else's commit history.

<pre><code class="language-git">
git filter-branch -f --env-filter
"GIT_AUTHOR_NAME='newName';
GIT_AUTHOR_EMAIL='newEmail';
GIT_COMMITER_NAME='newName';
GIT_COMMITTER_EMAIL='newEmail';"
HEAD
</code></pre>

Once this has run successfully (you can check this by running 'git log' and press wq to exit the log). Run the following git command:

<pre><code class="language-git">
git push -f origin master
</code></pre>

Once you've pushed to your remote, double check the commit history and you should find that all your commits now have the correct author information.

You can also find the above script as a [gist](https://gist.github.com/imjamesdotme/8ca2281ad15f61037b41). The git ['Getting Started - First Time Git Setup'](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup) documentation is certainly worth a browse if you need a remind of all the various config options.
