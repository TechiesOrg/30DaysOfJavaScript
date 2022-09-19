---
layout: post
title: "Angular 14 with Contentful tutorial"
categories: angular
---

This post will show you how to use Contentful in conjunction with Angular 14 to create a full-stack application.

Contentful is a cloud-based content management platform for organizing and managing contents which can then be accessed through a variety of platforms, such as a website and a mobile app.

When it comes to building client-side apps or providing content creation and management services, both Angular 14 and Contentful are popular choices.

One of the main advantages of [Angular 14](https://angular.io/) is that it provides a uniform way to write and share code, as well as the ability to create apps that can be used on the web, mobile web, native mobile, and the desktop.

Taking advantage of the current Web Platform's maximum performance as well as new approaches and APIs such as [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers) and [Angular Universal](https://angular.io/guide/universal) for server-side rendering, Angular 14 offers a number of benefits in terms of both performance and productivity. 

It also includes high-quality developer tools that simplify the process of developing features in an effective ways and comes with its own [template syntax](https://angular.io/guide/template-syntax) that extends HTML, and can be further expanded with custom components. Additionally, popular integrated development environment (IDE) and text editor provides Angular 14-specific feedback and help for its users. You won't have to worry about getting stuck in the ins and outs of the coding process in order to create powerfull apps; instead, you can concentrate on implementing your application idea.

Angular 14 is the technology that powers the frontend of Google applications that are utilized by millions of people all around the world because to its scalable architecture and its productivity-enhancing capabilities.

Contentful is a headless content management system that offers project-specific foundation for the purpose of managing the contents of a website.

It is headless, or independent of the front-end, enabling you to use the backend and content infrastructure with any framework, including Angular 14, React, Vue, etc.

It allows you to add and update information that will be displayed on the frontend of your website or mobile application. It also saves you the time and effort of developing your own backend – which requires knowing a backend language/platform such as Python or Node.js and database administration – and offers different tools that assist developers interface the frontend – a website or application – with the backend.

## Creating contents

Let’s get started with our first section in this tutorial – in the Contentful UI, we’ll create a [space](https://www.contentful.com/help/spaces-and-organizations/) with a content model and add content that we’ll be later retrieving from the frontend. As a demo, we’ll be developing a job listings website for developers.

We’ll not be showing a detailed step-by-step guide for this section but you can refer to [this page](https://www.contentful.com/help/contentful-101/) to learn how to do the process.

We should begin by creating our custom structure for our content. The structure functions similarly to a schema, allowing editors to create repeating pieces of content. In a nutshell, here is what you need to do:

-   Sign up for a free Contentful account
-   Create a content type/model called `JobListing`
-   Populate the space with content based on the `JobListing` content type
    
Ou Job model has the following fields and types:

-   Role: Short Text
-   Description: Long Text
-   HowToApply: Rich Text
-   Organization: Short Text
-   Date: Date & time
-   Skills: Short Text & List 
    
After you’ve created and published your job listings. We will now walk you through the process of fetching them through the API and display them with Angular 14.

> Note: Before you can communicate with Contentful, you'll need an [API key, consisting of the Space ID, the Access Token, and the Entry ID](https://www.contentful.com/developers/docs/references/authentication/) that you can get from your Contentful space.

## Create Angular 14 Project

Now that we’ve created our content type and populated some data, let’s proceed to create the Angular 14 project that will fetch and display the job listings from Contentful.

In this section, we’ll see how to:

-   Create an Angular 14 project and modify the page to display the retrieved content in an appropriate way.
-   Create an Angular 14 service that can fetch the data.
-   Include the routes required to navigate the app.
-   Connect the service to the page and display the fetched content.
    
Before you start, you will need to have some prerequisites regarding your development environment.

Since Angular 14 requires the use of [Angular 14 CLI](https://efficientcoder.net/install-angular-cli/) to scaffold the initial projects’ files and any necessary artifacts during the development of the project, you need to have recent versions of Node.js and npm installed on your development machine.

There are various ways that you use to install Node.js in your machine:

-   Obtain an installer that is compatible with your operating system from the [official website](https://nodejs.org/).
-   Make use of the official package manager of your system.
-   Use a Node version manager such as [NVM](https://github.com/nvm-sh/nvm) which will allow you to manage [multiple versions of Node](https://www.shabang.dev/multiple-versions-node-nvm/) on your development machine. We recommend using NVM.
 
If you have Node installed on your machine; simply go to a command-line interface, Command Prompt or PowerShell (Windows) or bash terminal (Linux and macOS) and let’s get started by installing Angular 14 CLI.

Install the most recent version of the Angular 14 CLI by running the following command:

```bash
npm install -g @angular/cli  
```
> Note: You may need to add sudo (for admin access) in macOS and Linux or use a command prompt with admin access in Windows to install the Angular 14 CLI globally on your machine.

After the installation, you’ll be able to use the `ng` tool from your terminal. 

At the time of writing this article, Angular CLI **v14** is installed.

> If you want to use the same version installed in this tutorial at any time later, you simpy need to specify the version when installing the CLI .i.e   `npm install -g @angular/cli@13.3.7`. 

Let’s create our Angular 14 project. In the command-line interface run the following command:

```bash
ng new angularcontentfuldemo --routing --style=css
```

After pressing **Enter** in your keyboard, Angular 14 CLI will create your initial project’s files and install the packages and log the process on the terminal which should have the following printed after project’s creation:

```bash
✔ Packages installed successfully.
    Successfully initialized git.
```

Next, navigate inside the root folder of your project:

```bash
cd angularcontentfuldemo  
```

You can then serve your Angular 14 application using the `ng serve` command as follows:

```bash
ng serve  
```

Your app will be served from `http://localhost:4200/`.

Leave your current command-line interface open for running the development server and open a new one for running the commands that will be following.

Before proceeding, let's first add our Contentful [Space ID and Access Token](https://www.contentful.com/developers/docs/references/authentication/) to the environment variables of our application. 

> Note: You can create an access token using the  [Contentful web app](https://be.contentful.com/login)  or the  [Content Management API](https://www.contentful.com/developers/docs/references/content-management-api/#/reference/api-keys/create-an-api-key).

Open the `src/environments.ts` file and update it as follows:

```ts
export const environment = {
  production: false,
  contentful: {
    spaceId: 'YOUR_SPACE_ID',
    accessToken: 'YOUR_ACCESS_TOKEN'
  }
};
```  

Make sure to replace `YOUR_SPACE_ID` and `YOUR_ACCESS_TOKEN` with your actual credentials.

Let's continue by installing some necessary dependencies such as `contentful`, `bootstrap`,  [rich-text-types](https://www.npmjs.com/package/@contentful/rich-text-types) and [rich-text-html-renderer](https://www.npmjs.com/package/@contentful/rich-text-html-renderer) using the following commands after navigating to your project's folder:

```bash
npm install contentful bootstrap 
npm install @contentful/rich-text-types @contentful/rich-text-html-renderer
```

We'll use contentful to connect with Contentful APIs and bootstrap for styling the Angular 14 UI.

Next, let's add Bootstrap to our project. There are various ways to [add Bootstrap to Angular 14](https://www.techiediaries.com/add-angular-bootstrap/), in our case, we'll include bootstrap files via the `angular.json` file so go ahead and open the configuration file that exists at the root of the project and add the following line:

```json
"styles": [
  "./node_modules/bootstrap/dist/css/bootstrap.css",
  "src/styles.css"
 ]
```

Open the `src/app/app.component.html` file and update it as follows:

```html
<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <h1>Developers Jobs</h1>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>
</nav>
<div>
  <router-outlet></router-outlet>
</div>
```
We simply removed the boilerplate markup except the [router outlet](https://angular.io/api/router/RouterOutlet) and added a Bootstrap header bar. 

### Create the service for communicating with Contentful

Let's now create the service that will encapsulate the code for communicating with Contentful. Go back to your command-line interface and run the following command to generate the service:

```bash
ng g s content
``` 

Create a `content-types.ts` file in the `src/app/` folder and add the following code:

```ts
import * as CFRichTextTypes from "@contentful/rich-text-types";
import * as Contentful from "contentful";

export interface TypeJobListingFields {
    role?: Contentful.EntryFields.Symbol;
    description?: Contentful.EntryFields.Text;
    howToApply?: CFRichTextTypes.Block | CFRichTextTypes.Inline;
    organization?: Contentful.EntryFields.Symbol;
    date?: Contentful.EntryFields.Date;
    skills?: Contentful.EntryFields.Symbol[];
}

export type TypeJobListing = Contentful.Entry<TypeJobListingFields>;
```

This will be used to type the entries corresponding to our content model. We can either write the types manually or use automated tools for a more scalable approach:

-   [cf-content-types-generator](https://github.com/contentful-userland/cf-content-types-generator)
-   [contentful-typescript-codegen](https://github.com/intercom/contentful-typescript-codegen)
-   [contentful-ts-type-generator](https://github.com/arimkevi/contentful-ts-type-generator)
-   [contentful-ts-generator](https://github.com/watermarkchurch/contentful-ts-generator)
-   [TS Content Types Generator App](https://github.com/marcolink/cf-content-types-generator-app) 

Open the `src/app/content.service.ts` file and start by adding the following imports:

```ts
import { Injectable } from '@angular/core';
import { createClient } from 'contentful';
import { from } from 'rxjs';
import { environment } from '../environments/environment';
import { TypeJobListingFields } from './content-types';
```

Next, add the client property and call the `createClient()` function to create a client as follows:

```ts
@Injectable({
  providedIn: 'root'
})
export class ContentService {

  client = createClient({
    space: environment.contentful.spaceId,
    accessToken: environment.contentful.accessToken
  });
  constructor() {}
}
```

Then, add the following method to fetch content from Contentful:

```ts
getJobListings(query?: object){
  return from(
  this.client.getEntries<TypeJobListingFields>(Object.assign({
   content_type: 'jobListing'
  }, query))
  );
}
```

We call the [getEntries](https://contentful.github.io/contentful.js/contentful/latest/ContentfulClientAPI.html#.getEntries) method of `contentful` to retreive the entries corresponding to our model content that we pass as the first argument of the method. We use [Object.assign](https://30daysofjavascript.com/object-assign/) to create an object containing the content type and any other queries that we pass to Contentful. 

The method also accepts a [generic type](https://www.typescriptlang.org/docs/handbook/2/generics.html) that defines the type of the content that will be returned which is in our case  `TypeJobListingFields`.

> _Note If you didn't save your content type id somewhere, you can get it as follows: contentful->content model -> click your content model name -> right sidebar look for your content type id._

Also, add the following method to fetch a job listing by ID:

```ts
getJobListingById(jobListingId: string, query?: any){
 return from(
   this.client.getEntry<TypeJobListingFields>(jobListingId, query)
   );
}
```

### Add routing and display the content

After implementing the service, we need to create a component to display the job listings fetched from the backend; and add routing.
Go back to your command-line interface and run the following commands:

```bash
ng g c jobListings 
ng g c jobListing
```

This will generate the components' files and add the components to the root application module.

Next, open the `src/app/app-routing.module.ts` file and start by importing the components as follows:

```ts
import { JobListingsComponent } from './job-listings/job-listings.component';
import { JobListingComponent } from './job-listing/job-listing.component';
```

Then, add the following routes:

```ts
const routes: Routes = [
  { path: '', pathMatch: 'full', redirectTo: 'listings' },
  { path: 'listings', component: JobListingsComponent },
  { path: 'listing/:id', component: JobListingComponent }
];
```
 Here we define three routes -- the first route simply redirects the user to the second route which links to the JobListingsComponent.
 
You can read more about routing in Angular 14 from this [article](https://www.webtutpro.com/angular-12-routing-by-example-f0cfbdc7b0a8).

Open the `src/app/job-listings/job-listings.component.ts` file and import the service and the other symbols as follows:

```ts
import { Component, OnInit } from '@angular/core';
import { ContentService } from '../content.service';
import { TypeJobListingFields } from '../content-types';
import { Entry } from 'contentful';
```
Next, inside the component's class define the following array to hold the fetched job listings:

```ts
jobListings: Entry<TypeJobListingFields>[] | undefined;
```

Next, inject the service via the component's class as follows:

```ts
constructor(public contentService: ContentService) { }
```

[Injecting the service](https://angular.io/guide/dependency-injection#injecting-services) makes it available to the component.

Then, define the following method for fetching the content:

```ts
getJobListings(){
  this.contentService.getJobListings()
  .subscribe({
     next: (entryCollection) => {
       this.jobListings = entryCollection.items;
       console.log(this.jobListings);
     }
 });
}
```

Then, call the previous method inside the `ngOnInit()` life-cycle method of the component:

```ts
ngOnInit(): void {
  this.getJobListings();
}
```

Life-cycle methods are methods that hook into key events of the component. You can find more information about them from this [article](https://angular.io/guide/lifecycle-hooks).

In the same way open the `src/app/job-listing/job-listing.component.ts` file and add the following imports:

```ts
import { ActivatedRoute, ParamMap } from '@angular/router';
import { switchMap } from 'rxjs/operators';
import { ContentService } from '../content.service';
import { TypeJobListingFields } from '../content-types';
```

Next, define the following property:

```ts
jobListing: TypeJobListingFields | null = null;
```

Next, inject the following services:

```ts
constructor(public contentService: ContentService, public route: ActivatedRoute) { }
```

The [ActivatedRoute](https://angular.io/api/router/ActivatedRoute) class provides information about active route in the outlet.

Next, update the `ngOnInit()` hook of the component as follows:

```ts
ngOnInit(): void {
  this.route.paramMap.pipe(
    switchMap((params: ParamMap) =>
      this.contentService.getJobListingById(params.get('id') as string)
    )).subscribe({
     next: (entry) => {
       this.jobListing = entry.fields;
    }});
}
```

When the component is initialized, we get the job's listing ID from the route using [ParamMap with switchMap](https://webtips101.com/angular-routing-switchmap/). Since our service method returns an observable, we flatten the observable with the `switchMap` operator and we subscribe to the resulting observable to get the fetched entry and assign it to the `jobListing` property. 

The [`switchMap` operator](https://rxjs.dev/api/operators/switchMap) also cancels previous ongoing requests. If the user navigates to the route with a different `id` while the ContentService is still fetching the content, `switchMap` removes the previous request and returns the job listing for the current `id`.

After that, we need to render the content in the component's template. Open the `src/app/job-listings/job-listings.component.html` file and update it as follows:

```html
<div *ngIf="jobListing" class="card" style="margin: 10px; width: 93%;">
  <div class="card-body">
    <h5 class="card-title">
      {{ jobListing.role }}
    </h5>
    <h6 class="card-subtitle">
      {{ jobListing.organization }} - {{ jobListing.date | date }}
    </h6>
    <hr>
    <div class="card-text">
      <h5>
      Description
      </h5>
     <p>
      {{ jobListing.description }}
     </p>
     <hr>
      <h5>
      How to apply?
      </h5>
      <div [innerHtml]="jobListing.howToApply | toHtml"></div>
     <hr>
    </div>
    <p>
    Skills: {{ jobListing.skills }}
    </p>
  </div>
</div>
```

You should notice that under the **How to apply** section, we are displaying the content of the `howToApply` field but we are getting `[object Object]` displayed. That's because this a Rich Text field which is a JSON format for handling complex content structures in a strongly typed manner in Contentful.
Contentful provides many tools to help you work with the [Rich Text](https://www.contentful.com/developers/docs/concepts/rich-text/) feature and we've previously installed the `@contentful/rich-text-html-renderer` package which makes it easy to display rich text fields via a `documentToHtmlString()` function.

Since, we are using Angular 14, we need to use the  function with a [custom pipe](https://angular.io/guide/pipes) that we can apply to the field in the component's template to display it correctly.
Go back to your command-line interface and run the following command to generate a pipe:

```bash
ng g pipe toHtml
```

Open the `src/app/to-html.pipe.ts` file and update it as follows:

```ts
import { Pipe, PipeTransform } from '@angular/core';
import { documentToHtmlString } from '@contentful/rich-text-html-renderer';
import { Document } from '@contentful/rich-text-types';

@Pipe({
  name: 'toHtml'
})
export class ToHtmlPipe implements PipeTransform {

  transform(value: unknown, ...args: unknown[]): unknown {
    return documentToHtmlString(value as Document);
  }
}
```

You can then go back to the file and display the rich text field using the following code:

```html
<div [innerHtml]="jobListing.fields.howToApply | toHtml"></div>
```
Since the result of applying our custom `toHtml` pipe to the `howToApply` field is HTML content, we need to [bind to the innerHtml](https://www.techiediaries.com/angular-innerhtml-binding/) attribute to render it inside the `<div>`. 

## Conclusion

We learned how to use Contentful as our Angular 14 application's backend for managing content.

Software like Wordpress sparked the rise of content management systems. Even though Wordpress is the most popular content management system in the world, Contentful allows you to accomplish more and separate your front-end or view layer from managing content. For more information, you can read [Is Contentful a WordPress alternative?](https://www.contentful.com/blog/2020/03/26/contentful-wordpress-alternative/) or [The Problems with Headless WordPress](https://www.webtutpro.com/the-problems-with-headless-wordpress-196630f5f8f6).

You'll save time and money because you simply need to write and update content once for all platforms that are integrated with your CMS. 
You can create an account for free and start using Contentful to quickly and efficiently manage the contents for your Angular application without the need to build a custom backend from scratch.
