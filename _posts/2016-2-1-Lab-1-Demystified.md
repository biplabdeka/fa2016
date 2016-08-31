---
layout: default
title: "Lab 1: Demystified"
<!-- permalink: lab1.html -->
---

The [first lab](https://uiuc-web-programming.github.io/fa2016/Lab-1) required you to go through a variety of steps and processes to get you ready for MP1. But you might be asking, “_why did we do all of those things?_” Well, I'm glad you asked, handsome stranger.

First of all, let's define a stack. From Webopedia:

*“The term used to refer to software stacks in Web development environments. The stack of software, mainly comprised of open source software, will contain an operating system, web server, database server, and programming languages. One of the most most well-known web stacks is LAMP.”*

In this class, we'll use the MEAN stack, but we'll get to that later. For now, we're primarily dealing with a server (your Digital Ocean instance or your VirtualBox VM), and the web files (HTML, SASS, JS).

<span class="section-heading">What is VirtualBox, and what is Vagrant?</span>

<img src="https://upload.wikimedia.org/wikipedia/commons/8/87/Vagrant.png" class="demystified-images">

Vagrant is a tool that can build complete development environments without hassle. It reduces setup time and creates a development environment for everybody. As Vagrant claims:

*“Say goodbye to the "works on my machine" excuse as Vagrant creates identical development environments for everyone on your team.”*

So Vagrant needs VirtualBox, which can create a Virtual Machine for you. Vagrant does all the weightlifting of setting up and booting that machine for you when you use the command:

```bash
vagrant up
```


So now typing this command in the same folder as the Vagrant file tells Vagrant to start your machine on VirtualBox. Where are the VirtualBox instances? On your local machine! In fact, you go to the VirtualBox program you installed to find the exact location for where it is stored. And when you start the VirtualBox, it boots it up on ```localhost```. Pretty cool, huh?

Now, we can get into the machine with:

```bash
vagrant ssh
```


Once inside the machine, you are inside a folder that is very inconveniently named vagrant. For the purpose of this class, we want to instead go the folder ```/vagrant```, which is at the very base directory of the VM. Inside that folder, you'll notice that all the files that you pulled onto your local machine are also on this VM. That's because Vagrant has designed the system such that the files in this folder are synced between your local machine and this VM, so it doesn't matter where you modify the files.

Next, we have you run the install script titled ```install.sh```. Feel free to check out the script yourself. The script is a bash script that does the following:

1. Updates your VM with the latest linux packages
2. Installs Git
3. Installs other utilities
4. Installs NVM, which installs Node and NPM (Node Package Manager)
5. Installs Bower, the frontend package manager
6. Installs Grunt, the automated task runner
7. Installs Yeoman, the scaffolding app
8. Installs Gulp, which allows live-reloading of your webpage when you make changes
9. Installs Mongo, for future MPs where we use a database
10. Installs Ruby (if your installation takes a long time, this is the main reason why)
11. Installs Bundler
12. Installs Foundation, a front-end framework
13. Installs Compass
14. Installs Susy
15. Installs the MeanJS Yeoman Generator

**So *why* did we do all of this?**

As a class, we have to ensure that everyone has a similar development environment and experience so that when working on the MP's, _we don't have compatibility problems across multiple machines,_ along with a lot of other individual issues. Instead, creating this VM with Vagrant makes the process easy for starting up a VM, and the install script installs the exact same things for every single user.

<span class="section-heading">MP1</span>

So now, we clone the mp1 starter kit. Let's take a look inside the files:

**Node**

<img src="http://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2015/07/1436439824nodejs-logo.png" class="demystified-images">

So what's Node? Basically, some genius named Ryan Dahl had the idea to take Google Chrome's V8 engine, an event loop, and a low-level I/O API to create an incredible piece of server software that is available to the front-end developer. Essentially, NodeJS is a server-side program written for JavaScript. The file ```app.js``` has the code to run this app on port 3000. This project also uses a middleware called Express, which provides a set of features for web applications. Basically, Node and Express let you have a server. In our case, this server runs on port 3000 and serves things in our ```/public``` directory.

**NPM**

<img src="https://www.npmjs.com/static/images/npm-logo.svg" class="demystified-images">

The basic node.js installation can be extended to have a variety of functionality with hundreds of open-source packages that are available. Rather than installing these ourselves, we let NPM, the Node Package Manager, do the work. The cool thing is NPM lets us install packages locally for a project - meaning we only install those packages that we need for a project. We also don't have to commit all this packages to our Github repos for each project. We only commit their names in the ```package.json``` file. When someone clones our project and uses NPM, NPM will know exactly which packages our project depends on and will install it for us when we use the  ```npm install```  command. Once you do that, you'll see a folder called ```node_modules```, which has all of those packages.

**Bower**

<img src="http://bower.io/img/bower-logo.png" class="demystified-images">

Bower works in the same way as NPM, but instead, is for front-end libraries. What are front-end libraries you ask? Well its all the Javascript files that your webpage will try to load in the browser. For example, the ever so popular, jQuery. Bower reads from a file called ```bower.json``` , and installs packages into ```public/lib```, when you run the command ```bower install```.  To make those Javascript files available on your webpage you'll have to include them in your ```index.html``` document.

**Sass**

<img src="http://sass-lang.com/assets/img/styleguide/color-1c4aab2b.png" class="demystified-images">

CSS is what adds style to your website. HTML, by itself, has a set of default styles that look terrible, so CSS adds some color and life to your webpage. However, CSS is not without its faults. It doesn't have variables so everything is provided as a literal value, code looks messy and repetitive, and there is no logic.  That's where SASS comes into play. SASS provides variables, logic, and nesting, along with a variety of other features. If you're new to web development, give CSS a try and then convert that code into SASS. You are required to have certain SASS features for your MP.

However, the web browser can't read SASS, so how does that work? Well, SASS has to be manually compiled every time to convert the file into CSS. A piece of software called Compass, watches your SASS files and converts them into CSS files. In MP1, Compass takes your files in SASS in the ```source_sass``` folder and compiles them into the ```public/css``` folder. **Do not work AT ALL in the ```public/css``` folder, because your work will be overwritten!**

**Grunt**

<img src="http://www.dancourse.co.uk/wp-content/uploads/2014/03/grunt-logo.png" class="demystified-images">

A way to automate and speed up our web development process is by using something called Grunt. Grunt has a ```Gruntfile.js``` , which lists a set of tasks that should be automated. So what tasks are automated?

1. First, as discussed above, SASS is automagically compiled into CSS with Compass.
2. Second, any changes made to your source files automatically reloads the web page and displays the changes using *livereload*.
3. Third, your files in ```source_js``` are 'uglified' into Javascript files in ```public/js```. We do this because page load time is very, very important in web development, and uglifying your Javascript code decreases the load time of your Javascript files by putting all your code into a single line and simplifying the variable names.

Time for a moment of déjà vu. **Do not work AT ALL in the ```public/js``` folder, because your work will be overwritten.**

We hope that clarifies things for you. As the MP approaches the deadline, we suggest that you sketch out the design and features of your website on a piece of paper, so that you have a sense of how your MP1 design is going to look. Be mindful of the tips and rules for the MP and tutorials on how to code in web technologies in pinned Piazza posts.

Good luck!

*Note: If anyone would like to help improve or modify parts of this article, feel free to send the staff a pull request on our [github](https://github.com/uiuc-web-programming/sp2016)*
