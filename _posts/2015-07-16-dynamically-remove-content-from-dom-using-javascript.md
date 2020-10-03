---
layout: post
title: Dynamically remove content from DOM using JavaScript
date: 2015-07-16 11:15 +0100
author: alfred_dsouza
categories:
  - blog
  - javascript
share: true
---

We have seen how jQuery can be used to [remove elements from DOM](http://dsouzaalf.red/blog/jquery/dynamically-remove-content-from-dom-using-jquery/ "Dynamically remove content from DOM using jQuery"). Now let us see how we can Dynamically remove content from DOM using JavaScript.

Like always let us start with HTML

```html
<!DOCTYPE html>
<html lang='en'>
	<head>
		<meta charset='utf-8'>
		<title>Remove textboxes</title>
	</head>
	<body>
		<h1>Remove Textboxes</h1>
		<div id='div-textbox-here'>
			<input type='text' class='magic-text-box' value="1" />
			<input type='text' class='magic-text-box' value="2" />
			<input type='text' class='magic-text-box' value="3" />
			<input type='text' class='magic-text-box' value="4" />
		</div>
		<button id='btn-remove-textbox'>Remove Textbox</button>
	</body>
</html>
```

Nothing fancy here, we have a simple HTML page with four text-boxes(`magic-text-box`) inside a div (`div-textbox-here`) and a button(`btn-remove-textbox`) to remove those text-boxes.

That’s all the HTML we need for now. Let’s call our button and ask it to listen for a click.

```javascript
var getButton = document.getElementById('btn-remove-textbox');
getButton.addEventListener('click',function(){

});
```

So here we first call([`getElementById`](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementById "MDN .getElementById documentation")) our button(`btn-remove-textbox`) and ask it to listen([`addEventListener`](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener "MDN .addEventListener documentation")) for a `click` event. Next we will tell the button what it has to do once it hears a `click`.

```javascript
var getButton = document.getElementById('btn-remove-textbox');
getButton.addEventListener('click',function(){
	var getDiv = document.getElementById('div-textbox-here');
	var getInputs = getDiv.getElementsByClassName('magic-text-box');
	getDiv.removeChild(getInputs[0]);
});
```

Once our button(`btn-remove-textbox`) hears a click we ask it to get the div(`div-textbox-here`) that contains all the text-boxes. Once we have the div we get all the text-boxes inside it using class name ([`getElementsByClassName`](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName "MDN .getElementsByClassName documentation")). Remember we have given the same class name(`magic-text-box`) to each of our text-boxes.

[`getElementsByClassName`](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName "MDN .getElementsByClassName documentation") will return an `array` of all the text-boxes with matching class name. Once we have the array, we remove the first element of the array, since we want to remove ([`removeChild`](https://developer.mozilla.org/en-US/docs/Web/API/Node/removeChild  "MDN .removeChild documentation")) the first text-box. Remember in an array ‘0’ is the first element.

And that’s about it. Of-course we can do a lot more. Like making sure that there is at-least one text-box remains in the div(user cannot remove all the text-boxes).

```javascript
var getButton = document.getElementById('btn-remove-textbox');
getButton.addEventListener('click',function(){
	var getDiv = document.getElementById('div-textbox-here');
	var getInputs = getDiv.getElementsByClassName('magic-text-box');
	if( getInputs.length > 1 ){
		getDiv.removeChild(getInputs[0]);
	}
});
```

Same code as before but here we have added an ‘if condition’. This ‘if condition’ will check if the number([`length`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/length  "MDN .length documentation")) of text-boxes is more then one only then remove the first text-box from the array.

And that’s how you Dynamically remove content from DOM using JavaScript.

Get full code on [github](https://github.com/dsouzaalfred/blogdemos/blob/master/remove_element/js.html "Github link").
