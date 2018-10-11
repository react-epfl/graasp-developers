---
title: Graasp Get Started With React

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

Also, we will help you well understand the building blocks of React apps: elements and components.

You can view code examples in the dark area to the right.

This guide is separated into several parts: <br>
- Forking the initial repository <br>
- Installing dependencies & Starting the application <br>
- Setting linting `eslint-plugin-react` <br>
- Testing the App
- Adding your own dependencies <br>
- Updating dependencies

# Lab

## Forking the initial repository

This is the quickest way to get started!
First, open the [graasp/react-get-started-app](https://github.com/react-epfl/graasp-app-starter-react) link in a new tab. Under the repository name, click Clone or download.

> You can also just clone using SSH or HTTPS

```shell
  git clone git@github.com:react-epfl/graasp-app-starter-react.git
```

## Installing dependencies & Starting the application

To install the application dependencies, <br>
1- Open your `Terminal` <br>
2- Navigate to the cloned of downloaded project directory or folder <br>
3- Run `yarn install`. But make sure you already have yarn installed on your development environment for this. <br>

To start your development server, run `yarn start` when all installations is completed and you're done.
This script executes a Webpack development server with force reloading enabled. Then your server keep listening on all your modified files and reload your browser as well to apply changes an asynchronous way running on the port `3000` by default.

Then navigate to `localhost:3000` to preview your application running.


## Setting linting `eslint-plugin-react`

ESLint is a tool for identifying and reporting on patterns found in ECMAScript/JavaScript code. Normally, it is configured by default (you can see the configuration [here](https://github.com/eslint/eslint)). Once you installed it, by restarting your server, you will see all synthax issues rendered in the terminal as well as the browser console.

> In case you want to enforce a coding style, you can just use this tho disable eslint controls for a particular section or lines of code.

```shell
  // eslint-disable-next-line no-param-reassign
```

## Testing the App

To run tests just execute `yarn run test`. Note that the tests are also asynchronous. Then every time you save a file, the tests are re-run. You can read more about react testing [here](https://github.com/kentcdodds/react-testing-library).
