---
layout: post
title: Prototyping with web components
excerpt: How to prototype an application using web components, ES6 modules and friends.
date: 2019-05-07
updatedDate: 
tags:
  - post
  - orcas
  - beer
---


# Prototyping with Web Components: Build an RSS Reader

How to prototype an application using web components, ES6 modules and friends.
![](https://cdn-images-1.medium.com/max/2520/1*ZRpioUtVq_G_SeCU0EHHOg.png)

We are about to embark on an exploration journey, down the path of prototyping an application using web components, es6 modules, event target, Bit.dev and what not.
[**Polymer/lit-html**
*Efficient, Expressive, Extensible HTML templates in JavaScript Full documentation is available at…*github.com](https://github.com/Polymer/lit-html)
[**teambit/bit**
*Component platform * Discover components * Video demo * Docs * Blog * Gitter * Discourse Bit makes it easy to share and…*github.com](https://github.com/teambit/bit)

This post is the first of a series, where I plan to introduce to you this vibrant web standard called Web Components in a way of joined discovery.

We will learn together how to use web components and explore some additional goodies. By all means, I’d love to see inputs from the community on how this work can and should improve.

In this post, we’ll prototype an RSS reader using Web components and friends. Our end result will look as follows:

![](https://cdn-images-1.medium.com/max/2000/1*B5tXOnFy9AthuzvpR6WLug.png)

And here’s the code in GitHub:
[**qballer/rss-reader**
*Prototyping an rss reader . Contribute to qballer/rss-reader development by creating an account on GitHub.*github.com](https://github.com/qballer/rss-reader)

## Why Web Components??

The main focus of the series is web components and before we dive in I would like to stop and talk about why you would choose web components for your UI strategy. There are a few reasons:

1. **Future proofing** — They used to call it JavaScript fatigue, but that term has fallen out of grace. Now, I hear people talk of future-proofing. Web components are a standard and are supported by the browser. In the short history of the web, choosing the standard has proven useful.

1. **Framework agnostic** — What do you do when you have several teams, working on a big application with a few libraries like Vue and React. Some times you would like the same functionality across all those libraries and this feat is hard to reach. Sometimes you have multiple teams on different versions of React which require the same component. **Standardize**!

1. **Reusable design system** — Another perspective for framework agnostic components is when you need to create a [design system for your team.](https://bit.dev) Web components seem like the best way to achieve that.

1. **Bundle size-** why should I ship something which the browser can do. VDOM rendering is a mind-blowing concept, but this can achieve much more. Now don’t get me wrong, React is more mature and ready in terms of API usage and supporting libraries, but sometimes size really matters.

## **What are web components?**

Web components allow you to develop a component encapsulated from the rest of the document. A vanilla way to do things. [There](https://dev.to/thepassle/web-components-from-zero-to-hero-4n4m#-a-components-lifecycle) [are](https://www.smashingmagazine.com/2014/03/introduction-to-custom-elements/) [many](https://hackernoon.com/how-to-think-about-web-components-9875d599d0ec) great guides on this subject. This is the main offering of web components:

1. **Custom Element** — Javascript API which allows you to define a new kind of html tag, specific to your component collection.

1. **HTML templates** — introducing the `<template>` and `<slot>` tags, which allow you to specify the layout of the template.

1. **Shadow DOM** — or as I call it, the “mini dom” which is specific to your component. Some kind of an isolated environment for your component DOM, separated from the rest of the document.

These 3 API’s together allow you to encapsulate the functionality of a component and isolate it from the rest of the APP with ease. It allows you to essentially extend your DOM api with additional tags.

## **How does lit work?**

Lit is an abstraction on top of the vanilla api which provides two main things:

[*Lit-html](https://github.com/Polymer/lit-html) — *a library for html templating. This library provides an easy way to create html template. It basically allows you to create re-usable html templates in the javascript context.
[**Polymer/lit-html**
*An efficient, expressive, extensible HTML templating library for JavaScript. - Polymer/lit-html*github.com](https://github.com/Polymer/lit-html)

The library uses a great feature called [tagged templates](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Tagged_templates), shipped with es6 which looks like this:

    tag `some ${boilerPlate} in my string`

This feature allows us to parse the string with a custom function. This is the core of lit-html, which combines templating in our javascript directly in the browser. In the case of lit a render function inside a lit element component can contain an expression like the following:

<iframe src="https://medium.com/media/d64eee669ea3f0aed5b92f362233d70d" frameborder=0></iframe>

You can read their docs [here](https://lit-html.polymer-project.org/guide/template-reference).

[*lit-element](https://lit-element.polymer-project.org/)* — base class for components. In the modern era we need to manage the life cycle of a component. Yea, we can do this from javascript without any abstractions on top of that. What lit-element does for us is give us a way to define props, hook to component lifecycle and unified component interface.
[**LitElement**
*A simple base class for creating fast, lightweight web components*lit-element.polymer-project.org](https://lit-element.polymer-project.org/)

For a bit deeper dive let’s look at the nav-bar component:

<iframe src="https://medium.com/media/59ac1f4c25c89de795191261bc28e768" frameborder=0></iframe>

## **Let’s build an RSS-Reader! This is so 1999…**

I loved the 90s. Also, I just couldn’t build another todo app.

I wanted to create a concise enough example to discuss over a blog, and broad enough to provide real value. Hence our friendly RSS reader was created.

For those of you unfamiliar with [RSS](https://en.wikipedia.org/wiki/RSS), it is a syndication protocol created in the turn of the century to allow users and application access to updates of online content. I’ve been using it for years to keep tabs on blogs and forums which I like. So without further ado …

You can find the source code of the project in this [repository](https://github.com/qballer/rss-reader).
[**qballer/rss-reader**
*Prototyping an rss reader . Contribute to qballer/rss-reader development by creating an account on GitHub.*github.com](https://github.com/qballer/rss-reader)

I encourage you to find my code smells, and offer pull requests, which will improve this guide. The highlights would be mentions in a future blog post about this application. like I mentioned earlier this is a joined exploration, and any contributions are welcomed.

### **Some general design constraints:**

1. **Lit-element** — this project is using the fine work of lit-html and lit-element by the polymer team. It seems like a great library to work with on top the web component standard which takes away a lot of boilerplate pain. It’s important to note that lit was heavily inspired by [hyper](https://html.spec.whatwg.org/multipage/custom-elements.html#custom-elements-api), another great library worth exploring.

1. **Bundle free** (almost) — Wishing to explore some more new features of the web, this project utilizes es6 modules heavily. This is but with one exception to the rule, the [RSS parser](https://github.com/bobby-brennan/rss-parser#readme) by Bobby Brennan is a “normal” browser package.

1. **Browser only** — this project doesn’t have a backend component because I feel Server Side Rendering is a topic for a different post which will go in more details.

1. All modules are made available on the [**bit.dev component platform](https://bit.dev)** for future reuse. The [bit cli](https://github.com/teambit/bit) and platform is one of the best ways to share JS components in general and web components specifically. It has the great benefit of encouraging modularity.

1. This project uses timers and eventTarget heavily instead of workers. Workers don't play well with es6 modules. When those reach to full working state, I would be more than happy to refactor.

1. This repo is in the prototyping phase and so it doesn’t contain tests. I believe in tests, and will insert them in the future. This may go against TDD but I feel wouldn’t contribute to the learning process currently. When it would be added I will share the refactoring needed to introduce tests.

Let's review the main entry points of the app to grasp what going on. index.html

<iframe src="https://medium.com/media/26d697a901e82b75758c8f9c20bf144c" frameborder=0></iframe>

Here is the main function in the reader.js file:

<iframe src="https://medium.com/media/b80e83d30393e5f1f622b9134d648203" frameborder=0></iframe>

The gist of things is that everything communicates via events and that way every component in the app is independent. For the rest of the app view the repo.

**General**

1. index.html - as the main layout of the project.

1. reader.js - the main javascript file of the project, setting up event emitters.

**Elements folder** — lit-element web components.

1. item-list.js - the feed item list rendering the current selected feed.

1. nav-bar.js - edit feeds and consume them.

1. rss-item.js/nav-item.js - representing a single fragment inside their respective lists.

**RSS folder — **Store and rss capabilities

1. events.js - containing all event names and event creation function.

1. feed-key.js - function for creating a unique feed key in the store.

1. rss-client.js - get and parse rss feeds.

1. rss-store - the application main state.

**Utils folder**

1. defer-function.js used to make dispatch events async.

1. define-elements.js - escape web components global as much as possible.

It’s worth noting that the structure of the app has modularity at it’s heart. All the folders in the project basically contain components of different kinds.

Our main drive for reusability is the bit CLI. Bit is a tool which helps your write more modular code, it does so managing the source code and dependencies of a component. Since I’ve started working with bit it has impacted the way I think about modularity and separation of concerns in a deep way.

Bit won’t save you from writing bad code, but the add and export process forces you to at least consider it. The added benefit is that you can share components between future projects, or existing ones.

Let’s dive into another component. Here is the code for the rss client component.

<iframe src="https://medium.com/media/90ef542c59d4c5f1023fb850ae35d2f2" frameborder=0></iframe>

The main point to notice in this component is the inversion of control, main dependencies of the client are received in the factory function. I’ve also used a setTimeout function which calls it’s self as the main timer for the polling the feed. It happens here every 10s just to make things easier to debug.

**Some issues with my project:**

As I was creating this prototype, I’ve encountered some issues I would like to share.

1. `customElements.define` is global. Like mentioned earlier, the components are defined in the global scope. Not only that, all the examples I’ve seen call the define method inside the module and I feel this break encapsulation, and may cause name collisions when the component code base in an App grows. Trying to push away all of this to one place I’ve created the [define-element](https://github.com/qballer/rss-reader/blob/master/source/define-elements.js) component to take care of the work. It can get better. Another thing, is that the spec creators are some what aware of this and are actively [working ](https://github.com/w3c/webcomponents/issues/716)on it.

1. Not so simple to reuse — Let’s say you want to ruse a component in React, you will need to wrap the web-component in a React one. This is in order to take care of propagation of events and props.

1. When working es6 modules and coming off node, the module resolution is a bit unintuitive. You would expect that a folder would resolve to index.js when thinking of it as a module system. But when you think of it as a web server which returns assets, this makes sense. Also adding those .js is somewhat ugly. I guess a browser module loader is order.

**What did we cover here?**

We explored the first prototype of an RSS reader app, how to structure it to drive modularity. We explored why to use web components, what are they and how to integrate them in to an app. Finally, we explored some issues with using web components today.

**What’s next?**

In the next blog posts I hope to touch on styling, and to further our knowledge in web components.

* Prototyping with Web Components — Style, theme and interactivity.

* Prototyping with Web Components — Testing UI elements.

* Prototyping with Web Components — Server Side rendering.
