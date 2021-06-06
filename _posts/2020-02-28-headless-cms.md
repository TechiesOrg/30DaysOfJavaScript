---
layout: post
title: Headless CMS
categories: headless-cms
tags: [headless-cms]
---

This article will cover the basics of what a headless CMS actually is. 

## What is a headless CMS?

A  **headless CMS**  is a back-end only content management system (CMS) built from the ground up as a content repository that makes content accessible via a RESTful API or GraphQL API for display on any device.

The term “headless” comes from the concept of chopping the “head” (the front end, i.e. the website) off the “body” (the back end, i.e. the content repository). A headless CMS remains with an interface to manage content and a RESTful or GraphQL API to deliver content wherever you need it. Due to this approach, a headless CMS does not care about how and where your content gets displayed. A headless CMS has only one focus: storing and delivering structured content and allowing content editors to collaborate on new content.

The counterpart of a headless CMS is often called  _monolithic_,  _regular_  or  _coupled_  CMS, We’re going to use those terms later on.


Let’s have a look at a Monolithic CMS and its feature set:

1.  A database for the content to read and write to.
2.  An admin interface to let editors manage the content.
3.  An integration of reading and writing.
4.  The actual front-end that combines the data from the database with HTML.

To convert that into a headless CMS we remove the templating feature (4.) from the stack as that is the head of that CMS - the actual website. With that done, we can replace it with an RESTful or GraphQL API that is accessible by other systems to access the data that was managed in the Admin UI.Et voilà: you now have got yourself a  **headless CMS**.


Other than by using a regular/monolithic CMS, a website can’t be built only with a headless CMS. A headless CMS separated the head from its stack and therefore lacks this point by design. Therefore, the developer must craft the website by themself and use the provided  REST or GraphQL APIs of the headless CMS to access the content.

Creating the whole website on their own seems like a big task on the list, but by decoupling the CMS from the front-end a developer can choose any technology they are already familiar with and do not need to learn the technology for that specific CMS.

Another big bonus is the fact that one developer can also focus on their own work without handling the bugs of an already existing stack of technology - therefore it is easier to  optimize pages for pagespeed and webvitals and even relaunch parts of the website or make breaking technology decision without worrying about losing the existing content.



## Use cases for Headless CMS

-   Separating your content from the tech stack of your website to give be able to move faster.
-   Websites, Web apps that use JavaScript frameworks like VueJS/Nuxt.js,  React/Next.js, Preact, 
-   Websites created with static site generators such as Jekyll,  Gatsby  or Middleman.
-   Native Mobile Apps for iOS,  Android,  Windows Phone
-   Enrich your ecommerce Stack BigCommerce,  Commercetools,  Hybris,  Magento2, or others) with a proper CMS for your marketing team.
-   Use it for feature flags of your own product to schedule releases of new features.
-   As a configuration interface for your home automation solution.
-   Or to manage content for your intranet.

## Summary

As you see there is no 100% right way and CMS for every use case - but we think that chopping off the presentation layer of your content and make it accessible for more than just one platform if needed is the approach we should aim for! Not just to reuse your content more easily, but if you every want to change your technology stack you don’t have to worry about your content.

