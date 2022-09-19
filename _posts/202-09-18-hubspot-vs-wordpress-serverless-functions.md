---
layout: post
title: "Serverless Functions on HubSpot CMS: vs. WordPress"
categories: Serverless
---

Throughout this post, we'll learn about serverless functions on HubSpot CMS for adding custom functionalities to your CMS-powered website on HubSpot that has, among other services, a built-in CRM and a set of inbound marketing tools out of the box.

Serverless functions offer nearly limitless extensibility. We will show you how easy it is to use them and how powerful they are.

HubSpot provides various built-in tools for working with your contacts, leads, customers, and prospects. Simultaneously, it offers a CMS that you can use to publish blog posts and publish landing pages. It has also services for SEO and analytics out of the box without installing plugins. 

Unlike WordPress, HubSpot provides a much better experience for developers. 

Recently, HubSpot added support for serverless functions that allows you to enhance your site's back-end functionality and easy extensibility without resorting to outdated plugins like in the case of WordPress, which was initially developed as a simple blogging platform.

After you install WordPress for the first time, it doesn't offer much; so if you only need to add a few pages or blog posts, that's quick and easy. However, when you need any advanced functions, such as generating leads or designing landing pages, you'll have to look for a plugin to install the required functionality. Even standard functionalities for SEO, such as adding fields for meta descriptions and sitemaps, are not present.

