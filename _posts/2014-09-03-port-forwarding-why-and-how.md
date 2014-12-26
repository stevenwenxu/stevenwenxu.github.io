---
layout: post
title: Port forwarding&#58; why and how
categories: [tech]
language: English
tags: []
published: True
---

If your team has a retired super computer (like a Mac Pro 2009), it could be used as a dedicated server for virtual machines. I'm sure you are like me who prefer running your VM on a server with 8-core Xeon cpu + 16GB RAM, rather than on your laptop which probably already has 90% resources in use.

It is often true that IPs are valueble and restricted resources in companies with large number of employees, therefore your devices that come from no where (like a VM) are not recognized by the IT department and don't get a IP within the same subnet over a bridged network.

This guide assumes that your VM only has a host-only ip (e.g. 192.168.56.101) which is unique to the Mac Pro, meaning you can't ping it directly from your host mac.

For web development, the goal here is to access the websites inside your VM from your host machine.

A sample setup:

{% highlight text %}
|            |         |             |          |                |
| your mac   | connect |   Mac Pro   | runs on  |   vagrant VM   |
| 10.0.28.10 | ------> | 10.0.28.173 | <------  | 192.168.56.101 |
|            |         |             |          |                |
{% endhighlight %}

### What is a port?

A port is like a door of a system. Sometimes you need to visit a particular door to enter certain places. 

e.g. an http website uses port 80 on the server.
When you visit http://www.google.com, your browser is visiting port 80 on a machine that hosts the google site.

Some common ports: \\
21: FTP \\
22: SSH \\
23: Telnet \\
80: HTTP \\
443: HTTPS 

### Why port forwarding?

If you had a browser inside the VM, you could just visit http://site.local with that browser. However, I am using ssh to log onto my VM, and also I want to use the browser installed on the host (my local mac) to visit the site inside the VM. The magic is to **forward** the port 80/443 on the VM to my host computer, so I don't have to visit the ports of the machine I don't have direct access, but visit localhost on a particular port.

SSH itself provides port forwarding, making it a lot simpler than tweaking the Vagrantfile or virtualbox settings, especially in a situation like this.

### Let's do this

1. Find out all IPs

   Run `ipconfig` on the 3 machines, and take note of the IPs.

2. Run the command

{% highlight bash %}
ssh user@10.0.28.173 -L 8080:192.168.56.101:80 -L 8081:192.168.56.101:443
{% endhighlight %}

\3. Done!
   Visit http://localhost:8080 on your local mac. (or visit an awesome local domain if you followed my [previous post](/blog{% post_url 2014-09-01-setting-up-an-apache-server %}))

### Understand the command

The -L command makes port forwarding requests.

#### breaking it apart

{% highlight text %}
ssh user@10.0.28.173    -L 8080:    192.168.56.101:80
---------------------   ---------   ------------------
        (1)                (2)            (3)
{% endhighlight %}

(1) That's how you normally ssh into the Mac Pro.

(2) port 8080 refers to the port on <u>the machin that you type this ssh command</u>, so in this case, your local mac.

(3) 192.168.56.101 refers to an IP that <u>the machine you are ssh-ing can visit</u>. The port followed refers the port on that machine. In this case, 192.168.56.101 can only be visited by 10.0.28.173 which just fits our needs.

(as a whole) 
We are telling ssh to: 
1. Log in to 10.0.28.173
2. Find 192.168.56.101
3. Take its 80 port and map it to the 8080 port on my machine.

#### Extending the command

As you can see, you can add multiple -L options to one single ssh connection, so as your project goes, eventually your command end up like this:

{% highlight bash %}
sudo ssh wxu@10.0.28.173 -L 80:192.168.56.101:80 -L 443:192.168.56.101:443 -L 8095:192.168.56.101:8095 -L 8082:192.168.56.101:8080 -L 8083:192.168.56.101:8081 -L 8181:192.168.56.101:8181 -L 2201:192.168.56.101:22 -L 8090:192.168.56.101:8090 -L 8443:192.168.56.101:8443 -L 3366:192.168.56.101:3306
# format: inside to outside
# 80   to 8080 is for http
# 443  to 8081 is for https
# 8095 to 8095 is for Crowd server
# 8080 to 8082 is for Jenkins server
# 8081 to 8083 is for Jira
# 8181 to 8181 is for google site map generator
# 22   to 2201 is for sshfs (macfusion)
# 8090 to 8090 is for Confluence
# 8443 to 8443 is for Jira https
# 3306 to 3366 is for mysql
{% endhighlight %}

Put this block of code inside a file called "connect", give it execute permission (`chmod u+x connect`), and you have a bash script that saves tons of typing!

{% highlight bash %}
./connect
# Actually, ./c[tab] --> four keystrokes make your life a lot easier
{% endhighlight %}

#### Why don't you port forward the same port (why not 80 to 80?)
That's because port under 1024 are considered "privileged". Read: [Why are ports below 1024 privileged?](http://stackoverflow.com/questions/10182798/why-are-ports-below-1024-privileged). If you would like to map to that area, you will need to execute that command with root: `sudo ./connect`. The goal here is to *type less*, I don't want to type the sudo password every time.