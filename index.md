---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: post
title: "JavaScript in 30 days"
banner: "/assets/images/banners/home.jpeg"
---

This website aims to be the definitive resource and reference for studying modern web development using latest web technologies and methods.

> Note: Read the relevant articles and tutorials for each topic, then complete the challenges.

If you are an absolute beginner in web development, please begin by gaining a basic grasp of the following topics:


- What is Http and Https
- How web browsers work
- DNS or Domain Name Service
- Hosting


You simply need a fundamental understanding of the preceding subjects to become a web developer; in-depth knowledge is unnecessary.

Although we have some tutorials for the three pillars of the web i.e HTML, CSS and JavaScript, we recommend that you are already familiar with these three prerequisites. You don't need to master every detail of JavaScript, nor HTML or CSS.

> Note: HTML, CSS and JavaScript are three official languages of the web but recently the web got a fourth official language that is called WebAssembly.


What do you need to learn about HTML?


- Commonly used tags
- The anatomy of an HTML document
- The DOM
- Semantic HTML
- SEO basics
- Virtual DOM and Shadow DOM



What do you need to learn about JavaScript?


- The basic syntax such as declaring variables, functions and classes, constructs such as loops and conditional statements, etc.
- DOM manipulation methods
- How to fetch data from remote sources using the fetch API or Ajax (XHR)
- Promises and asynchronous programming
- Observables and reactive programming (advanced)
- MVC design pattern


You also need to familiarize yourself with the following concepts:


- Modules and components
- Client-side routing
- SPAs
- Server-side rendering

And formats such as:

- JSON format

### Common questions asked by developers


> What is JS?
> What is HTML?
> What is CSS?
> What is WebAssembly?


### Resources


These are some of the best free online resources to help you learn these HTML, CSS, and JavaScript.


Traditional web development involves frontend development and backend development with different technologies such as JavaScript, HTML and PHP. If you are a veteran web developer, you'll mostly be familiar with the LAMP stack.


> Note: A LAMP Stack is a mix of open-source software for creating websites and web applications. LAMP stands for Linux, Apache HTTP Server, MySQL relational database management system, and PHP programming language.

However, nowadays, contemporary tools and technology exist to develop web apps. This is the outcome of a single tool that allows developers to execute JavaScript on the server in addition to the initial platform, the browser. This software is known as Node.js, although it may also be referred to as node.

> Also check out deno.

The majority of web applications contain similar functionality, and many developers are keen to make their implementations available to others as open source libraries and modules.


These implementations are shared through centralized services like GitHub and the NPM registry.


You may download and install packages from the npm registry directly into your Node.js project using package managers such as npm and yarn.


Node is not just utilized as a server technology, but it is also deployed on development machines to offer the runtime for command-line interface tools aimed to enhance developer productivity. Popular frameworks and technologies, such as Angular, include their own Node-based CLI tool. For example:


- Angular CLI
- etc.


It's worth noting that you can also use package managers such as npm to install and manage the dependencies of your front-end application.



By incorporating JavaScript onto the server, developers ushered in a new era of web development that involves designing and developing web applications using a single programming language. This eliminates the need for JavaScript developers to learn another language, such as PHP or Python, in order to build the backend of frontend web applications.


Another important factor that has contributed to the modernization of web development is that web browsers have evolved into powerful platforms capable of running full-fledged JavaScript apps without relying on the server for processing but only for serving the static files of the application and data.


Front-end web developers, backend web developers, and full-stack web developers are the three sorts of web developers. However, with the ability to run JavaScript on the server, frontend developers can develop full-stack web apps more easily than ever before.


This is also true owing to cloud services that provide platforms such as PaaS, Firbase, hosted backends such as Appwrite, and headless CMS systems such as WordPress and Contentful.


Moreover, when browsers become powerful, new frontend frameworks and libraries are created by giant tech companies such as React by Facebook and Angular by Google.


On top of these frameworks, new meta frameworks and practices are developed such as:

- Next.js
- Remix
- Nest.js: this is actually a server-side framework inspired by Angular but not built on top if it.
- Server side rendering
- Static site rendering
- Lazy loading
- JSX
- Reactive programming
- State management
- REST and GraphQL APIs
- React server components


Although Angular is a JavaScript client-side framework, it is actually built and used with TypeScript, a superset of JavaScript created by Microsoft that adds support for strong typing and object oriented concepts to JavaScript.


> Note: Web browsers do not interpret TypeScript, thus it must be compiled to JavaScript on the development machine before being sent and executed on the users' machines. However, a new proposal to support TypeScript in browsers was recently introduced.



React also introduced a new syntax called JSX that can be used to write HTML in JavaScript.

Because modern web browsers can render and run full-fledged web applications, which frequently comprise several source code files and other assets such as CSS, images, and fonts. This resulted in the development of a type of tools known as bundlers, such as webpack.

For JavaScript applications, Webpack is a static module bundler that takes all of your application's code and makes it usable in a web browser. The JavaScript, node modules, images, and CSS styles used in your app are bundled into reusable pieces of code called modules that may be utilized in your website with ease. With this modular split of responsibilities provided by Webpack, it is much simpler to manage, debug, validate, and test your code. Webpack isolates the code depending on how it is utilized in your app.

> Also check out Vite

The majority of the processing in modern frontend or client-side JavaScript frameworks can be done in the browser, but they still need to retrieve data from the server, which houses the database that can properly store user data. As a result, they must connect with the backend via a set of standards known as web programming application interfaces, or APIs. REST and, more recently, GraphQL are the most prevalent.


