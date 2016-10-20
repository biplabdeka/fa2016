---
layout: default
title: "MP 4 Demystified"
<!— permalink: lab1.html -->
---

In <a href="http://uiuc-web-programming.github.io/sp2016/MP-4" target="_blank">MP4</a>, we are asking you to do two things: create a RESTful API and consume it with a front-end. Hopefully in the next page or so, I’ll clear up some confusion around what goes into creating/consuming an API, and how the technologies we’re using help us do this.

Just a quick note before we dive into the details, this blog post will be split into two parts: High Level Thinking and Technologies. The high level will explain the overall thinking behind this MP, and the technologies will talk about the specifics behind the frameworks & libraries we are using.

<span class="section-heading">High Level Thinking</span>

Think of this MP as 3 layers interacting with each other: <b>the layer that holds the data (database), the layer that lets us consume that data (the API), and the layer that consumes that data (the front-end)</b>. 

- <b>Layer 1</b>: The database simply needs to hold our data. MongoDB/mlab will take care of this and this isn’t CS411, so I won’t say too much about this. 

- <b>Layer 2</b>: The API needs to be able to pull data from the database, and make it available to anybody with an internet connection (aka HTTP). This is the meat of the API implementation, and will probably be the part that cause the most confusion. More on how we do this later.

- <b>Layer 3</b>: The front end you already have experience with. The only difference is that the data you’re consuming isn’t from a local JSON file, but from an API (either yours or the one we have provided).

<img style="height: 100px; width: auto" class="demystified-images" src="http://findicons.com/files/icons/346/sweet/128/cake1.png">

You could think of these layers as stacks of cake! This is sort of where the term “Full-stack Developer” comes from — a person who works with both the back-end and front-end, and ensures they work together perfectly. The official definition of a "stack" was discussed in <a href="http://uiuc-web-programming.github.io/sp2016/Lab-1-Demystified" target="_blank">Lab 1 Demystified</a> by Sujay.

<span class="section-heading">Technologies</span>

Now that we have the high level taken care of, we can drill down to the specifics and start outlining what technologies we’ll use and why we’re using them. 

In this MP, we are going to be using something called the MEAN stack (some of you might already be familiar with it). The MEAN stack is made up of four different technologies: <u>M</u>ongoose, <u>E</u>xpress, <u>A</u>ngular, and <u>N</u>odeJS. To make explaining and understanding the stack a little easier, I’m going to describe the technologies out of order: instead of the MEAN stack, I’m going to be talking about the NAME stack.

First, what we already know: 

 
**Node** 

<img src="http://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2015/07/1436439824nodejs-logo.png" class="demystified-images">

We already talked about this. Node is basically JS outside of the browser. For more see <a target="_blank" href="http://uiuc-web-programming.github.io/sp2016/Lab-1-Demystified">here</a>.

**AngularJS**

<img style="width: 100px;" src="https://camo.githubusercontent.com/6795c053f2fafee4d1c76f3a181876013827dd5e/68747470733a2f2f662e636c6f75642e6769746875622e636f6d2f6173736574732f333437303430322f313230383630372f32376637643134322d323564362d313165332d386330372d6139316532633736396435322e706e67" class="demystified-images">

This is Layer 3. You should already be familiar with this from working on MP3. We are asking you to do something very similar for MP4. See <a target="_blank" href="http://uiuc-web-programming.github.io/sp2016/MP-3-Demystified">here</a> if you want to read more about Angular.

Now to the unfamiliar. Remember with these last two technologies, we want to be able to fill in Layers 1 and 2. More specifically, we want some way of (1) pulling data from a database and then (2) making that data available over HTTP.

**Mongoose**

<img src="http://mongodb-tools.com/img/mongoose.png" class="demystified-images">

This is what we’re going to use to do that part (1) . Mongoose will let us point to a Mongo database somewhere using:

~~~
mongoose.connect('mongodb://localhost/mp4');
~~~
<br>
After connecting, we can access that data with vanilla Javascript like so:

~~~
User.findByID(id, function(err, user){ ... });
~~~
<br>

To do this, we need to define simple schemas (like User) that define our data, and then use the functions Mongoose provides (like findById) to access that data. For more on this, see the <a href="http://mongoosejs.com/docs/guide.html" target="_blank">docs</a>. Again, you are not doing anything fancy here. <b>All you should do is use some predefined functions that spit data from your database back at you.</b> Afer you might need to do some processing on that data, but that’s it.

**Express**

<img src="https://i.cloudup.com/zfY6lL7eFa-3000x3000.png" class="demystified-images">

Express takes care of part (2) from above. It will create endpoints that anybody can call and grab data from. Don’t worry about the nuts and bolts about how Express works. Just know that you create some Javscript functions (what happens in these functions is up to you) and define some endpoints (GET, POST, etc.), and Express will take care of hooking everything together. For example, creating a simple route looks something like this:

We define a new endpoint in separate module.

~~~
// llama.js
module.exports = function(router) {
    //Llama route
    var llamaRoute = router.route('/llamas');

    llamaRoute.get(function(req, res) {
      res.json([{ "name": "alice", "height": 12 }, { "name": "jane", "height": 13 }]);
    });

    return router;
}
~~~

In some other file, we've instantiated our router instance. We require the module where we've defined our logic for our endpoint. We pass our router instance as an argument to that module. 

~~~
    // server.js
    var express = require('express');
    var router = express.Router();
    
    // tell our app to use this route
    app.use('/api', require('./llama.js')(router));
~~~

Our endpoint can now be reached at: 
~~~
/api/llamas
~~~

 The docs are <a href="http://expressjs.com/en/api.html" target="_blank">here</a>.
 The docs are <a href="http://expressjs.com/en/api.html" target="_blank">here</a>.

<span class="section-heading">Wrap Up</span>

This should clear up a lot of confusion surrounding what the heck we’re doing in this MP. Technically and theoretically, this MP is the most complex and the most involved, so please start early and work often. Good news is at the end of all this, you’ll be able to officially call yourself a Full-stack Developer!

Good luck!

