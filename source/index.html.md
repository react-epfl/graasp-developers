---
title: Developer Resources

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

search: true
---

# Introduction

Welcome to the `Graasp Get Started with React App`! An initial project structure.
This `Get Started React App` has been developed for starters adoption. You can use it as much as you need, add small to big modifications. All links in the sections and this documentation will help you get started.

You can view code examples in the dark area to the right.

This guide is divided into the following sections:

- Forking the Starter Repository

- Installing Dependencies

- Starting the application

- Code Style

- Testing

- Adding your own dependencies

- Updating dependencies

# Labs

Labs are a special type of application that power the core learning component of Graasp. Labs usually refer to subject-specific simulations or virtual experiments that can be run on the browser or within Graasp's mobile application. Labs usually have pedagogical requirements, which are out of the scope of this guide, that should be clear before one starts developing a lab. For example, if you want to develop a lab to teach students about pH, you should have a good idea about how this is taught in a typical Chemistry class. Technically speaking, however, labs are simple web applications, usually involving only HTML5, CSS and JavaScript. In this section we explain how to get you started developing labs using JavaScript frameworks such as React and Angular. Choose your preferred framework and start developing labs for education with this short guide.

## React

### Forking the Starter Repository

This is the quickest way to get started!
First, open the [graasp/react-get-started-app](https://github.com/react-epfl/graasp-app-starter-react) link in a new tab. On the top right of the repository, click fork. Then clone or download the cloned app from your own account.

> You can also just clone using SSH or HTTPS

```shell
  git clone git@github.com:your-username/graasp-app-starter-react.git
```

### Installing Dependencies

To install the application dependencies

1- Open your `Terminal`

2- Navigate to the cloned of downloaded project directory or folder

3- Run `yarn install`. But make sure you already have yarn installed on your development environment for this.

### Starting the application

To start your development server, run `yarn start` when all installations is completed and you're done.
This script executes a development server with force reloading enabled. Then your server keeps listening on all your modified files and reload your browser as well to apply changes an asynchronous way running on the port `3000` by default.

Then navigate to `localhost:3000` to preview your application running.


### Code Style

ESLint is a tool for identifying and reporting on patterns found in ECMAScript/JavaScript code. Normally, it is configured by default (you can see the configuration [here](https://github.com/eslint/eslint)). Once you installed it, by restarting your server, you will see all synthax issues rendered in the terminal as well as the browser console.

> In case you want to enforce a coding style, you can just use this tho disable eslint controls for a particular section or lines of code.

```javascript
  // eslint-disable-next-line no-param-reassign <here include the eslint rule you want to disable, e.g. no-param-reassign>
```

### Testing

To run tests just execute `yarn test`. Note that the tests are also asynchronous. Then every time you save a file, the tests are re-run. You can read more about React testing [here](https://github.com/kentcdodds/react-testing-library).


# API

# Authentication

Authentication is handled by the Graasp ecosystem. Apps hosted on the `graasp.eu` domain will receive
the cookie from the Graasp context they are running in.

So for example, an app running inside the Graasp Pages context will make requests to the API with the
cookie that it receives from the parent.

There are two types of users that we consider in the ecosystem and each is handled with its own cookie. 

## Graasp Users

Graasp users are those authenticated with their email via the `graasp.eu` platform. These are usually
the teachers or authors of spaces.

In the case of Graasp Pages, if you access a space from the `viewer.graasp.eu` subdomain, Graasp users
will be enforced.

## Light Users

Light users are those authenticated with a nickname, nickname and password combination, or anonymously.
Light users usually represent the learners, students or consumers of a space.

In the case of Graasp Pages, if you access a space from the `cloud.graasp.eu` subdomain, light users
will be enforced.

# App Instance

An app instance is a document that represents an instantiation of an app that has been configured to
run inside a space. App instances are linked to one user, but can be potentially accessed by users
with more permissions.

In order for an application to save data for a user, it needs to have an app instance. Inside an app
instance, an app can save its state. Similarly, with an app instance, a client can create resources
for it.

## Create

> In order to create an app instance you need to make a `POST` request to the following endpoint.

> **POST /app-instances**


> Example `POST` request body.

```json
{
  "app": "5bd072b3532c3e058807decb",
  "state": {
    "modified": false,
    "progress": 0
  }
}
```

Creating a new `AppInstance` object is done via a `POST` request and takes the following arguments
inside of the body of the request.

**Arguments**

  - **app:** The string ID of the app, which corresponds to the app once it is configured.
  - **state:** An string, object, array or other structure you want to seed the app instance with.

## Read

> In order to fetch a specific `AppInstance` you need to make a `GET` request to the following
endpoint specifying the `id` of the `AppInstance` in question.

> **GET /app-instances/:id**

> In order to fetch all of the `AppInstance` objects for a given app, you need to make a `GET`
request to the following endpoint, specifying the `appId` in question.

> **GET /app-instances?appId=:appId**

You can fetch a specific `AppInstance` or all of the `AppInstance` objects of an app by performing
different types of `GET` requests.

## Update

> In order to update a specific `AppInstance` you need to make a `PATCH` request to the following
endpoint specifying the `id` of the `AppInstance` in question.

> **PATCH /app-instances/:id**

> The body of your request should include the state with the **full** updated state. 

> Example `PATCH` request body.

```json
{
  "state": {
    "modified": true,
    "progress": 42
  }
}
```

You can update a specific `AppInstance` by performing a `PATCH` request and including the updated
parts of the `AppInstance` inside the request's body. For clients, the most important part to
consider is what is placed inside the `state` key, which is how clients handle the state of an
`AppInstance` that they want to persist.

<aside class="warning">
  If you do not pass the <strong>full</strong> state, you will override the <code>AppInstance</code>
  state <strong>without</strong> the ommitted information. 
</aside>

## Delete

To delete an app instance, you can send a `DELETE` request.

<aside class="warning">
  This request is final. You will not be able to recover the <code>AppInstance</code> after it has
  been deleted.
</aside>

> In order to update a specific `AppInstance` you need to make a `DELETE` request to the following
endpoint specifying the `id` of the `AppInstance` in question.

> **DELETE /app-instances/:id**


# App Instance Resources

An app instance resource is a document or object created by an instance of an app that can be either
private to the app instance or public to any app running inside the space. The shape of an app
instance resource is as follows:

```javascript
{
  appInstanceId: String,
  ...,
  content: {
    // mixed content
    ...
  }
}
```

Any client of the API can insert arbitrary content (i.e. whatever it wants) inside the `content` key.
This is limited to a bit less than 16MB by our database constraints.

## Create

To create an app instance resource an application needs to send a `POST` request to the following URL.

```html
/app-instances/:id/resources
```

The body of this request needs to include the `content` of the resource inside the `content` key.

```javascript
{
  content: ..., 
}
```

The response sent from the server will include the location of the newly created resource.

## Read

If the application is configured to create `public` resources, then any application running inside its
same space will be able to access its resources. Otherwise, only the application itself will be able
to read its own resources.

To fetch the resources that an app has created, any client of the API can perform a `GET` request to
the following endpoint.

```html
/app-instances/:id/resources
```

To fetch the **public** resources that have been created inside a given space, you perform the following
`GET` request.

```html
/spaces/:id/resources
```

Both aforementioned endpoints support a query string with the following options.

  - `query`: A MongoDB-style query that we will run against the data inside the `content` key. 
  - `select`: A MongoDB-style select that we will run against the data inside the `content key.
  - `...`

```html
?query=...&select=...
```

Both the `query` and the `select` options are intended to allow consumers of the API to filter and
project parts of the resources that have been saved for a given app or space.

An example follows:

```html
/spaces/:id/resources?query={a:1}&select={b:1}
```

A `GET` request to the endpoint above would get all of the public resources for space `:id` where
`a` inside the `content` key is equal to `1` and will return only key `b` from inside the `content` key.

If we assume that the resources inside a space are the following:

```javascript
[
  {
    _id: 1,
    content: {
      a: 1,
      b: 2,
    }
  },
  {
    _id: 2,
    content: {
      a: 1,
      b: 3,
    }
  },
  {
    _id: 3,
    content: {
      a: 2,
      b: 3,
    }
  }
]
```

Then the query above would return the values of `b` for documents with `_id` equal to `1` and `2`,
which is where `a` is equal to `1`.

```javascript
[
  { _id: 1, content: { b: 2 } },
  { _id: 2, content: { b: 3 } }
]
```

To fetch a specific resource, you can do a `GET` request to the following endpoint.

```html
/app-instances/:appInstanceId/resources/:resourceId
```

The endpoint to fetch a single resource also supports `select` query parameters mentioned above.

## Update

To update the resource a client can send a `PATCH` request including the data that it wishes
to updated inside the `content` key.

Note that you need to send the **complete** content that you wish to replace the **current**
value of the `content` key with.

The endpoint for updating would be the following:

```html
/app-instances/:appInstanceId/resources/:resourceId
```

## Delete

To delete a resource, a client would send a `DELETE` request to the following endpoint:

```
/app-instances/:appInstanceId/resources/:resourceId
```


# Testing

You can test your apps' connection to our API locally using our development server. In order to do
this, you need to configure your `localhost` to  point to `apps.dev.graasp.eu`.

On most Linux and macOS machines you would have to edit the `/etc/hosts` file. On Windows machines this is achieved you edit the `hosts` file inside `C:\Windows\System32\drivers\etc`.

In both cases, simply add the following line to the respective file:

```
127.0.0.1   apps.dev.graasp.eu
```