Because Node is a platform for executing JavaScript on the server at the first place, we can use it to build backend apps that provide access to the server's database and other resources to client-side applications via REST or GraphQL APIs.


So, assuming you already know JavaScript syntax, which is required for any frontend web developer, you can leverage Node with a variety of frameworks such as Express.js and Happi.js to provide a web API for your frontend app to communicate with the server, allowing you to develop a full-stack web application.

> Talk about databases
> Hosted and managed vs self hosted databases
> Relational vs Document vs Graph databases

- CockroachDB is a distributed database with standard SQL for cloud applications
- YugabyteDB


- MySQL

- PostgreSQL

- MongoDB

> How about storing data on the client side, is that possible?

> What is an ORM?





What if you don't want to learn additional backend staff and instead want to focus on your frontend skills, but you still need to develop full-stack web applications? This is also achievable thanks to cloud services, either hosted or self-hosted.

- Firebase by Google
- Appwrite
- Supabase
- Parse 

This sort of services is known as PaaS, which stands for Platform As A Service.


The list also inlcude headless CMS systems — Content Management Systems — such as Contentful that you can use to manage contents of any types and integrate that with your frontend application to deliver a complete experience for users.


WordPress, the most popular CMS of all times, has recently exposed a REST API for interacting with your site from a frontend application allowing developers to build modern applications that use PHP and Wordpress as the backend without building everything from scratch.


In most situations, building web applications entails implementing authentication to allow users to identify themselves before they can access restricted resources, such as regions of your application or data. You may create your own authentication system by employing several strategies, such as:


- JWT
- Session and cookies.


If you want to build the authentication system yourself, you'll have to use a bunch of different libraries on top of Node.js and frameworks such as Express. However, you can also use other third party services such as Firebase to provide authentication functionality for your application.
📚
Aside from web APIs, authentication is considered one of the most common web development problems that most developers must solve when developing web applications, so you don't have to worry about that because you don't have to reinvent the wheel, but you can use existing solutions as downloadable modules and libraries available from npm.


Other Common web dev problems are CRUD operations and pagination. Pagination can be implemented at server-side or client-side, as finite or infinite scrolling, etc.
offset and cursor pagination
> Client-side pagination is for a small amount of data and is primarily for presentation purposes. Server side pagination handles large amount data, and provides stability and scalability.

> https://nordicapis.com/everything-you-need-to-know-about-api-pagination/
> https://itnext.io/the-best-database-pagination-technique-is-530abf2aab51

One more common web dev problem is routing...

- Client-side vs server-side routing
- File-based routing


> Talk about caching

> Talk about state management

What about WebAssembly? Don you need to worry about that? Actually, not that much as you don't need to master it unless you have to build advanced tools such as compilers for the web. However, knowing about it is a good addition to your web development knowledge.


As a web developer, you'll mostly won't need to write WebAssembly directly but through frameworks such as Blazor which is a toolkit built by Microsoft on top of WebAssembly that allows developers to write client-side web applications with C#. So this is only necessary beneficial for you if you are a C# developer and want to use your skills to build web applications without learning JavaScript.

--


Build desktop and mobile applications with your JavaScript skills.


- Ionic
- React Native
- Electron


- Git-based workflows
- Monorepos
- Material design, Bootstrap and Tailwind
- Serverless



> Realtime communication


# Web development stacks
# Static site generators


- Next.js
- Gatsby


# Modern Frontend Web Frameworks


- Angular
- React
- Vue
- Svelte
- Preact
- Lit
- Alpine
- Solid
- Elm
- Stimulus

PWAs
Web components 
https://stackdiary.com/front-end-frameworks/




# Modern browser APIs such as:


- Dark mode
- Payment APIs
- Web mentions



# Learn web development with Angular


## Angular & Appwrite
## Angular & Firebase
## Angular & Contentful
## Angular & Node/Express.js
## Angular & Bootstrap
## Angular & Tailwind
## Angular & Material Design


## Angular & Ionic
## Angular & Electron


## Angular basics


## Common webdev problems with Angular


### Angular & authentication
### Angular & CRUD
### Angular & routing
### Angular & pagination
### Angular & http client
### Angular & REST API
### Angular & GraphQL API
### Angular architecture
### Angular monorepo


# Learn web development with React
# Learn web development with Vue
# Learn web development with Svelte


>> In essence, a CSS framework comprises several CSS stylesheets ready for use by web developers and designers. The stylesheets are prepped for use for standard web design functions: setting colors, layout, fonts, navbars, etc. Generally, stylesheets are supported and expanded by other scripting technologies like SASS and JavaScript.


>> With a CSS framework, the user has a completed CSS stylesheet, and they only have to code the HTML with accurate classes, structure, and IDs to set up a web page. The framework already has classes built-in for common website elements – footer, slider, navigation bar, hamburger menu, column-based layouts, etc.


1. Bootstrap
2. Tailwind CSS
3. Foundation
4. Bulma
5. Skeleton


Hosting services

- Netlify
- Railway
- Vercel
- Cloudflare

Other frameworks:

- Blazor
- PyScript

## Next Generation Web Frameworks

>The next-gen web framework.
> fresh is a next generation web framework, built for speed, reliability, and simplicity. Some stand out features:

- Just-in-time rendering on the edge.
- Island based client hydration for maximum interactivity.
- Zero runtime overhead: no JS is shipped to the client by default.
- No build step.
- No configuration necessary.
- TypeScript support out of the box.
- File-system routing à la Next.js

