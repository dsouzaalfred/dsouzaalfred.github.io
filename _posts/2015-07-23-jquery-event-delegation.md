---
layout: post
title: jQuery Event Delegation
date: 2015-07-23 11:15 +0100
author: alfred_dsouza
categories:
  - blog
  - jQuery
share: true
---

jQuery Event Delegation allows us to attach an event listener to a parent element, and this event will fire for all descendants matching the selector we pass.

The example in this post, will use concepts from our previous posts about [`dynamically adding`](https://dsouzaalf.red/blog/jquery/dynamically-add-content-to-dom-using-jquery/ "Dynamically Add content to DOM using jQuery") and [`removing`](https://dsouzaalf.red/blog/jquery/dynamically-remove-content-from-dom-using-jquery/ "Dynamically remove content from DOM using jQuery") content from DOM using jQuery. And we will add in a bit of jQuery Event Delegation.

So like always lets start with HTML :
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <title>Add Remove Text-boxes</title>
        <script src="http://code.jquery.com/jquery-2.1.4.min.js"></script>
    </head>
    <body>
        <H1>Add Remove Text-boxes</H1>
        <button id="btn-add-textbox">Add Textbox</button>
        <div id="div-add-remove">

        </div>
    </body>
</html>
```

We have a button(`btn-add-textbox`) to add text-boxes to our div(div-add-remove) and we have inserted jQuery using a [CDN](https://code.jquery.com/ "jQuery CDN"). That is about it with the HTML part. Let’s get working on jQuery.

First up we will construct a template(`inputTemplate`), this template will be [`appended`](http://api.jquery.com/append/ "jQuery .append documentation") to our div(`div-add-remove`) when our button(`btn-add-textbox`) is clicked.

```javascript
var inputTemplate = '<div>';
    inputTemplate += '<input type="text" class="magic-text-box" />';
    inputTemplate += ' <span class="remove-textbox">x</span>';
    inputTemplate += '</div>';
```

On the first line we define a [`variable`](https://api.jquery.com/Types/ "jQuery .variable documentation") using `var` and name our variable `inputTemplate`, also assign the opening div to this variable.
On the next line we add the text-box to our existing template using `+=`
Then we add a `span` element, we will use it to remove the text-boxes.
And lastly we close the ‘div’

Here is what our template looks like :

```html
<div>
    <input type="text" class="magic-text-box" />
    <span class="remove-textbox">x</span>
</div>
```

Next we ask our button(`btn-add-textbox`) to listen for a click. And when it hears a click we [`append`](http://api.jquery.com/append/ "jQuery .append documentation") our template(`inputTemplate`) to our div(`div-add-remove`).

```javascript
$('#btn-add-textbox').on('click',function(event){
    $('#div-add-remove').append(inputTemplate);
});
```

Adding text-box is done, now lets work on removing text boxes

## jQuery Event Delegation

Now removing a text-box using our `span` will be a bit tricky. This is because, our text-box and span do not exist in the DOM on page load(this is the time our script is loaded). So our script does not know about these elements and will not be able to attach an event listener to these elements.

To solve this problem, we will use jQuery Event Delegation.

Let’s get going then :

```javascript
$('#div-add-remove').on('click','.remove-textbox', function(){
        $(this).parent('div').remove();
});
```

What did we do here? :

We attached the event listener to our div(`div-add-remove`), we do this for two reasons
1. Our span element will be inside this div
2. This div is the closest element to our span that will exist in the DOM when our script is loaded.
We used the [`.on()`](http://api.jquery.com/on/ "jQuery .on documentation") method to help us with delegation
We ask the div to listen for a ‘click’
On the elements with `remove-textbox` class

Once we hear a click :

`$(this)` is used to refer to the element that triggered the event. In our case this will be our `span`
Get the [`parent`](https://api.jquery.com/parent/ "jQuery .parent documentation") `div` of our `span`.
Remove the parent div, since our text-box and span are inside the div

And that’s how you use jQuery event delegation. Of course you could do more with the code. Like limit the number of text-boxes that can be added to 10 or make sure that at-least one text-box is always present in the div.

```javascript
$('#btn-add-textbox').on('click',function(event){
    if( $('#div-add-remove').find('div').length < 10 ){
        $('#div-add-remove').append(inputTemplate);
    }
});

$('#div-add-remove').on('click','.remove-textbox', function(){
    if( $('#div-add-remove').find('div').length > 1 ){
        $(this).parent('div').remove();
    }
});
```

When using jQuery event delegation you have to worry about event bubbling or event propagation. That will be a topic for some other day. To know more about event delegation you head [`here`](http://learn.jquery.com/events/event-delegation/ "jQuery .here documentation").

Get full code on [github](https://github.com/dsouzaalfred/blogdemos/blob/master/add_remove_element/jQuery.html "Github link").
