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

-    Forking the Starter Repository

-    Installing Dependencies

-    Starting the application

-    Code Style

-    Testing

-    Adding your own dependencies

-    Updating dependencies

-    Internationalization

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

### Internationalization

The starter app supports internationalization using the react-i18next library.

To add a new language to your app:

1- Add a language json file under `src/langs`. For example `de.json` for German.

2- Add your language translations using a key value pairs format. The key being the expression you use in your source code and the value beings its corresponding translation.  For example: "Welcome to the Graasp App Starter Kit": "Willkommen im Graasp App Starter Kit".

3- Import and add you language json to the react-i18next library under `src/config/i18n.js` by adding your language to the resources.

4- Add a language query string to your links to show the translated version of the app. For example: `http://localhost:3000/?mode=student&lang=de`.

5- To allow teachers and students to be able to change the language, a select box is available by default in the header. 

> You could remove this select box or include it in either the student or the teacher components by copying it along with the changeLanguage and colorStyles methods and editing the options array under `src/constants/langs` to add your new languages.

```javascript
  <Select
    styles={this.colorStyles}
    className="LanguageSelector"
    defaultValue={options[0]}
    options={options}
    value={selectedLanguage}
    onChange={this.changeLanguage}
  />
```

# API

# Authentication

The user authentication is handled by Graasp's ecosystem in a very transparent and familiar way: using session cookies.

Apps hosted on `graasp.eu` domain need to use/send the session cookie when calling the API endpoints.
It is mandatory for the usage of the API.

There are two types of users to consider in the ecosystem, and each uses its own session cookie for authentication purposes.

## Graasp Users

Graasp users are those authenticated using their email and password via the `graasp.eu` platform. These are usually
the teachers or authors in spaces.

If one opens a Graasp page using the `viewer.graasp.eu` link, Graasp users will be enforced.

## Light Users

Light users are those authenticated using a nickname, nickname and password combination, or none (anonymous), when opening a space using the Pages app.
Light users usually represent the learners, students or consumers of a space.

If one opens a Graasp page using the `cloud.graasp.eu` link, light users will be enforced.

# App Running Context

When an embedded app is loading in an ILS, a set of query parameters is passed down to it to provide the appropriate running context. These parameters can be necessary to call the API.

The most important parameter is *`appInstanceId`*. In most calls to the API, this ID needs to be specified.

Other parameters:

  - **appInstanceId**: ID of the `app-instance` of linked to running app (more details about `app-instances` below)
  - **spaceId**: ID of the space/ILS where the app is localed
  - **subSpaceId**: ID of the sub-space/phase where the app is localed
  - **userId|sessionId**: the user identifier, for both the case where a "real" (Graasp/Light) user is accessing the space/ILS, or the case where the content is public and a simple session ID is assigned to this "ephemeral" user.

# Entities: App-Instance

An `app-instance` is a document that represents, as the name implies, an instance of an app that will run inside a space.

The main property of an `app-instance` is the `settings`. This property's purpose is to store app configuration
data. As an app developer, you should only care about modifying or reading this property.

Each `app-instance` is also linked to a Graasp `item` where the app's url is stored along with other metadata related to Graasp.

<aside class="warning">App instances, and its corresponding endpoint, can only be accessed by Graasp Users.</aside>

## Get
> Example of returned `app-instance` JSON object:

```json
{
  "_id" : "<app-instance id>",
  "settings" : "<valid JSON - object/array/string/value/number>",
  "item" : "<graasp item id>",
  "createdAt" : "2018-12-06T10:00:00.000Z",
  "updatedAt" : "2018-12-06T10:00:00.000Z"
}
```

In order to read an `app-instance` one needs to make a `GET` request to `/app-instances/<id>`.

A JSON structure similar to the one on the right will be returned.

## Update
> Example of a `PATCH` request body:

```json
{
  "settings": { "min": 1, "max": 10, "step": 0.5 }
}
```

In order to update an `app-instance` one needs to make a `PATCH` request to `/app-instances/<id>`.

The request's body should contain a JSON object with the `settings` property defined.
An `app-instance` update can only change the `settings` property - any other properties will be discarded.

