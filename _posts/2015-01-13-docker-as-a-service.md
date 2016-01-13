---
layout: post
title: HandsOn: Docker-as-a-Service in vRealize Automation
excerpt: "With the availability of Coopto i wanted to show you how to Create a Service in vRealize Automation Center for Docker Containers."
modified: 2015-01-13
tags: [docker, handson, automation, orchestrator, devops]
comments: true
image:
  feature: sample-image-5.jpg
  credit: WeGraphics
  creditlink: http://wegraphics.net/downloads/free-ultimate-blurred-background-pack/
---

With the availability of Coopto - Docker Plug-in for vRealize Orchestrator in the VMware Solution Exchange (VSX) i wanted to show you how to Create a Service in vRealize Automation Center for Docker Containers.

# Short Intro

Last week i showed you in my post [HandsOn: Coopto – a Docker Plug-in for VMware vRealize Orchestrator](http://my311.de/post/2015-01-05-handson-coopto/) how to implement Coopto to your vRealize Orchestrator Environment.

Today my employer [Fritz & Macziol GmbH](http://www.fum.de/en/) uploaded Coopto to the VMware Solution Exchange where you could download it as a vRealize Orchestrator Plug-in [here](https://solutionexchange.vmware.com/store/products/coopto-a-docker-plug-in-for-vmware-vrealize-orchestrator--2).
Documentation and Wiki is still available on [GitHub](https://github.com/m451/coopto) but there is also a [UserGuide](https://solutionexchange.vmware.com/store/products/coopto-a-docker-plug-in-for-vmware-vrealize-orchestrator--2/files/20898) in PDF Format available for download.


## vRealize Automation Advanced Service Designer

I prepared my Lab Environment with the latest release of vRealize Automation 6.2.0-2299574 running builtin vRealize Orchestrator 6. To the Orchestrator part i installed the Coopto Plug-in from VMware Solution Exchange and i created a Docker Node/Host as described in my post [HandsOn: Coopto – a Docker Plug-in for VMware vRealize Orchestrator](http://my311.de/post/2015-01-05-handson-coopto/).

If everything is fine and running in vRealize Orchestrator let's start with the **Advanced Services** in vRealize Automation.

-----------

### Custom Resources
To manage Docker Containers through vRealize Automation we have to create a **Advanced Services > Custom Resource** with Orchestrator Type *Coopto:DockerContainer* which could be selected by only typing *coo*. Give it a Name like *DockerContainer* and some Description. For this demo i leave the Details From as it is but for a real scenario i would hide all fields which are not necessary to the user.

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0000.png)

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0001.png)

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0002.png)

### Service Blueprints
As a first Service Blueprint i wanted to add on of the prepared Coopto Workflows from the Sandbox folder in the Coopto Plug-in.
Start with **Advanced Services > Service Blueprints** and click **Add** to create a new Service.

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0004.png)

Browse the vRealize Orchestrator Library to **Library : Coopto : Sandbox** and Select the *Create Web SSH Console* Workflow.

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0005.png)

Give a Name, Description and maybe Version to the Blueprint.
I love the possibility to hide this ugly catalog request information page from the Service Request.

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0006.png)

As in the Custom Resource Form i keep all information in this Blueprint form which come from the Workflow.

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0008.png)

An important step is to bind the Output Parameter from the Workflow to a Provisioned Resource. Otherwise you did not receive any manageable Items in vRealize Automation.


### Catalog Management
For Coopto i created a *Services Group* in **Administration > Catalog Management > Services** and i linked the created Service Blueprint *Create Web SSH Console* to this Services Group. A nice new logo and then we can preview our new Service in the **Catalog** View.

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0013.png)

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0014.png)

### New Request
Let's request one container through vRealize Orchestrator and  we wanted to use this Container as a SSH Client to connect to a SSH Host with the *IP 10.111.6.212 Port 22* and *User root*.

You can give a Name to the Container which later also appears in the **Items list**.

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0015.png)

### Items
After a few seconds check the **Items List** for the Name given to the Container in the previous request.
Click on the Name to view the Details of this Item.

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0016.png)

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0017.png)

### New Resource Action : Remove Container
Now that we have created a Docker Container as Custom Resource managed by vRealize Automation we should create some Resource Actions specially for the management of Docker Container Items.

Go to **Advanced Services > Resource Actions** and Click *Add* to create a new Action.


![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0009.png)

Browse the vRealize Orchestrator Library to **Library : Coopto : Containers** and Select the *Remove Container* Workflow.

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0010.png)

Define the Resource type and the Input parameter to match with the Custom Resource created earlier.

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0011.png)
Keep the Name and Description and give a Version to the action. Don't forget to check *Hide catalog request information page* - if you want.
You can also check the Type : *Disposal* and as the Target criteria select *Always available*.

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0012.png)

Keep the form Elements and click **Add**.

### Resource Action : Get Connection in vRA

For some Applications in Docker Container it is helpfull to get the URL or Connection string.  Our example Service Container Web SSH Console to connect to a SSH Host creates such a connection string but unfortunately it is not redirected to the vRealize Automation Portal directly.

A Resource Action could be the solution ...

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0018.png)

Browse the vRealize Orchestrator Library to **Library : Coopto : Containers : vRA ** and Select the *Get Connection in vRA* Workflow.

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0019.png)

Map the Resource Action to the Custom Resource of the Docker Container.

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0020.png)

Give a Name, Description and Version...

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0021.png)

You can define Prefix and Postfix if you want and sometimes it make sense to remove or hide these fields.
In my example i normally would define *http://* as a Prefix but this is currently not in the Screenshots.

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0022.png)

You have to publish and configure the Actions to the Entitlement before they are visible to the Items Actions menue!

Select your Container for the *Web SSH Console* and Click **Actions > Get Connection in vRA**

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0023.png)

You don't have to define a Prefix or a Postfix as you don't need them in this example. Click **Next**.

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0024.png)

In this Output - Form you can see the link to my Docker Host and a Port which is mapped into the Container i created before. If i had configured a Prefix like http:// i could directly click on the URL to open the connection.
I have to copy the URL s00-lxc-01:49155 and paste it to a Chrome Browser...

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0025.png)

and again : it works
I'm now connected to the Container on my Docker Host which has created a SSH Connection to the ip i configure in my Request.

![Coopto - Docker Plugin for vRealize Orchestrator](http://my311.de/images/2015-01-13-docker-as-a-service/SNAG-0026.png)

Last step is to go back to my Items View, select my Container and remove it with the created Resource action.

I hope you have some fun with Coopto, vRealize Orchestrator and vRealize Automation.

Thanks to my colleague [Robert Szymczak](https://github.com/m451/coopto) who is the father of this Coopto "Baby" and thanks also to our employer [Fritz & Macziol](http://www.fum.de/en) for supporting this project!

If you are interested in vRealize Suite, Coopto or if you have an interesting Service in your company which should be implemented into vRealize Orchestrator or vRealize Automation - feel free to contact me.
