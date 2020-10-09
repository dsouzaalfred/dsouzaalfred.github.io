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
const dishesToMap = ['steak', 'fried rice', 'clear soup'];
const addEggs = (dish) => 'fried egg + ' + dish;

const updatedDishesToMap = dishes.map(addEggs);
console.log(updatedDishesToMap);
```

Remember
- `.map()` will not run the test function on empty elements.
- `.map()` returns a new array, the original array is not changed.

## filter

The [`.filter()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter "MDN .filter documentation") method takes a test function and will call the function once on each array and returns a new array of elements that passed the test.

This time you are served a few dishes but you are in no mood to each vegetables. So you check each dish and see if they have vegetables, if they do you don't eat them.

So the dishes are our elements inside an array. Checking each dish if it has vegetables is a function. And `.filter()` will repeat the process on each dish and return all the dishes without vegetables.

```javascript
const dishesToFilter = [
  { name: 'steak', hasVeggies: false },
  { name: 'fried rice', hasVeggies: false },
  { name: 'stir fried vegetables', hasVeggies: true },
];
const removeDishesWithVeggies = (dish) => !dish.hasVeggies;

const updatedDishesToFilter = dishesToFilter.filter(removeDishesWithVeggies);
console.log(updatedDishesToFilter);
```

Remember
- `.filter()` will return an empty array if non of the elements pass the test.
- `.filter()` returns a new array, the original array is not changed.

## reduce
The [`.reduce()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce "MDN .reduce documentation") method takes a function (called reducer) and uses it on every element of the array and outputs a single value.

After eating a huge spread at the restaurant you want to calculate the total you will have to pay. So you take the price of each dish and keep adding till you are done with all the dishes and the final number is the total you will have to pay.

So the dishes are our elements inside an array. Adding up cost of each dish is the reducer. You pass this reducer to `.reduce()` and it gives you the total.

```javascript
const dishesToTotal = [30, 20, 15, 40];
const reducer = (accumulator, currentValue) => accumulator + currentValue;

const total = dishesToTotal.reduce(reducer);
console.log(total);
```

## includes
The [`.includes()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes "MDN .include documentation") method can be used when you want to check if a value exists in an array.

Say you want to check if a restaurant servers your favourite dish.

So the dishes are our elements inside an array. You tell `.includes()` which dish you are looking for and it will tell you yes(`true`) or no(`false`).

```javascript
const restaurantMenu = ['steak', 'biryani', 'kebbabs'];
console.log(restaurantMenu.includes('biryani'));
```

## find
The [`.find()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find "MDN .find documentation") method takes a test function and returns the value of the first element that passes the test.

Where `.includes()` tells you if a restaurant servers your favourite dish, `.find()` will get you the dish if the restaurant servers it.

So the dishes are our elements inside an array. Checking if the restaurant serves your favourite dish is a function. And `.find()` check each dish and first instance it comes across your favourite dish it will get it for you.

```javascript
const restaurant2Menu = ['steak', 'biryani', 'kebbabs'];
const findBiryani = (dish) => dish === 'biryani';
console.log(restaurant2Menu.find(findBiryani));
```

## findIndex
The [`.fndIndex()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex "MDN .findIndex documentation") method takes a test function and returns the index of the first element that passes the test.

This time you are at a buffet and want to with chocolate cake. So you ask one of the waiters to point you in the direction of chocolate cake.

So the dishes are our elements inside an array. `.findIndex()` is the waiter who takes in what you want and points you to the location where it is.

```javascript
const restaurant3Menu = [
  'steak',
  'biryani',
  'kebbabs',
  'vanilla cake',
  'chocolate cake',
];
const findChocolateCake = (dish) => dish === 'chocolate cake';
console.log(restaurant3Menu.findIndex(findChocolateCake));
```

## some
The [`.some()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some "MDN .some documentation") method takes a test function and returns true if at-least one element in the array passes the test.

Today you are in the mood to eat some potato dishes. So want to check if a restaurant has some potato based dishes. So you check the ingredients of each of the items on the menu to find dishes that have potato in them.

So the dishes are our elements inside an array. Checking if a dish has potato is the function. `.some()` will take this function and test each of the dishes and in the end if at least one dish passes the test it will return true.

```javascript
const restaurant4Menu = [
  { name: 'fried rice', hasPotatoes: false },
  { name: 'french fries', hasPotatoes: true },
  { name: 'stir fried vegetables', hasPotatoes: true },
];
const hasDishesWithPotatoes = (dish) => dish.hasPotatoes;
console.log(restaurant4Menu.some(hasDishesWithPotatoes));
```

https://medium.com/@d7k/js-includes-vs-some-b3cd546a7bc3

## every
The [`.every()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every "MDN .every documentation") method takes a test function and returns true only if all the element in the array pass the test.

So a friend has invited you for a dinner but you have condition you will only go if all the dishes are meat bases. So you confirm the menu with your friend and only when you confirm all the dishes are meat based you go for dinner.

So the dishes are our elements inside an array. Checking if a dishes are meat based is the function. `.every()` will take this function and test each of the dishes and only if all the dishes pass the test it will return true.

```javascript

```


https://www.javatpoint.com/es6-array-methods
