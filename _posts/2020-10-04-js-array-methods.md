---
layout: post
title: A foodies guide to JavaScript array methods
date: 2020-10-04 12:01 +0100
author: alfred_dsouza
categories:
  - blog
  - javascript
share: true
image:
  path: /images/react-styling-hero-image.jpg
  caption: "JavaScript array methods"
---


## .map()

The [`map()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map "MDN .map documentation") method takes a function and will call the function once for every element in the array and return a new array with the updated values.

Let's say you are have five dishes served but you like eggs with everything, so you decide to fry eggs and put them on all the dishes. After all eggs make everything good.

So the dishes are our elements inside an array. Frying the egg and putting it on a dish is the function. And `.map()` will repeat the process for us for each dishes.

```javascript

```

Remember
- `.map()` is smart it will not put an egg on an empty plate, there should be a dish there.
- It create a totally new dish so your original dishes (array) is untouched.



## filter

The [`.filter()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter "MDN .filter documentation") method takes a test function and will call the function once on each array and returns a new array of elements that passed the test.

This time you are served a few dishes but you are in no mood to each vegetables. So you check each dish and see if they have vegetables, if they do you don't eat them.

So the dishes are our elements inside an array. Checking each dish if it has vegetables is a function. And `.filter()` will repeat the process on each dish and return all the dishes without vegetables.

```javascript

```

Remember
- If none of the dishes pass your test you can an empty plate(empty array).

## reduce
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce
Take all the ingredients and make a dish

## spread operator
Pot luck
spread operator

## include
The [`.include()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes "MDN .include documentation") method can be used when you want to check if a value exists in an array.

Say you want to check if a restaurant servers your favourite dish.

So the dishes are our elements inside an array. You tell `.include()` which dish you are looking for and it will tell you yes(`true`) or no(`false`).

```javascript
```

## find
The [`.find()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find "MDN .find documentation") method takes a test function and returns the value of the first element that passes the test.

Where `.include()` tells you if a restaurant servers your favourite dish, `.find()` will get you the dish if the restaurant servers it.

So the dishes are our elements inside an array. Checking if the restaurant servers your favourite dish is a function. And `.find()` check each dish and first instance it comes across your favourite dish it will get it for you.

```javascript
```

## findIndex
The [`.fndIndex()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex "MDN .findIndex documentation") method takes a test function and returns the index of the first element that passes the test.

This time you are at a buffet and want to with chocolate cake. So you ask one of the waiters to point you in the direction of chocolate cake.

So the dishes are our elements inside an array. `.findIndex()` is the waiter who takes in what you want and points you to the location where it is.

```javascript
```

## some
The [`.some()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some "MDN .some documentation") method takes a test function and returns true if at-least one element in the array passes the test.

Today you are in the mood to eat some potato dishes. So want to check if a restaurant has some potato based dishes. So you check the ingredients of each of the items on the menu to find dishes that have potato in them.

So the dishes are our elements inside an array. Checking if a dish has potato is the function. `.some()` will take this function and test each of the dishes and in the end if atleast one dish passes the test it will return true.

```javascript
```

https://medium.com/@d7k/js-includes-vs-some-b3cd546a7bc3

## every
The [`.every()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every "MDN .every documentation") method takes a test function and returns true only if all the element in the array pass the test.

So a friend has invited you for a dinner but you have condition you will only go if all the dishes are meat bases. So you confirm the menu with your friend and only when you confirm all the dishes are meat based you go for dinner.

So the dishes are our elements inside an array. Checking if a dishes are meat based is the function. `.every()` will take this function and test each of the dishes and only if all the dishes pass the test it will return true.

```javascript
```


https://www.javatpoint.com/es6-array-methods
