---
layout: post
title: Customizing without Redux
---
This page will take you through the steps you need to do to modify the app and add your own content.

## Table of Contents
- TBD

# What if you don't want to use Redux
The `pwa-starter-kit` is supposed to be the well-lit path to building a fairly complex PWA, but it should in no way feel restrictive. If you know what you're doing, and don't want to use Redux to manage your application's state, that's totally fine! We've created a separate template, [`template-no-redux`](https://github.com/Polymer/pwa-starter-kit/tree/template-no-redux), that has the same UI and PWA elements as the main template, but does not have Redux.

Instead, it uses a unidirectional data flow approach: some elements are in charge of [maintaining the state](https://github.com/Polymer/pwa-starter-kit/blob/template-no-redux/src/components/my-view2.js#L44) for their section of the application, and they [pass that data down](https://github.com/Polymer/pwa-starter-kit/blob/template-no-redux/src/components/my-view2.js#L35) to children elements. In response, when the children elements need to update the state, they [fire an event](https://github.com/Polymer/pwa-starter-kit/blob/template-no-redux/src/components/counter-element.js#L56).

## Next step
We now understand multiple ways to put our PWA together. Let's look at what it take to get it to production with:
- [Building and deploying]({{site.baseurl}}/building-and-deploying/).