If you still want to use WordPress, you can also benefit from HubSpot CRM and the other built-in marketing tools by [integrating your WordPress website with HubSpot](https://www.techiediaries.com/wordpress-hubspot-integration/).

For the security side, it's infrequent for a month to pass by without some security issues.

WordPress is highly customizable with plugins and themes, especially if you know how to use or even develop them. However, installing them without caution can mess up your website.

Moreover, if the plugins are not updated and maintained, they become more vulnerable to various spambots, crashes, and attacks, exposing your website to many security vulnerabilities. 

Unlike WordPress, we designed HubSpot for marketers in the first place with an easy-to-use interface that enables you to author and optimize content with no extra plugins.

There are other tools such as [Gatsby or Hexo](https://www.techiediaries.com/jekyll-hugo-hexo/) which are very developer-friendly, but if you want to build a website for clients with no technical background; these are not the best choices. 

At some point, you'll need some customization or functionality which is not built-in into HubSpot. Thanks to the serverless functions, you can use JavaScript to extend and customize your website without managing your server.
 
HubSpot's serverless functions, combined with other developer-friendly HubSpot CMS  features, provides a solution that works for everyone. Serverless functions offer developers almost unlimited extensibility, while users and marketers can quickly populate the site with content. 

In the following sections, we'll show you step by step how HubSpot serverless functions can enable you to customize websites that your clients will appreciate while still using the modern frontend tools that you are familiar with.


## HubSpot Serverless Functions

Serverless is a modern architecture that enables developers to build and run applications and services without managing the server's infrastructure. You don't need to provision, scale, and maintain servers or install and manage databases to host and serve your web applications. 

As a developer, you only need to write code without worrying about any required infrastructures. Moreover, when your business grows, they are much easier to scale. 

HubSpot serverless functions are built with Node.js and JavaScript, so they use tools modern developers are comfortable with, and unlike the case of WordPress, you don't need to learn PHP or WordPress APIs to build them.  

Note, however, that they are not designed as a generic platform where you would run code unrelated to HubSpot.

In terms of extensibility, serverless functions are as powerful as WordPress plugins. We can use them to interact with HubSpot and integrate it with any third-party services through APIs.

The use cases of HubSpot serverless functions are unlimited, and you can use them to implement any requirements you or your clients need. For example, you could generally use them for:

- Getting data and persisting it in HubDB or the HubSpot CRM
- Integrating your website with other third-party services like Google Forms
- Event registration systems
- Submitting forms that send data to other services

HubSpot’s serverless functions are built-in JavaScript and use the [NodeJS](https://nodejs.org/en/) runtime. They are designed to extend your HubSpot site's functionality, such as implementing advanced form submissions and fetching data from other third-party services. 

The functions' code is stored in the developer file system and accessed from the Design Manager UI or the CLI. You can use the CLI to generate and edit the code locally using your preferred local development tools and then upload them to HubSpot. 

For the next section, you need to access a CMS Hub Enterprise account or sign up for a [free sandbox account](https://app.hubspot.com/signup/standalone-cms-developer?userType=developer) to try the example serverless functions. 

## Practical Example with HubSpot Serverless Functions 

This section will present you by example how to deploy serverless functions into a site created based on the [CMS Boilerplate](https://github.com/HubSpot/cms-theme-boilerplate).

If you are not familiar with HubSpot development, you also need to follow [the getting started with serverless functions](https://developers.hubspot.com/docs/cms/guides/getting-started-with-serverless-functions) guide before going through this section if you want to write your code as your progress through the steps. 

Let's start by implementing a serverless function that sends a GET request to a third-party REST API to fetch the latest news data using the Axios client.

> **Note**: We’ll be using a third-party API available from [NewsAPI.org](https://newsapi.org/) to retrieve news data. So you first need to go to their website [here](https://newsapi.org/register) to register for an API key.

APIs that require authentication or use API keys are not safe for a website's frontend, as they would expose your credentials. That's why serverless functions are a good solution as an intermediary, allowing you to keep your credentials secret. 

Head over to a command-line interface and run the following commands:

```bash
cd local-cms-dev
mkdir myfunctions
hs create function 
```

First, we navigate to our local CMS project, and we call the `hs create function` command to generate a simple boilerplate function.

> **Note**: For a comprehensive documentation on the HubSpot CLI, see the [reference documentation](https://developers.hubspot.com/docs/cms/developer-reference/local-development-cms-cli). 

You'll be prompted for some information about your functions, such as:

- Name of the folder where your function will be created, enter `myfunctions\getnews`
- Name of the JavaScript file for your function, enter `getnews`
- Select the HTTP method for the endpoint, select `GET`
- Path portion of the URL created for the function, enter `getnews`

You should get a message saying that **A function for the endpoint "/_hcms/API/getnews" has been created. Upload "myfunctions\getnews.functions" to try it out**

This means, once uploaded, our function will be available from the `/_hcms/API/getnews` endpoint.

Before uploading the function, let's first implement our desired functionality.

Open the `myfunctions\getnews.function\getnews.js` file, you'll find some boilerplate code for a serverless function that sends a GET request to HubSpot search API. Remove the boilerplate code and leave only the following updated code:

```js 
const axios = require('axios');
const API_KEY = '<YOUR_API_KEY_HERE>';

exports.main = async (_, sendResponse) => {
   
};
```

We require the Axios library for sending HTTP requests, and we export a main function that HubSpot will execute when a request is made to the associated endpoint. We also define an `API_KEY` variable that holds the API key from the news API.

Next, inside the body of the main function, add the following code:

```js 
const response = await axios.get(`https://newsapi.org/v2/everything?q=HubSpot&from=2021-03-12&sortBy=popularity&apiKey=${API_KEY}`);
sendResponse({ body: { response: response.data }, statusCode: 200 });
```

We call Axios to send a GET request to the API endpoint; then, we call the `sendResponse` method to send the fetched data back to the client. We could call this API directly from the frontend code, but we'll need to expose our API key, which should be secret, but thanks to the serverless function fetching data will take place on the server-side, and we don't have to expose the secret.

This API will search for news articles that mention the "HubSpot" keyword on the internet.

Finally, run the following command to upload your function:

```bash
hs upload myfunctions myfunctions
```

This command will upload files from the `myfunctions` local folder to a `myfunctions` folder (that will be created) in the Design Manager of your account.

Finally, you can run the method by visiting the `/_hcms/API/getnews` endpoint with your web browser. In our case, we need to visit [http://hubspot-developers-ch48rf-14526108.hs-sites.com/_hcms/api/getnews](http://hubspot-developers-ch48rf-14526108.hs-sites.com/_hcms/api/getnews)

Next, let's implement a second serverless function for creating HubSpot contacts from new Google form submissions. 

If you use Google forms for generating leads, you can easily and automatically save the submissions to HubSpot CRM to organize, track, and build better relationships with your leads and customers.

Head back to your terminal and run the previous command to generate a serverless function:

```bash
hs create function 
```

You'll be prompted for the following information:

- Name of the folder where your function will be created, enter `myfunctions\getformcontact`
- Name of the JavaScript file for your function, enter `getformcontact`
- Select the HTTP method for the endpoint, select `POST`
- Path portion of the URL created for the function, enter `getformcontact`

Next, you need to get a HubSpot API key from [https://app.hubspot.com/l/api-key/]( https://app.hubspot.com/l/api-key/) then open the `myfunctions\getformcontact.function\getformcontact.js` file and add the following code to your serverless function:

```js 
var request = require("request");

exports.main = (context, sendResponse) => {
  const body = context.body;
  
  var options = {
    method: 'POST',
    url: 'https://api.hubapi.com/crm/v3/objects/contacts',
    qs: { hapikey: '51a40969-a29d-45bc-88fa-d687df3c31b7' },
    headers: { accept: 'application/json', 'content-type': 'application/json' },
    body: {
      properties: {
        firstname: body['First name'],
        lastname: body['Last name'],
        email: body['Email'],
        phone: body['Phone']
      }
    },
    json: true
  };

  request(options, function (error, response, body) {
    if (error) throw new Error(error);
    sendResponse({ body: { response: "The contact is successfully created!" }, statusCode: 200 });
  });
};
```

We use the `body` property of the `context` parameter, passed to the exported `main` function by HubSpot when sending a request to the associated endpoint, to retrieve the data submitted via a POST request to the endpoint. Next, we use the data (first name, last name, email, and phone) to create a contact on HubSpot CRM by sending a POST request to the `https://api.hubapi.com/crm/v3/objects/contacts` endpoint.

Next, we need to set up a simple Google form. Simply go to [Google forms](https://docs.google.com/forms/u/0/) and create a new form with the first name, last name, email, and phone fields.

After creating the form,  you should go to **Script editor** of the form, then [add a script and set up a trigger](https://efficientcoder.net/post-google-form-webhook/) for invoking the script when the user submits the form. In the script editor, write the following code:

```js
var hubspotEndpoint = "https://hubspot-developers-ch48rf-14526108.hs-sites.com/_hcms/api/getformcontact";
function onSubmit(e) {
    const form = FormApp.getActiveForm();
    const allResponses = form.getResponses();
    const latestResponse = allResponses[allResponses.length - 1];
    var res = latestResponse.getItemResponses();
    var data = {};
    for (var i = 0; i < res.length; i++) {
        const qTitle = res[i].getItem().getTitle();
        const qAnswer = res[i].getResponse();
        data[qTitle] = qAnswer;
    }
    
    UrlFetchApp.fetch(hubspotEndpoint, {
        "method": "post",
        "contentType": "application/json",
        "payload": JSON.stringify(data)
    });
};
```
This is a [Google Apps script](https://en.wikipedia.org/wiki/Google_Apps_Script), a scripting platform developed by Google for light-weight application development in the Google Workspace platform.

Inside the the `hubspotEndpoint` variable, make sure to put the URL to your HubSpot serverless endpoint.

Next, run the following command to upload your functions:

```bash
hs upload myfunctions myfunctions
```
 
Now, go to your form, fill in some contact details and submit it.  After doing that, this script will invoke our serverless function to create the contact on HubSpot CRM and send the contact's details via a POST request. You can make sure the contact with the same details is created by accessing the [Contacts](https://app.hubspot.com/contacts) page of your HubSpot CRM account. 

Without serverless functions, you would need to resort to workarounds such as automations using services such as [Zapier](https://zapier.com/apps/hubspot/integrations) or [Integromat](https://www.integromat.com/en/integrations/hubspotcrm) if you need to connect both apps. 

## Conclusion

We have covered how to use serverless functions to add custom functionality to our HubSpot powered website and integrate with its built-in services such as the CRM.

We introduced you to serverless functions on HubSpot, which offers developers an edge over websites created with Wix, Squarespace, or similar services; with unlimited extensibility and custom functionalities while working with the preferred tools and modern workflows such as CLIs, IDEs, and GitHub, etc.

Also, unlike WordPress, HubSpot serverless functions let you add powerful features to websites quickly and easily with JavaScript and modern tools. In the same time, you avoid the security issues and other problems related to WordPress plugins. 

If you need a small brochure based website where you only need to update the content once in a while,  any CMS would do the job.

However, for those looking for more out of the box functionalities such as CRM management, SEO, and extensibility without resorting to workarounds and hacks, you owe it to yourself to try HubSpot. Make sure to sign up for a [sandbox account](https://app.hubspot.com/signup/standalone-cms-developer?userType=developer) and create your own HubSpot serverless functions in minutes. 

### Further reading

- [HubSpot vs. WordPress](https://www.hubspot.com/products/cms/best/wordpress-alternatives)
- [Serverless Architectures](https://martinfowler.com/articles/serverless.html)
- [HubSpot Serverless Functions](https://developers.hubspot.com/docs/cms/features/serverless-functions)