The resulting updated `app-instance` JSON object will be returned after a successful update request.

## Create/Delete

The creation and deletion of this type of entity is not available in the API - `app-instances` are created/deleted when the corresponding item/app is created/deleted in Graasp.

# Entities: App-Instance-Resource

An `app-instance-resource` is a document that holds data linked to a specific app and user pair.
It can be anything, be it some user input or some metadata generated by the app and related to that user.

For the same user and app pair there can be any number of `app-instance-resources`.

`app-instance-resources` can be potentially accessed by other users with more permissions.

Both Graasp Users and Light Users can use the API endpoints for this entitiy.

## Create

> Example of a `POST` request body:

```json
{
  "appInstance": "5bd072b3532c3e058807decb",
  "data": {
    "offset": -34,
    "progress": 43
  },
  "type": "user-input",
  "format": "my-format-v1",
  "visibility": "public"
}
```

In order to create an `app-instance-resource` one needs to make a `POST` request to `/app-instance-resources`.

The request's body should contain a JSON object similar to the one provided in the example.

**JSON object's properties:**

  - **appInstance:** The `app-instance`'s ID. Mandatory.
  - **data:** Any valid JSON. Defaults to `null`.
  - **type:** Some string representing the type of data being saved. This property can later be used to
  filter results while fetching `app-instance-resources`.
  - **format:** Some string representing the format of the data being saved. Similarly to `type`, this property can later be used to
  filter results while fetching `app-instance-resources`.
  - **visibility:** The possible values are `private` or `public. A private `app-instance-resource` can only be read in the context of its specific app and user pair. A 'public' `app-instance-resource` can be accessed in the context of other apps and users. Defaults to `private`.

The resulting `app-instance-resource` JSON object will be returned after a successful create request.

## Get

To fetch `app-instance-resources` one needs to make a `GET` request to `/app-instance-resources`, and there's two options:

```
GET /app-instance-resources/<id>
```
Fetching a single `app-instance-resource`, by appending its ID in the endpoint's path:

&nbsp;
&nbsp;

```
GET /app-instance-resources?
  appInstanceId=<app-instance id>
  [&userId=<user id>]
  [&type=<type string>]
  [&format=<format string>]
