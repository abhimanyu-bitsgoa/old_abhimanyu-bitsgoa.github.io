---
layout: post
title:  "1111"
desc: "我的第一篇jekyll博客"
keywords: "jekyll,blog,first"
date: 2015-01-08
categories: [Life]
tags: [blog]
icon: fa-bookmark-o
---

So we have previously seen how Davide, Alessandro and I designed the [Rating Engine](https://keenlearner.wordpress.com/2016/07/25/weve-come-a-long-way-from-where-we-began/) for our  **[WikiRating:Google Summer of Code](https://github.com/WikiToLearn/WikiRating)**project. Now this is the time for our last step , that is to connect the engine to the Website for displaying the computed results and for providing voting functionality to WikiToLearn users. In MediaWiki additional functionalities like this are added via [extensions](https://www.mediawiki.org/wiki/Manual:Extensions). You can think of extensions in the literal sense too as something that provides some extension points on the top of the current code base. This make the life of developers easier since by using extensions we can add new code in a modular fashion and thereby not much fiddling with the Wiki code base. So now I needed to write an extension that can the following:

*   Fetch the information about the page being viewed by the user.
*   Allowing the user to vote for the page.
*   Displaying additional information about the page is user demands.

So with the following things in mind I began to analyse the basic components of a MediaWiki Extension. ![extension_components](https://keenlearner.files.wordpress.com/2016/08/extension_components1.png) So besides the [boiler plate](https://www.mediawiki.org/wiki/Manual:Developing_extensions) components that required minor tweaking **extension.json , modules , specials **are of our interest.

# extension.json

![extension_JSON](https://keenlearner.files.wordpress.com/2016/08/extension_json.png) This JSON file stores the setup instructions for instance name of the extension, the author, what all classes to load etc.

# modules

![module_pic](https://keenlearner.files.wordpress.com/2016/08/module_pic.png) The module folder of our [WikiRating Extension](https://github.com/WikiToLearn/WikiRatingExtension) contains these 2 components:

*   **resources**: where all the images and other resources are stored.
*   **wikiRating.js**: A java script file to fetch, send and display data between the engine and the Website instance.

It is the wikiRating.js script where we wrote most of our code.

# specials

![specials](https://keenlearner.files.wordpress.com/2016/08/specials.png) This folder contains a php script whose function is display additional information about the page when asked for. The information will be passed to the script via the URL parameter by our master script (**wikiRating.js**). So the final step(or first step !) is to enable our extension by adding this to [LocalSettings.php](https://www.mediawiki.org/wiki/Manual:LocalSettings.php) file in the WikiToLearn local instance. `wfLoadExtension( 'WikiRating' );` So now it is the time to see the fruits of our labour: [caption id="attachment_1126" align="alignnone" width="1353"]![score1](https://keenlearner.files.wordpress.com/2016/08/score11.png) Basic information about the page[/caption] [caption id="attachment_1127" align="alignnone" width="1353"]![score2](https://keenlearner.files.wordpress.com/2016/08/score2.png) Additional information about the page[/caption] So this is how the output of our engine looks , subtle like a **tip of an iceberg** :P