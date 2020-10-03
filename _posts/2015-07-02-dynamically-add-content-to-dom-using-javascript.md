---
layout: post
title: Dynamically Add content to DOM using JavaScript
date: 2015-07-02 11:15 +0100
author: alfred_dsouza
categories:
  - blog
  - javascript
share: true
---

We have seen how our wand (jQuery) can be used to [Dynamically Add content to DOM](https://dsouzaalf.red/blog/jquery/dynamically-add-content-to-dom-using-jquery/ "Dynamically Add content to DOM using jQuery "). But then there are powerful wizards who do not like to use wands for such small tricks. Here is how you perform the same trick with pure magic (JavaScript).

First things first, lets start with our HTML

```html
<!DOCTYPE html>
<html lang="en">
       <head>
              <meta charset="utf-8">
              <title>Add textboxes</title>
       </head>
       <body>
              <h1>Add Textboxes</h1>
              <div id="div-add-textbox-here">

              </div>
              <button id="btn-add-textbox">Add Textbox</button>
       </body>
</html>
```

Simple HTML page. With an empty div (`div-add-textbox-here`), textboxes will be added to this div. A button (`btn-add-textbox`) to trigger the text box addition. And that’s about it.

Lets start with the magic.

```javascript
var getButton = document.getElementById('btn-add-textbox');
getButton.addEventListener('click', function(){

});
```

First we summon the button (`btn-add-textbox`) and then tell the button to listen for a `click` using [`addEventListener`](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener "MDN addEventListener documentation"). Next we will tell the button what to do when it hears a click.

```javascript
getButton.addEventListener('click', function(){
       var getDiv = document.getElementById('div-add-textbox-here');
       var newInput = document.createElement('input');
       newInput.type = "text";
       newInput.className = "magic-text-box";
       newInput.value = getDiv.children.length + 1;

       getDiv.appendChild(newInput);
});
```

We create a new element of type `input` using [`createElement`](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement "MDN createElement documentation")  and do the following :

We need an input box so  we tell the element that it will be of type `text`.
Then tell the element that will be of class `magic-text-box` (this is just for styling).
Lastly we tell the element what its value will be.

We use `getDiv.children.length` to get a count of all elements inside `getDiv` and add one to that count (`getDiv.children.length + 1`).

So on the first click, there are zero elements inside `getDiv`. Therefore `0 + 1 = 1`, hence element will get value 1. So on and so forth.

Now we are done setting up our textbox, we add it to `getDiv`.

And that’s it. Of-course we can do lot of things here. Like we can restrict a user to add only 10 textboxes.

```javascript
var getButton = document.getElementById('btn-add-textbox');
getButton.addEventListener('click', function(){
       var getDiv = document.getElementById('div-add-textbox-here');
       if( getDiv.children.length < 10 ){
              var newInput = document.createElement('input');
              newInput.type = "text";
              newInput.className = "magic-text-box";
              newInput.value = getDiv.children.length + 1;

              getDiv.appendChild(newInput);
       }
});
```

Here before adding a textbox we check if the number of elements inside `getDiv` (`getDiv.children.length`) is less then 10 only then we add the textbox.

Get full code on [github](https://github.com/dsouzaalfred/blogdemos/blob/master/add_element/js.html "Github link").
