---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

search: true
---

# Introduction

Welcome to the Triangle comparator App Documentation! This App based source code has been forked from [react-epfl/graasp-app-starter-react](https://github.com/react-epfl/graasp-app-starter-react)

The main goal is compares two triangles based on: `points coordinates, angles or sides`.

For our first version we can only test triangles with `x` and `y` coordinates of each triangles point and tell if they are similar or not. In our next version we will be adding the possibility to compare triangles using `Angles` or `Sides`.

This Triangles comparator documentation page was created with [Slate](https://github.com/lord/slate).

This source code is divided into several components.
```
common
forms
preview
```

The `static propTypes` will be used for all changes validation in certain classes.

```shell
static propTypes = {
  ...
}

```

# Initial Structure

> This is our main Code structure:

```shell
# With shell, you can just pass the correct header with each request
Main "https://github.com/react-epfl/graasp-app-starter-react"
  .idea
  public
    index.html
    favicon.ico
    manifest.json
  scripts
    setup.sh
  src
    common  
      Error.js
    student
      StudentView.js
    teacher
      TeacherView.js
    App.css
    App.js
    App.test.js
    index.css
    index.js
    logo.svg
    registerServiceWorker.js
  .editorconfig
  .eslintignore
  .gitignore
  .huskryc
  .npmrc
  CHANGELOG.md
  LICENSE
  README.md
  commitlint.config.js
  package.json
  yarn.lock
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

The `student and teacher` folders are the template rendering student and teacher view initially that we will have to modify later in our case.

Firstly we will have to work on the `Student view` since only students are going to learn about triangles now.

# Components

## common

This folder only contains our `Triangles Comparator Button Class` that handle all triangles datas and check if the two triangles are similar or not.

### Our initial state

Here we initialise the default state for all calculated values from our `SimulationButtons` class.

The `flash` params handle when the flash message should be displayed or not;

The `visible` params handle when to display the `Alert` on the page since it should be displayed only when a user clicks on the button and will disappear when click on it close button.

Finally the `success` is the `Object` that contain the calculated values.

> This is our main Code structure:

```shell
constructor(props) {
  super(props);
  this.state = {
    flashed: props.flashed,
    visible: true,
    success: {
      value1: '',
      value2: '',
      value3: '',
    },
  };
  this.onDismiss = this.onDismiss.bind(this);
}
```
### handleSimulate: function()

This function is called when the Compare button is clicked from the triangles view. It get all the coordinates for each point. Basically we have Triangle `ABC` and `DEF` so for the first triangle points coordinates we have: `A(x, y), B(x, y), C(x, y)` and for the second one we have: `D(x, y) , E(x, y), F(x, y)`. Then from these point `x` and `y` coordinates, we calculate the distance between each point respectively `AB, AC, BC` for the triangle `ABC` and `DE, DF, EF` for the triangle `DEF`. Then we divide each distance side by side and save the results into our `application state`

> Our handleSimulate function:

```shell
handleSimulate = () => {
  ...
}
```
### handleMessage: function()

This function recover the calculated results from our `application state` and check if they are equal then render a `flash message` with value: `Triangle ABC DEF are similar` else `Triangle ABC and DEF are not similar`
> Our handleMessage function :

```shell
handleMessage = () => {
  ...
}
```

## forms

This folder contains Dimensions and FormView Classes.

The `Dimension` class is in charge of just displaying the title `Triangle ...` for each triangle, the corresponding form and also the triangle tree.
Within it `constructor`, we define the default triangle point coordinates `x` and `y` value as well.

The `FormView` class contains a table with all input fields used to set each coordinates as well and also the buttons to rotate left or right or to shift our triangle to left or right based on student choice. It will pass it to our `Dimensions` Class to render the `Table`. As we have multiple input that are all similar, we created our `TableDatas` Component that return a single `td` with the right inputs.

We then handle the form input changes with the `handlePChange` function that we pass to our form Component.

> Our Dimensions constructor

```shell
constructor(props) {
  super(props);
  this.state = {
    rotated: false,
    points: this.props,
  };
}
```

> Our FormView constructor

```shell
constructor(props) {
  super(props);
  this.state = {
    rotated: this.props,
    points: this.props,
  };
}
```

### handlePointChange function()

This function is called when all our different form input value change; then check if the value is empty, replace it by 0 since the input can not be null in our case, and fill in an input by 300 when the value is higher than 300. Once these controls are completed, it then passes all the new coordinates to it parent witch is our `Dimension` class by calling the `handlePChange` function and sending params: `handlePChange(newPoints)`

```shell
handlePointChange = (event) => {
  ...
}
```

### handleShiftRight function()
Here we, start by increasing all coordinates by 20, then we check the first Point that x coordinates has reached 300 and then we stop increasing the other point `x` coordinates values to avoid getting the triangle out of the box.

```shell
handleShiftRight = (event) => {
  ...
}
```
### handleShiftLeft function()
Unlike to the previous, we will just need to decrease by 20 and then stop when we found the first point that has it `x` coordinate value less than 20.

```shell
handleShiftLeft = (event) => {
  ...
}
```
### handleRotate function()
For the Rotation, we firstly get the middle of the triangle then make the rotation or 90 degree.

```shell
handleRotate = (event) => {
  ...
}
```

## preview
Here we just import [react-konva](http://konvajs.github.io) library we used to draw our triangle. This folder contains our Tri class that draw and display our Triangle. The `Text` tag helped us to append our triangle laters to eat point at a specific coordinate.

```shell
const Tri = ({ color, node, points }) => (
  <Layer>
    ...
  </Layer>
);
export default Tri;
```

# Student View
Basically our have Two different views: student and teacher's one. But currently all passes in the student view
From here we just call our Dimension Class then pass all datas it needs to such as: the triangle, the translation, the update method, the triangles nodes as well as the related colors. We also pass the translation, triangles and flash parameters to our Simulation button class to automatically handle all changes.

```shell
const StudentView extends Component {
  static propTypes = {
    ...
  }

  constructor(props) {
    ...
  }
}
export default StudentView;
```

# Teach View

For the moment our Teacher view just contain a welcome message nothing else. But we will certainly update it as soon as possible. But we pass the `t` in params to allow the translation function works.

```shell
const TeacherView = ({ t }) => (
  <Layer>
    ...
  </Layer>
);
export default TeacherView;
```

# App.js

This is the core App that handle our teacher and student views and render the corresponding. But default, we just set the student View as default one. So when our App loads, we see the student view that contains all the other stuffs. Note that in `React JS` everything in our App should be in separated components.

# index.js

Everything begins from here. The main parent that import our App.js, our style files and all necessary files we need on our App initialisation.

# Translation
We used the [react-i18next](https://github.com/i18next/react-i18next) library for the translation feature. But all our translation words are located in our `translate.json` file. We use the `t` params in all our components and classes to call the translation function, then we pass it the requested word for the translation to render the right text based on the params.
