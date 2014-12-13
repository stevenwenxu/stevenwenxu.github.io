---
layout: post
title: Setting up an Apache Server
categories: [tech]
tags: []
published: True
---

We are all mesmerized when we put an *index.html* file in the */var/www* directory and then get a static page running on localhost, but that's not everything. How do you install multiple sites with some awesome local names like *http://blog.dev*, or *http://sxu.local*.? It's time to say goodbye to http://localhost/site1, http://localhost/site2 etc.

Here are some practices I learned from my first Co-op work term as a web developer.

1. Put all sites in other directories, and make symlinks to */var/www*.
2. Edit hostfile and configure Apache Server with VirtualDocumentRoot.

In this way, the /var/www directory is kept easier to manage. If you have a newer version of the site, but you don't want to delete the old one or set up a new domain name, just point the symlink to that new place and you are good to go. It also saves time and disk space, because you don't have to copy files over.

By editing your hostfile and configuring VirutalDocumentRoot, you can get whatever local domain you want, and keep a cleaner url to visit. 


### Symlinks

1. Create a directory under root (e.g. /web)
2. Use git, svn, or copy the site to /web (e.g. /web/site1, /web/site2)
3. Make symlinks to /var/www like this:

{% highlight bash %}
sudo ln -s /web/steven-xu94.github.io /var/www/sxu
{% endhighlight %}

The bash `ls -hl` command gives a fairly human readable format for symlinks, look at these awesome arrows:

{% highlight text %}
vagrant@precise64:/web/blog$ ls -hl /var/www
total 8.0K
lrwxrwxrwx  1 root root   11 Nov 29 16:48 canvas -> /web/canvas
lrwxrwxrwx  1 root root   23 Nov 29 02:56 html5 -> /web/presentation_html5
lrwxrwxrwx  1 root root   27 Nov 27 02:48 sxu -> /web/steven-xu94.github.io
{% endhighlight %}


### Configuring Apache Server

File: /etc/apache2/sites-enabled/000-default

Normally you would add a `Directory` block in your apache conf file for each site:

{% highlight apache %}
<VirtualHost *:80>
   ...

   <Directory /var/www/blog>
      Options Indexes FollowSymLinks
      AllowOverride None
      Order allow,deny
      allow from all
   </Directory>

   ...
</VirtualHost>
{% endhighlight %}

But then you will need to edit it and restart Apache every time you add a new site, which is very tedious. That's where `VirtualDocumentRoot` comes. Here is my apache configuration file:

{% highlight apache %}
<VirtualHost *:80>
   ServerAdmin steven.xu13@gmail.com

   VirtualDocumentRoot /var/www/%1

   ServerName *.dev
   ServerAlias *.dev
   ErrorLog ${APACHE_LOG_DIR}/error.log

   LogLevel debug

   CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>
{% endhighlight %}

Note on the 3rd line that it's using VirualDocumentRoot. The `%1` is a parameter, it takes the value of the directory name, and appends it with the `ServerName`. So for example, if there is a directory */var/www/blog*, then I can just use http://blog.dev.

Restart apache2 and you are good to go. If you encountered any errors, it might be because the `vhost_alias` module is not enabled. To fix this, run

{% highlight bash %}
sudo a2enmod vhost_alias
{% endhighlight %}

and try again.

### Editing host file

The host file acts like a local DNS service which maps a domain name to an IP address. It has higher priority than your real DNS service provider.

Since I'm using a Vagrantbox and it has a host-only IP, I can add entries on my host machine like this:

{% highlight text %}
192.168.33.10 sxu.dev
192.168.33.10 canvas.dev
192.168.33.10 html5.dev
{% endhighlight %}

Every time when my browser hits "http://sxu.dev", it will first check if there is an entry in my host file - and there is, so it will *resolve* the url to the ip 192.168.33.10, which is my Vagrantbox. There, the rest is handled by the Apache server we just configured - it will grab the domain name before the `ServerName` *\*.dev*, which is *sxu*, and hit on */var/www/sxu* which is a symlink to */web/steven-xu94.github.io*.