```

Fetching multiple `app-instance-resources`, matching a specific filter passed as a query string:

**Query parameters:**

  - **appInstanceId:** The `app-instance`'s ID. Mandatory.
  - **userId:** If one is trying to fetch other user's `app-instance-resources`, this parameter should be present. Only a Graasp user with admin rights over the app can make this request.
  - **type:** To filter a specific *type*.
  - **format:** To filter a specific *format*.

## Update

To update an `app-instance-resource` one should issue a `PATCH` request to `/app-instance-resources/<id>`

```json
{
  "data": {
    "offset": -34,
    "progress": 73
  }
}
```
The request's body should contain a JSON object with a `data` property defined (see the example). Any other properties will be discarded.

The resulting updated `app-instance-resource` JSON object will be returned after a successful update request.


## Delete

To delete an `app-instance-resource`, one can send a `DELETE` request to `/app-instance-resources/<id>`, passing in the path the ID of the `app-instance-resource`to be delete.

The deleted `app-instance-resource` JSON object will be returned after a successful delete request.

<aside class="warning">
  This request is final. You will not be able to recover the <code>app-instance-resource</code> after it has been deleted.
</aside>

# Entities: User

## Get
> Example of a returned `user` JSON object:

```json
{
  "id" : "<user id>",
  "name": "<user's name>",
  "email": "<user's email>"
  "type": "<graasp|light>"
}
```
In order to get the current `user` (linked to the current cookie session) one needs to make a `GET` request to `/users/current`.

In order to get some `user` one needs to make a `GET` request to `/users/<id>`. In this case the `email` information will be ommitted.

The `type` field can be either `graasp` (normal graasp user) or `light` (users created _on-the-fly_ when _viewing/using_ a space/ILS, based on the authentication scheme chosen by the owner of the space/ILS: username, username with password, or anonymous)

# Entities: Spaces

An `space` document represents a Graasp space.

Both Graasp Users and Light Users can use the API endpoints for this entitiy, except if signaled otherwise.

## Get users
> Example of a list of users belonging to a space:

```json
[
  {
    "id" : "<user1 id>",
    "name": "<user1's name>",
    "type": "graasp"
  },
  {
    "id" : "<user2 id>",
    "name": "<user2's name>",
    "type": "light"
  }
]
```

To get the users that belong to a space one should make a `GET` request to `/spaces/<id>/users`.

<aside class="warning">This endpoint can only be accessed by Graasp Users which have permissions to access the space.</aside>

## Get light-users
> Example of a list of light-users belonging to a space:

```json
[
  {
    "id" : "<user1 id>",
    "name": "<user1's name>"
  },
  {
    "id" : "<user2 id>",
    "name": "<user2's name>"
  },
]
```

To get the light-users that belong to a space, the ones with authentication schemes based on a username, username with password, or _anonymous_, one should make a `GET` request to `/spaces/<id>/light-users`.

<aside class="warning">This endpoint can only be accessed by Graasp Users which have permissions to access the space.</aside>

# Testing

You can test your apps' connection to our API locally using our development server. In order to do
this, you need to configure your `localhost` to  point to `apps.dev.graasp.eu`.

On most Linux and macOS machines you would have to edit the `/etc/hosts` file. On Windows machines this is achieved you edit the `hosts` file inside `C:\Windows\System32\drivers\etc`.

In both cases, simply add the following line to the respective file:

```
127.0.0.1   apps.dev.graasp.eu
```

# Offline

Apps and labs that want to be able to run offline can still make calls to local APIs provided by
the Graasp Desktop and Graasp App offline clients. These calls will tell the client to write or
fetch information from their local databases. Not all of the calls are supported, though. In this
section we outline how to setup the appropriate listeners and how to run the calls.

## Downloading

When an app is downloaded for offline use, its `AppInstance` object and all of the **public**
`AppInstanceResource` objects will be downloaded along with it. These objects will be available for
the application to get from within its offline context.

## Context

An application running inside an offline client will be sent the `?offline=true` flag in its query
string. This flag should be used by offline-ready applications to show a different offline UI, if
needed, and fall back to calling the offline API rather than the online one.

For example, in order to reduce the number of calls to the offline API and thus the amount of disk
I/O, the Graasp Input App will disable auto-saving functionality if offline, and instead show a
"Save" button to the user.

```javascript
// simplified example of rendering a button only when offline, using the react framework
renderButton() {
  const { offline } = this.props;

  // button is only visible offline
  if (!offline) {
    return null;
  }
  return (
    <Button
      variant="contained"
      color="primary"
      onClick={this.handleClickSaveText}
    >
      Save
    </Button>
  );
}

// simplified example of an onchange event handler that calls the api only when online
handleChangeText = ({ target }) => {
  const { value } = target;
  const { offline } = this.props;
  this.setState({
    text: value,
  });
  // only save automatically if online
  if (!offline) {
    this.saveToApi({ data: value });
  }
};
```  

These are just some example of all of the logic that can be dependent on whether or not an app is
running within an offline context.

## Types of Messages

The offline API, when replying, will always send a message with a `type` and `payload`.

```json
{
  "type": <TYPE>,
  "payload": <PAYLOAD>
}
```

The payload will be similar to the response that you would expect, for a given call, from the
online API. However, because the responses are being sent through the messaging channel, we need
to be able to distinguish what type of message is being sent/received. We achieve this by having
a standard for `PostMessageType` and for `ReceiveMessageType`. You should define these in
your application.

```javascript
// PostMessageType
export const GET_APP_INSTANCE = 'GET_APP_INSTANCE';
export const GET_APP_INSTANCE_RESOURCES = 'GET_APP_INSTANCE_RESOURCES';
export const PATCH_APP_INSTANCE_RESOURCE = 'PATCH_APP_INSTANCE_RESOURCE';
export const POST_APP_INSTANCE_RESOURCE = 'POST_APP_INSTANCE_RESOURCE';

