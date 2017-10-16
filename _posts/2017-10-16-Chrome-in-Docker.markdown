---
layout: post
comments: true
title: "Install Google Chrome inside Docker on Ubuntu 16.04 LTS"
date: 2017-10-16
---

Google Chrome is a great browser with a huge number of plug-in. I think I dont need to advertise more for Chrome since it already has a huge popularity nowadays. 

Last week, one question raised from my head "How can I install and use Google Chrome browser via Docker?" and this question got stuck inside me for a quite time. Let me explain my scenario a little bit about the reason of this question.

1. I want to have the second Chrome installed in my computer. Searching around does not give me any positive results.

2. I want to have the safe browsing. Some examples are testing new interesting plug-ins of Chrome or checking some websites.

All of the requirements are satisfied by Docker but running GUI apps via Docker is quite tough task. After searching around, I have found the [instruction of Jessie Frazelle](https://blog.jessfraz.com/post/docker-containers-on-the-desktop/). She created some Dockerfile for the easy of using Chrome via Docker. I follow her guide with some modification to be able to run in my computer.

**TL;DR:** Install image using her Dockerfile and run 

```
docker run -it --net host --cpuset-cpus 0  -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY -v $HOME/Downloads:/root/Downloads --name chrome --cap-add=SYS_ADMIN jess/chrome
```

Below are step by step guide and some explanation

1. Pull her Dockerfile and create and image in our machine ```docker pull jess/chrome```.

2. Run the docker run command above to open Chrome. Notice that I have changed some arguments from the original recommendation of Jessie.
  - To overcome the error ```Failed to move to new namespace: PID namespaces supported, Network namespace supported, but failed: errno = Operation not permitted```, we need to add ```--cap-add=SYS_ADMIN``` to assign some admin capacities for docker containers to control the host machine. There are a [little documents](https://docs.docker.com/engine/reference/run/#pid-settings-pid) about this docker option. I am not sure if it makes any harms for the host machine but from [the discussion here](https://serverfault.com/questions/824809/chrome-under-docker-cap-sys-admin-vs-privileged), we can trust this option over ```--privileged``` one. 
  - I use ```-e DISPLAY``` instead of ```-e DISPLAY=unix$DISPLAY ``` since docker is intelligent enough to automatically select our current display and make use. In her setting, the ```unix$DISPLAY``` is a little bit unique for her computer. To check the X display, you can use ```xauth list``` to see if it matches the default setting. If not match, we usually get the error 
  
  ```
  No protocol specified

  (google-chrome:1): Gtk-WARNING **: cannot open display: unix:0
  ```

That is all. Hura, now we can use the second Chrome in our computer within docker.
