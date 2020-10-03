---
layout: post
title: JavaScript Event Delegation
date: 2015-08-12 11:15 +0100
author: alfred_dsouza
categories:
  - blog
  - javascript
share: true
---

In our previous post we saw event [`delegation using jQuery`](https://dsouzaalf.red/blog/jquery/jquery-event-delegation/ "jQuery Event Delegation "), in this post we will see JavaScript event delegation.

Make sure you check these two posts before we start with this one.

Dynamically Add content to [`DOM using JavaScript`](https://dsouzaalf.red/blog/javascript/dynamically-add-content-to-dom-using-javascript/ "Dynamically Add content to DOM using JavaScript ")
Dynamically remove content from [`DOM using JavaScript`](https://dsouzaalf.red/blog/javascript/dynamically-remove-content-from-dom-using-javascript/ "Dynamically remove content from DOM using JavaScript ")

Let’s get started with our HTML :

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <title>Add Remove Text-boxes</title>
    </head>
    <body>
        <H1>Add Remove Text-boxes</H1>
        <button id="btn-add-textbox">Add Textbox</button>
        <div id="div-add-remove">

        </div>
    </body>
</html>
```

We have a button(`btn-add-textbox`) to add text-boxes to our div(`div-add-remove`). That’s about it with HTML. Next we will add JavaScript to add text-boxes.

```javascript
var getButton = document.getElementById('btn-add-textbox');
var getDiv = document.getElementById('div-add-remove');
getButton.addEventListener('click',function(e){
    var divToAdd = document.createElement('div');
    divToAdd.className = 'magic-div';
    var inputToAdd = document.createElement('input');
    inputToAdd.type = 'text';
    inputToAdd.className = 'magic-text-box';
    var spanToAdd = document.createElement('span');
    spanToAdd.className = 'remove-textbox';
    spanToAdd.innerHTML  = ' x';
    divToAdd.appendChild(inputToAdd);
    divToAdd.appendChild(spanToAdd);
    getDiv.appendChild(divToAdd);
});
```

That looks like lot of code for adding a simple text-box, but all we are doing is constructing a template and adding it to our div.

First we get our button (`getButton`) and div (`getDiv`). Next we ask our button(`getButton`) to listen for a click. Here is what we do once our button hears a click :

We create([`createElement`](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement "MDN .createElement documentation")) a `div` element(divToAdd) and give it a class([`className`](https://developer.mozilla.org/en-US/docs/Web/API/Element/className "MDN .className documentation")) of `magic-div`
Next we create([`createElement`](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement "MDN .createElement documentation")) a ‘input’ element(inputToAdd), give it a type of ‘text’ and class([`className`](https://developer.mozilla.org/en-US/docs/Web/API/Element/className "MDN .className documentation")) of ‘magic-text-box’
Then we create([`createElement`](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement "MDN .createElement documentation")) a ‘span’ element(spanToAdd), give it a class([`className`](https://developer.mozilla.org/en-US/docs/Web/API/Element/className "MDN .className documentation")) of `remove-textbox` and add text(‘x’)(innerHTML) to this span.
Then we append([`appendChild`](https://developer.mozilla.org/en-US/docs/Web/API/Node/appendChild "MDN .appendChild documentation")) the ‘input’ element(inputToAdd) and ‘span’ element(spanToAdd) to the ‘div’ element(divToAdd).
Lastly we append([`appendChild`](https://developer.mozilla.org/en-US/docs/Web/API/Node/appendChild "MDN .appendChild documentation")) the ‘div’ element(divToAdd) to getDiv(div-add-remove).

In short we create a template and append the template to the div. Now let’s look at the next part of our problem, removing text-boxes.

According to the template structure, we will have to click on the span(`spanToAdd`) to remove the text-box (we will remove the entire template div for that text-box). This span(`spanToAdd`) does not exist on page load, hence JavaScript does not know that it exist. So we will use event delegation to make sure this span can listen for an event.

```javascript
var getDiv = document.getElementById('div-add-remove');
getDiv.addEventListener('click',function(e){
    if( e.target.className == 'remove-textbox' ) {
        var getParentElement = e.target.parentElement;
        getParentElement.remove();
    }
});
```

## JAVASCRIPT EVENT DELEGATION

In event delegation, we have to add the event listener to an element closest to the ‘span’ and this element should exist in the DOM on document load. In our example ‘div-add-remove’ will be that element. So we ask ‘div-add-remove'(getDiv) to listen for a click. Once it hears a click we

check if the target class is `remove-textbox` (that’s the class given to our span)
If that is the case we get the [`parentElement`](https://developer.mozilla.org/en/docs/Web/API/Node/parentElement "MDN .parentElement documentation") of this element (to get the complete template) remove parentElement.
And that is all there is to JavaScript Event Delegation. We can also do something like, at a time max 10 text-boxes can only exists in the div. And when removing at-least one text-box should always exist in the div

Get full code on [github](https://github.com/dsouzaalfred/blogdemos/blob/master/add_remove_element/js.html "Github link").
