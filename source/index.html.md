---
title: Developer Resources

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

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
