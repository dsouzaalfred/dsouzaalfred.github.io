---
layout: post
title: Dynamically remove content from DOM using jQuery
date: 2015-07-07 11:15 +0100
author: alfred_dsouza
categories:
  - blog
  - jQuery
share: true
---

Another magic trick that I love most is when objects disappear. Specially pretty ladies, I wonder what magicians do with them.

If magicians can make objects disappear, so can we. But we can only make elements disappear from our DOM using jQuery.

Check this [post](https://dsouzaalf.red/blog/javascript/dynamically-remove-content-from-dom-using-javascript/ "Dynamically remove content from DOM using JavaScript") to see how this can be done using JavaScript

Let's define our trick : We will remove textboxes from a div every time a button is clicked.

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="utf-8">
		<title>Remove textboxes</title>
		<script src="http://code.jquery.com/jquery-2.1.4.min.js"></script>
	</head>
	<body>
		<h1>Remove Textboxes</h1>
		<div id="div-textbox-here">
			<input type="text" class="magic-text-box" />
			<input type="text" class="magic-text-box" />
			<input type="text" class="magic-text-box" />
			<input type="text" class="magic-text-box" />
		</div>

		<button id="btn-remove-textbox">Remove Textbox</button>
	</body>
  </html>
```

We have a div (`div-textbox-here`) with four textboxes. We also have a button (`btn-remove-textbox`). When a user clicks on this button we will remove the first textbox.

We use our [`.on()`](http://api.jquery.com/on/ "jQuery .on documentation") spell to listen when the button is clicked.

```javascript
$('#btn-remove-textbox').on('click',function(event){

});
```

What do we do next, remove the first textbox from the div.

```javascript
$('#btn-remove-textbox').on('click',function(event){
	$('#div-textbox-here').find('input').first().remove();
});
```

We have our button listening for a click. And as soon as it hears a click, it will

- Go to the div (`div-textbox-here`)
- [`find()`](https://api.jquery.com/find/ "jQuery .find documentation") all input elements
- Get the [`first()`](https://api.jquery.com/first/ "jQuery .first documentation") input element
- And [`remove()`](https://api.jquery.com/remove/ "jQuery .remove documentation") it

And like always we can extend this the way we want. Like we can make sure that there is always at least one element present in the div.

```javascript
$('#btn-remove-textbox').on('click',function(event){
	if( $('#div-textbox-here').find('input').length > 1 ){
		$('#div-textbox-here').find('input').first().remove();
	}
});
```

This is what we do here

- Go to the div (`div-textbox-here`)
- [`find()`](https://api.jquery.com/find/ "jQuery .find documentation") all input elements
- Check if number([length](https://api.jquery.com/length/  "jQuery .length documentation")) of input elements is greater than 1
- If yes then get the [`first()`](https://api.jquery.com/first/ "jQuery .first documentation") input element
- And [`remove()`](https://api.jquery.com/remove/ "jQuery .remove documentation") it

Get full code on [github](https://github.com/dsouzaalfred/blogdemos/blob/master/remove_element/jQuery.html "Github link").
