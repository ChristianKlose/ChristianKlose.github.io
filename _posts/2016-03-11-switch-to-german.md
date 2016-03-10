---
layout: post
title: my311de - switching to Deutsch
excerpt: "Blog post to explain why i switch to german and where to find my articles in english..."
modified: 2016-03-11
comments: true
image:
  feature: sample-image-1.jpg
  credit: WeGraphics
  creditlink: http://wegraphics.net/downloads/free-ultimate-blurred-background-pack/
---

Coopto is a plug-in for VMware’s orchestration engine vRealize Orchestrator. It aims to provide full Docker functionality within the central automation component of the VMware stack in order to utilize and combine the power of container technology with virtualization technology. The combination of both can result in an even more powerful and flexible computation stack then possible with just one of the technologies.

# Short Intro

My colleague [Robert Szymczak](https://twitter.com/rszzy) created a Docker Plug-In for VMware vRealize Orchestrator which should help Administrators or Users to easily deploy and manage Docker Instances, Containers and Nodes on VMware Infrastructure.

The project is open source and is located on [GitHub](https://github.com/m451/coopto)  and there is also a [ReadMe](https://github.com/m451/coopto/blob/master/README.md) and a [Wiki](https://github.com/m451/coopto/wiki)  available.

You could also download it as a vRealize Orchestrator Package from VMware Solution Exchange [here](https://solutionexchange.vmware.com/store/products/coopto-a-docker-plug-in-for-vmware-vrealize-orchestrator--2).



# Install to Demo Environment


I have successfully installed the PlugIn and the Package File and i have a Docker Host on CoreOS running Server Version 1.4.1 with API Version 1.16.

But you can use any other OS or Docker distribution. Install instructions are available at [docker.com](https://docs.docker.com/installation/)

Check your version of Docker with
```bash
docker version
```

![Image of Docker Version](http://my311.de/images/2015-01-05-handson-coopto/05-01-_2015_16-12-19.png)

# Overview

In vRO Workflow Library you see the new menu Coopto which is structured into four sections

- Configuration
- Containers
- Images
- Sandbox

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-05-handson-coopto/05-01-_2015_16-22-12.png)

In *Configuration* you can Add and Remove Docker Nodes / Hosts. In *Containers* you can manage your Containers on the specified Node and on *Images* you can handle images from Dockerhub. *Sandbox* is a section to show you how you can predefine Applications using Docker Containers.

There are also some Actions coming with the Coopto Plug-In and the Coopto Package which are needed for the predefined Workflows and Sandbox Samples.

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-05-handson-coopto/05-01-_2015_16-54-42.png)

Let’s get started with adding a new Docker Node by simply starting ***Add Docker Node*** from the Configuration Section

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-05-handson-coopto/05-01-_2015_16-33-51.png)

After successful Workflow run check the vRO Inventory Tab and expand the Coopto Menu and select the Node you added before. The Status in the General Tab should be ONLINE!

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-05-handson-coopto/05-01-_2015_16-37-22.png)

As you can see in the screenshot the Node was added and it scans for existing Docker Images on that Host which are shown under the Host in the Inventory.

By simply running

``` bash
docker images
```
on the Docker Host you can double-check the downloaded Images.

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-05-handson-coopto/05-01-_2015_16-46-18.png)

# Use case / Example
As an quick and easy test we use one of the prepared Workflows Create Web SSH Console in the Sandbox Section coming with the Plug-In.

Let’s asume we did not have access to a SSH Client but we wanted to connect to a Linux Host. Therefore we can use wetty, a web based SSH console which is based on ChromeOS’ terminal emulator (hterm). You’re wright – this only works with a Chrome Browser :-)

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-05-handson-coopto/05-01-_2015_17-09-37.png)


After successfull workflow run switch to the Logs tab and copy the URL highlighted in the screenshot and paste it to a Chrome Webbrowser

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-05-handson-coopto/05-01-_2015_17-12-26.png)


et voilà – we have a connection to the Linux Host.

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-05-handson-coopto/05-01-_2015_17-16-25.png)

That’s it as a first review of Coopto Docker Plug-In for VMware vRealize Orchestrator.

More Information about Coopto integration into VMware Environment like vSphere WebClient and especially vRealize Automation is coming soon…