// ReceiveMessageType
export const GET_APP_INSTANCE_SUCCEEDED = 'GET_APP_INSTANCE_SUCCEEDED';
export const GET_APP_INSTANCE_RESOURCES_SUCCEEDED = 'GET_APP_INSTANCE_RESOURCES_SUCCEEDED';
export const PATCH_APP_INSTANCE_RESOURCE_SUCCEEDED = 'PATCH_APP_INSTANCE_RESOURCE_SUCCEEDED';
export const POST_APP_INSTANCE_RESOURCE_SUCCEEDED = 'POST_APP_INSTANCE_RESOURCE_SUCCEEDED';
```

## API

By leveraging the `offline` flag provided by in the query string, the app can fall back on using
the offline API. The offline API uses the `postMessage` functionality to send messages to the
offline client and the `window.addEventListener` functionality to receive messages from the client.

To register to receive messages from the client, you should first have a function that will run
every time a message is received. Messages sent from the offline client will always have a `type`
and a `payload`. The types will be one of the ones defined above.

```javascript
const receiveMessage = event => {
  const { data } = event;
  try {
    const message = JSON.parse(data);

    const { type, payload } = message;

    // do something with the payload given the type
    // ...

  } catch (err) {
    console.error(err);
  }
}
```

Once you have your `receiveMessage` handler, you need to register it to listen to the `'message'`
event. Hence the following code should run once in the app.

```javascript
// if offline, we need to set up the listeners here
if (offline) {
  window.addEventListener('message', receiveMessage);
}
```

Every time the app receives a message, the `receiveMessage` handler will be called and it can
update itself accordingly.

Sending a message is a very similar process. Wherever your app is requesting information from the
online API, you can include a conditional so that if the app is in an offline context, it can
request from the offline API instead by posting a message using `postMessage`.

For this it needs to include the `type`, which is one of the `PostMessageType` strings outlined
above, as well as a payload, which is similar to that of the online API, but might include some
extra details.

Currently, the following `postMessage` calls are supported.

To get the `AppInstance`, you post a message of type `GET_APP_INSTANCE`, along with the ID of
the `AppInstance`, `Space` and `SubSpace`, which have been passed down through the url.


```javascript
// example offline api call to get the app instance
if (offline) {
  return postMessage({
    type: GET_APP_INSTANCE,
    payload: {
      id: appInstanceId,
      spaceId,
      subSpaceId,
    },
  });
}
```

To get the all `AppInstanceResource` objects, you post a message of type
`GET_APP_INSTANCE_RESOURCES`, along with the optional `type` of `AppInstanceResource`, as well as
the IDs of the `AppInstance`, `Space` and `SubSpace`, which have been passed down through the url.

```javascript
// example offline api call to get the app instance resources
if (offline) {
  return postMessage({
    type: GET_APP_INSTANCE_RESOURCES,
    payload: {
      type,
      spaceId,
      subSpaceId,
      appInstanceId,
    },
  });
}
```

To create an `AppInstanceResource`, you post a message of type `POST_APP_INSTANCE_RESOURCE`,
along with the `data`, optional `type` and `format` of `AppInstanceResource`, as well as mandatory
IDs of the `Space`, `SubSpace`, `AppInstance` and `User`, which have been passed down through the
url.

```javascript
// example offline api call to create an app instance resource
if (offline) {
  return postMessage({
    type: POST_APP_INSTANCE_RESOURCE,
    payload: {
      data,
      type,
      format,
      spaceId,
      subSpaceId,
      appInstanceId,
      userId,
    },
  });
}
```

To update an `AppInstanceResource`, you post a message of type `PATCH_APP_INSTANCE_RESOURCE`,
along with the `data` and the IDs of the `AppInstanceResource`, `Space`, `SubSpace`,
`AppInstance`, which have been passed down through the url.

```javascript
// example offline api call to patch an app instance resource
if (offline) {
  return postMessage({
    type: PATCH_APP_INSTANCE_RESOURCE,
    payload: {
      id: appInstanceResourceId,
      spaceId,
      subSpaceId,
      appInstanceId,
      data,
    },
  });
}
``` 
