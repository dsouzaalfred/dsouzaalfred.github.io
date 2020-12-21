---
layout: post
title: What is state
date: 2020-12-20 12:01 +0100
author: alfred_dsouza
categories:
  - blog
  - react
share: true
image:
  path: /images/what-is-state.jpg
  caption: "What is state"
---

As frontend developers we keep hearing about __state__, and it can be confusing to begin with. When I started out I had no clue that such a thing existed. It took me sometime to figure out this __state__ thing. In this post, let's try and understand what is __state__.

## So what is state?
__State__ is the data that represents the current state of your UI. Key thing to note is that it is the __data__ not the actual UI(DOM). This __data__ is then used to render the UI correctly.

## Examples
Let's take a look at couple of examples:
#### Network call :
The App will go through these states:
  - `isLoading` (is the network call in progress)
  - `isSuccess` (is the network call a success)
  - `isError` (if the call returned an error)

Now depending on any of these states our UI will change, as an example
  - if `isLoading` is `true` we show the loading animation
  - if `isSuccess` is `true` we hide the loading animation and show the response
  - if `isError` is `true` we hide the loading animation and show the error message

#### Form submission :
  - `isValid` (is the form valid/all the fields are filled in correctly)
  - `isSubmitted` (is the form submitted)

When the user clicks on submit
  - If `isValid` is `true` we submit the form else show an error
  - If `isSubmitted` is true we hide the form and show a message that form is submitted
  (This is just an example, in the real world you might submit the form by making a network call
    or each field can have it's own state to check if it's valid and capture the value.)

## When does the state update?
1. Every action that the user performs in your app, will update the __state__ and this in turn will update the UI.
Examples of user actions:
  - route change
  - focus on a input field
  - submit a form
2. Side effects after the initial __state__ change, like network call after route change.
3. Push notification, to show the user that there is a new notification or update.

That's all for today, next time we have a look at state management.

<hr>
> <span>Cover photo by <a href="https://unsplash.com/@nate_dumlao?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Nathan Dumlao
</a> on <a href="https://unsplash.com/">Unsplash</a></span>
