---
layout: default
title: "Lab 2: Demystified"
<!— permalink: lab1.html -->
---

The [second lab](http://uiuc-web-programming.github.io/sp2016/Lab-2/) is having you use Foundation, which may seem scary, since it's a wealth of information and resources to use, but we're here to help break it down for you.

<span class="section-heading">Why Foundation?</span>

<img src="http://foundation.zurb.com/assets/img/learn/training/intro.png" style="display:block; margin-left:auto; margin-right:auto;"/>

It's one of the most popular frameworks available, it's responsive, semantic, and easily customizable, and it has a lot of great plugins.

<i>So why not Bootstrap?</i> Bootstrap is cool too, but we'd like everyone to consistently use one framework, and, for this course, we've chosen Foundation. It has more built-in features than Bootstrap, a whole new upgrade to Foundation was made more recently than Bootstrap, and, aesthetically, we don't want people to fall into the front-end criticism of having their site look too "bootstrap"-y. Also, yes, Bootstrap 4 is coming. No, we don't want to experiment with the alpha release of a framework for a course.

<u>So let's get into some details about MP2:</u>

MP1 was a chance to get your feet wet with modern web dev. It focused a lot on implementation so that you can understand the fundamentals of HTML, CSS, and JS. However, there are some awesome frameworks that have written a lot of awesome CSS and JS for us, so let's now use that!

First, some ground rules. It was indeed possible for your MP1 to have some nonsense content (e.g. A simple button that said “Open the modal here” that opened your modal, which said “This is modal”). However, we definitely need your MP2 to have some sort of information architecture. This information could be fake or made-up, but the information has to all cohesively make sense. The whole point is to observe the larger idea of making a product, instead of just a collection of web documents that have certain features. If your MP1 had some information architecture, awesome! If not, you have a little extra work to do.

Part A of MP2 is to help you understand some neat concepts of designs that you could use for your website. To actually implement them, we look to Parts B & C. Keep in mind, <b>the requirements of features from MP1 (the modal, carousel, etc) are still required</b>. Here are some neat parts of Foundation that you may find useful:

<span class=“section-heading”>The Global Styles</span>

Inside the foundation6_lib folder, you'll find a handy file called _settings.scss. Foundation comes with a bunch of nice (global styles)[http://foundation.zurb.com/sites/docs/global.html]. But, you should obviously want to customize it. Simply enough, changing the values of the variables in _settings.scss lets you change certain styles and aspects without completely reinventing whatever they have already given you. You can also see all the original global styles in _global.scss.

<span class=“section-heading”>The Grid</span>

Time to make things responsive!

So here's a basic grid example where you would do multi-column for your content:


The surrounding div has the row class, which will apply the grid to any encapsulated divs. The inside divs have multiple classes applied to them like small-2 large-4. You have to apply multiple classes to account for different screen sizes.

The idea is that once your screen size hits a certain threshold, certain classes will be applied. From the site:

* Small: any screen.
* Medium: any screen 640 pixels or wider.
* Large: any screen 1024 pixels or wider.

So when you apply a large class, the amount of space you account for that div (in the case of large-4, four columns of space) only kicks in after the screen is larger than 1024 pixels. So the above code looks like this:

[Image: https://datadrivendesign.quip.com/-/blob/dCdAAA7Hrr6/W4uS6kt8IzS-zovz59nxFw]when the screen is larger than 1024 pixels. If it is smaller than that, it becomes:
[Image: https://datadrivendesign.quip.com/-/blob/dCdAAA7Hrr6/WZ1WTXoBnaRpXscFUCQ78g]Now, what happens if we don't apply a small class to the divs?
[Image: https://datadrivendesign.quip.com/-/blob/dCdAAA7Hrr6/6x7rZe7xFNiX8UmQgrzzdw]It just takes up the full width! That's why we must adhere to the Foundation principle that:

“Foundation is mobile-first. Code for small screens first, and larger devices will inherit those styles. Customize for larger screens as necessary.”

If you wish to customize the breakpoints, the column widths, or anything else, you can find those values in the _settings.scss file, although you generally shouldn't need to.

<span class=“section-heading”>Components</span>

Certain requirements from MP1 are now cake with the toolbox of resources that Foundation gives us. For example:

_Sticky Nav Bar:_
Add the sticky class and data-sticky to any component to make it stick to the top. Also, when your navigation bar adjusts to different viewports, you have either the option to make the menu items stack or become a hamburger icon. More details (here)[http://foundation.zurb.com/sites/docs/responsive-navigation.html]

_Modal_
Foundation takes care of the modal logic for you. Just declare it and customize it with Sass. More details (here)[http://foundation.zurb.com/sites/docs/reveal.html]

_Video_
Your videos can now be responsive too! Add flex-video as a class to the div. More details (here)[http://foundation.zurb.com/sites/docs/flex-video.html]

_Carousel_
The Orbital Slider is pretty neat (here)[http://foundation.zurb.com/sites/docs/orbit.html]. Foundation also recommends that a more robust carousel to use is (Owl Carousel)[http://owlgraphic.com/owlcarousel/].

<span class=“section-heading”>Wrap-up</span>

That's it for now! Read the full docs for the (full details)[http://foundation.zurb.com/sites/docs/]. The bottom of most sections have a nice Sass reference that you can look at when changing the appropriate Sass variables in your _settings.scss file.

Be sure again to do a quick Google check on any questions you may have before posting on Piazza. Chances are, some of the issues you'll have are addressed by the Foundation community through issues on their Github repo. Good luck!
