---
layout: post
title:  "Linux Permissions"
date:   2019-12-25 06:20:00 +0700
categories: ['linux']
---

In Linux, every file and every directory has a permission list. These permissions divided to
3 sections as users, groups and others. In this post we'll talk about them.

{% highlight ruby %}
id
{% endhighlight %}
When you write this code to the terminal you should see uid ve gid numbers that created for you.
uid means user identifier which is unique for every user on the other hand gid is the group
identifier. Every user has its own group. So your own user group is created when you did
create your user.

There are three types of permissions. Read, write and execute. However, these permissions
have different meanings depends on if it is a directory or file.

Read: For file it means, the file can be opened and read. For directory, the files inside of
the directory can be listed.
Write: For file, you can overwrite or edit the file but you cannot rename or delete the file.
To do those, you gotta look at the directory permissions that the file belongs to.
So for directory, it allows you can rename, delete or create new files inside the directory.
Execute: For files, the file can be executable, for directory you can enter the directory.

You can read the permissions by writing ls -l to the terminal.

{% highlight ruby %}
drwxr-x--- // it is a directory. The owner can do everything. The group owner cannot write.
           // others cannot do anything
{% endhighlight %}

How to change the permissions? With chmod.

{% highlight ruby %}
chmod 760 file // 7 means rwx, 6 means rw-, 0 means ---
               // so it is -rwxrw----
chmod u+x files // add executable to the owner

chown bob:clones directory // this makes the owner bob, the group clones
chown bob:  // the owner bob, the group bob's group
{% endhighlight %}

