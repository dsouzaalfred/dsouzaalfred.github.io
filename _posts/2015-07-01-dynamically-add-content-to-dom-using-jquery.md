---
layout: post
title: Dynamically Add content to DOM using jQuery
date: 2015-07-01 11:15 +0100
author: alfred_dsouza
categories:
  - blog
  - jQuery
share: true
---

I love it when magicians conjure things out of thin air. A dove, a rabbit you name it and it’s there. Sure they have their tricks but what’s amazing is how it’s presented.

As web developers, sometimes we are required to conjure elements and add them to the DOM. Be it  an error span or an addition textbox or an additional div, using our wand (jQuery) we can perform this trick with ease.

Powerful wizards can even perform magic without wands (using only JavaScript).

How to perform this WAND-LESS magic see [here](https://dsouzaalf.red/blog/javascript/dynamically-add-content-to-dom-using-javascript/ "Dynamically Add content to DOM using JavaScript").

Let me  first define our trick, so we know exactly what we are to do. We will add a textbox to a div every time a button is clicked.

Lets have our DOM ready.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Add textboxes</title>
    <script src="http://code.jquery.com/jquery-2.1.4.min.js"></script>
  </head>
  <body>
    <h1>Add Textboxes</h1>
    <div id="div-add-textbox-here">

    </div>
  <button id="btn-add-textbox">Add Textbox</button>
  </body>
</html>
```

Nothing fancy here. We have an empty div and a button. So we have two parts of our trick in place: a button and a div. We have also kept our wand ready. Pretty neat, we are all set to start our trick.

First listen for the button click. We will need a magic spell [`.on()`](https://api.jquery.com/on/ "jQuery .on documentation").

```javascript
$('#btn-add-textbox').on('click',function(event){

});
```

We are using jQuery’s `.on()` method to handle the `click` event on our button `btn-add-textbox`.

Now that we are listening for a click, what should we do when the user clicks? Add a text box! Time for another magic spell [`.append()`](https://api.jquery.com/append/ "jQuery .append documentation").

```javascript
$('#btn-add-textbox').on('click',function(event){
  $('#div-add-textbox-here').append('<input type="text" class="magic-text-box" />');
});
```

`.append()` will insert content to the end of our div.

Thats it! we append a textbox to our div `div-add-textbox-here`. So every time a user clicks on the button a text box will be added to the div.

We can do a few more tricks here like, limiting the number of textboxes to ten.

```javascript
$('#btn-add-textbox').on('click',function(event){
  if( $('#div-add-textbox-here').find('input').length < 10 ){
    $('#div-add-textbox-here').append('<input type="text" class="magic-text-box" />');
  }
});
```

[`.length`](https://api.jquery.com/length/ "jQuery .length documentation") returns the number of elements currently matched.

[`.find()`](https://api.jquery.com/find/ "jQuery .find documentation") method will get descendants and filter the elements we want.

So we ask jQuery to find all inputs (textboxes) inside our div. And if the number of textboxes (.length will give the count) is less than 10 only then will we add another textbox. Neat little trick rite?.

We can use this same trick to add ‘options’ to ‘select’ or add any other element to the DOM.

With your wand (jQuery) and a few magic spells we can do all possible tricks.

Get full code on [github](https://github.com/dsouzaalfred/blogdemos/blob/master/add_element/jQuery.html "Github link").
