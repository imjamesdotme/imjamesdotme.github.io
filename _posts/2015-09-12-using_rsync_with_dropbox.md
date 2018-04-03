---
layout: post
title:  "Using rsync with Dropbox"
date:   2015-09-12 21:45:03
author: James L
categories: terminal rsync
image: /assets/using-rsync.jpg
imageAlt: Using rsync with Dropbox
---

I recently decieded to review my backup process and fortunately at the same time learnt about [rsync](http://linux.die.net/man/1/rsync) from a colleague. rsync is file transfer program that comes pre-installed on Ubuntu and can be used both locally & remotely.

The reason I wanted to try this with Dropbox is because after the initial backup (a few GB's in my case), I'd only be syncing small amounts of data at anyone time, keeping bandwidth & CPU usage low. Getting started with Dropbox is as simple as locating the path you want to back up (in my case my 'home' directory) and the path of the reciepent (in this case a Dropbox folder I had sync'd locally). The command below will copy everything from my home folder & place it into my ubuntu-home folder on Dropbox. rsync will make sure there are no differences between the files - if anything changes in my home folder (such as new files or deleted folders) it'll apply those changes to my folder in Dropbox.

The 'a' (archive) argument tells rsync to recurse into all directories and the 'v' stands for verbose (as with most commands) this outputs everything that's happening to the Terminal - this can be very useful to see if you have any issues. The delete argument 'delete' will remove anything in the second directory that isn't in the origin directory (effectively making sure the remote folder is mirrored). Finally --progress output the (you guessed it) progress of rsync to the terminal, this is very useful when syncing large amounts of data. There are a lot of other [rsync arguments](http://www.evbackup.com/support-commonly-used-rsync-arguments/) available.

<pre><code class="language-bash">
$ rsync -av --delete --progress /home/james/ /home/james/Dropbox/Backup/ubuntu-home/
</code></pre>

On a side note, there maybe folders or files you want to exclude from your directory, in my case I wanted to exclude my Dropbox & Videos folder from the backup. If you have a lot of directories you want to exclude then take a look at this [article](http://articles.slicehost.com/2007/10/10/rsync-exclude-files-and-folders). The command below includes the --exclude option. The rest of this post will continue without the exclude flags, just know they exist if you need them.

<pre><code class="language-bash">
$ rsync -av --delete --progress --exclude 'Dropbox' --exclude 'Videos' /home/james/ /home/james/Dropbox/Backup/ubuntu-home/
</code></pre>

Rather than typing out the above command each time I wanted it to run, I added it to a script file & then to my .bashrc file to easily run it from Terminal.

<pre><code class="language-bash">
#!/bin/bash
rsync -av --delete --progress /home/james/ /home/james/Dropbox/Backup/ubuntu-home/
</code></pre>

To do this, go to your favourite text edit and paste the above command (with your own paths) and then save the file with the extension .sh (.sh files are shell scripts you can run from the Terminal), I save my scripts into a 'Scripts' folder in my home folder so they're easy to locate. You can now drag & drop that file onto a Terminal window, hit enter and rsync will start up.

If you want to be able to run a command from the Terminal (without having to drag & drop it each time) for your new script to execute you can add it your .bashrc file but first you'll need to make sure your script is executable. In the Terminal type in 'chmod +x' then drag & drop your script into the window for Terminal to add it's path. Press enter & your script is now executable.

<pre><code class="language-bash">
$ chmod +x /home/james/Scripts/rsync-dropbox.sh
</code></pre>

First of all navigate to your home folder & press CRTL + H (on Ubuntu) which reveals hidden files and look for a file named bash.rc. At the bottom of the file add in comment (always useful in case you don't return for a while) and then give your script an alias in my case it was 'backup-db' and then the path to your script.

<pre><code class="language-bash">
# Backup home folder to Dropbox with rsync
alias backup-db='/home/james/Scripts/rsync-dropbox.sh'
</code></pre>

Now when your run 'backup-db' (or whatever your alias is called) in Terminal, your script will trigger & your rync session will start running!

You've now got a simple method of backing everything up to Dropbox with a single command & it should be lighter on bandwidth & processing power as you should be syncing smaller amounts of data. This could also be extended by adding it as a CRON job.

### Notes
When I originally started out using rysnc with Dropbox I ran into two note worth issues.

*Dropbox* is limited from monitoring more than 10000 folders on linux, this was causing me an issue. The Dropbox app did offer to fix it but that didn't resolve the issue. You can fix it manually using the the code below;

<pre><code class="language-bash">sudo sysctl fs.inotify.max_user_watches=100000</code></pre>

To make the limit permanent you can edit the file /etc/sysctl.conf and add the same command, but without _sudo_. You can find out more about this issue [here](https://www.dropbox.com/help/145).

Finally I ran into an issue with symlinks. One of the directories in my home folder contained several projects that are using Gulp and accompanying node modules, there were a vast number of symlinks in the node modules pointing back to my local file system. It turns out that Dropbox really doesn't like symlinks, therefore this was causing me some sync headaches. If you want to check your Dropbox for symlink you can use the command below; It's advisable to remove all symlinks to avoid issues. It's also worth noting that I found symlinks inside some hidden directories from applications such as Atom - just be cautious and when it double check with the command below.

<pre><code class="language-bash">find ~/Dropbox -type l -exec ls -lah {} \;</code></pre>
