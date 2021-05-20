---
layout: post
title: State Management
date: 2021-05-19 18:37 +0000
author: alfred_dsouza
categories:
  - blog
  - react
share: true
image:
  path: /images/what-is-state-management.jpg
  caption: "What is state management"
---

## What is state management
From the previous [post](https://dsouzaalf.red/blog/react/what-is-state/ "What is state") we know what is state, now let's try to understand what is state management.

> State management is how we manage the application state, that's it!

## Why is state management difficult

It’s important that whatever the source of this our state:
- It is always the single source of truth
- It always has the latest values
- UI and data are always in sync

Handling these things in the most efficient way is complex. For a small app we maybe able to handle it without a library but as the application grows so does the state and the complexity of handling the state and keeping the UI & state in sync.

Things can become complicated and difficult very fast, that is why we have libraries like Redux, RxJs and others that help us implement state management.

## React and state management
React(version 16.8 and above) provides us with tools like `useState` and `useReducer` that help us manage state. And most of the times these should get you a long way, but sometimes you will have to look at other options like Redux or Recoil or some other library.

* Hooks like useState & useReducer can only be used inside a function component.

## Example
Let's take a look at a simple example, we will have a div, with two buttons. One button will show/hide the div and the second button will start rotating the div.

First the html:
```html
<!-- example.html-->
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Example</title>
    <style media="screen">
      #content {
        margin: 20px;
        width: 100px;
        height: 100px;
        background: #d99e9e;
        padding: 10px;
      }
      .content-show {
        display: block;
      }
      .content-hide {
        display: none;
      }
      .spinner {
        animation-name: spin;
        animation-duration: 4000ms;
        animation-iteration-count: infinite;
        animation-timing-function: linear;
      }
      @keyframes spin {
        from { transform:rotate(0deg); }
        to { transform:rotate(360deg); }
      }
    </style>
  </head>
  <body>
    <div id="buttons">
      <button id="toggler" onclick="handleToggle();">Toggle Content</button>
      <button id="spinner" onclick="handleSpin();">Toggle Spin</button>
    </div>
    <div id="content" class="content-show">
      This will be toggled.
    </div>
  </body>
</html>
```
We have two buttons, first button to show/hide the `content` div and the second button to spin the `content` div. We call some function `onclick` (we will add these functions in a moment).
We also have a bit of styles going for the `content` div and then a `.spinner` class to add the spinning animation.

Next let's add some *state*. Just before the body tag ends, we add a script tag. In there we define a variable called `state` and this `state` is an object.
```html
<!-- example.html-->
<script type="text/javascript">
  var state = {
    isContentHidden: false,
    isSpinning: false,
  }
</script>
```
We are using an object as our state store and we call it `state`. Our object has two keys `isContentHidden` and `isSpinning` to track if the content div is visibility and if it is spinning.

Next let's add a function to show hide the content.
```html
<!-- example.html-->
<script type="text/javascript">
  function handleToggle() {
    // get content div
    var content = document.getElementById('content');

    if(state.isContentHidden) {
      // show content
      content.classList.remove('content-hide');
    } else {
      // hide content
      content.classList.add('content-hide');
    }

    state.isContentHidden = !state.isContentHidden;
  }
</script>
```
In this function we are checking the value of `state.isContentHidden` and depending on the current value we add or remove the `content-hide` class on the `content` div.
And on the last line we are updating the value in our state.

Next let's handle spinning our content.
```html
<!-- example.html-->
<script type="text/javascript">
  function handleSpin() {
    // get content div
    var content = document.getElementById('content');
    // get the spinner button
    var spinner = document.getElementById('spinner');

    if(state.isSpinning) {
      // remove class
      content.classList.remove('spinner');
      // change button label
      spinner.innerText = 'Start spinning';
    } else {
      // add class
      content.classList.add('spinner');
      // change button label
      spinner.innerText = 'Reset';
    }

    state.isSpinning = !state.isSpinning;
  }
</script>
```
Just like our previous function here too we perform some action depending on the value in state. In this function we check the value of `state.isSpinning` and then if it is `true` we add the `spinner` class and if it is `false` we remove the `spinner` class.

This is a very simple and small example but hopefully you see how state management works.

Next time we will have a look at `useState`.

<hr>
> Photo by <a href="https://unsplash.com/@robsonhmorgan?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Robson Hatsukami Morgan</a> on <a href="https://unsplash.com/">Unsplash</a>
