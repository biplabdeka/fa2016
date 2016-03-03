---
layout: default
title: "MP 3 Demystified"
<!-- permalink: lab1.html -->
---

Welcome to AngularJS! Time to delve into one of most powerful frontend frameworks in the world. Your goal again for this MP is to get your feet wet with Angular before we get into MP4, which has both a frontend and backend component.

<span class="section-heading">Why Angular?<span>

It's designed for declaring dynamic views in web-applications, it's extremely powerful, and it's backed and supported by Google. It's also very widely used so StackOverflow should be your friend for debugging.

<b>However, </b> Angular can be tricky to debug and weird to learn at first glance. When debugging, most of our experiences in this class and with using Angular have taught us that <u>weird errors often occur with misspelling variable names and/or not using exact Angular syntax</u>. So definitely double check those before posting to Piazza or checking StackOverflow to save you some time. Just for reference, we are using Angular version 1.3.13. As far syntax goes, here are some useful things to know for this MP:

<span class="section-heading">ng-app<span>

In Angular, you need to define a module to get started on your app.

~~~
var app = angular.module('myFirstAngularApp',['ngRoute']);
~~~

This is the initial declaration of our app and everything we do will be modifying the app through dot notation (.config, .controller, etc). The `ngRoute` is there loaded in as a dependency that we will use later for routing.

The accompanying HTML inserts the name we declared (myFirstAngularApp) into the HTML markup.

~~~html
<body ng-app="myFirstAngularApp">
~~~

Usually, the ng-app directive is placed in the body or html tag of the page so that it can encompass all of the HTML markup.

<span class="section-heading">ng-controller<span>

Now, we want to define a controller where we can declare some code to work on displaying the code to the frontend. A basic controller definition is done like this:

~~~js
app.controller('myFirstController', ['$scope',  function($scope) {
    $scope.myFirstVariable = ""
}]);
~~~
<br>

The controller is appended to the overall Angular app, has a name (myFirstController), and it is passed in the $scope variable into the array and as a parameter in the callback function. The $scope variable is something that Angular gives us so that we can control aspects of the data model that we share with the HTML markup of the application. The `$scope.myFirstVariable` declaration creates the variable in that controller's scope and that variable can be accessed in the HTML, and the same can be done for functions. Declaring variables or functions in the standard JS manner without making them a part of the $scope Object will not make them available in the markup.

Here is the accompanying HTML:

~~~
<div ng-controller="myFirstController">
\{\{myFirstVariable\}\}
</div>
~~~

The location of the ng-controller directive should be based in the topmost HTML tag you want the controller to encompass. i.e. in the example above, the controller will encompass and cover everything inside the div. The `{{ }}` notation takes any variables that are attached to the $scope object and you can display them in the HTML markup.

NOTE: the ng-controller directive will be superfluous when we get to routing.

<span class="section-heading">$http<span>

When working with this MP, you'll need to retrieve some data in a JSON format. Thankfully, we have already crawled the data for you, and it should be located in the `public/data` folder. Inside your controller, you can use the $http Angular variable to get that data:

~~~
$http.get('/someUrl').
  success(function(data) {
  }).
  error(function(err) {
  });
~~~
<br>

<span class="section-heading">ngRoute<span>

Now, we will have three separate views in this application. To manage those views with routes, Angular can make setup very easy. In the `index.html`, you'll have this line:

~~~
<div ng-view></div>
~~~
<br>
In short, whenever we request a particular partial from our `/partial` folder, Angular will take that partial's html and put inside this div and keep replacing it depending on the route requested. Your partials can be written as regular divs without anything extra.

Now to the JS:

~~~
app.config(function ($routeProvider) {
    $routeProvider
        .when('/', {
            templateUrl : 'partials/first.html',
            controller: 'myFirstController'
        })
        .otherwise({
            redirectTo: '/'
        });
})
~~~

This code allows you define a route name with `\` and then matches a partial and a controller with that route name. This means you don't need to explicitly declare the `ng-controller` in the HTML markup too in these partials since this takes care of it for us.

<span class="section-heading">Closing<span>

That should be enough to get you started! Be sure to refer to the spec whenever you need help in a particular area and keep checking up on the Angular documentation whenever you need it.
