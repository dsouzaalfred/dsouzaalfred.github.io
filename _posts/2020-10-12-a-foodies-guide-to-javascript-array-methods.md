---
layout: post
title: A foodies guide to JavaScript array methods
date: 2020-10-12 12:01 +0100
author: alfred_dsouza
categories:
  - blog
  - javascript
share: true
image:
  path: /images/a-foodies-guide-to-javascript-array-methods.jpg
  caption: "A foodies guide to JavaScript array methods"
---
JavaScript has a lot of built in array methods. Let's have a look at some that will help us in our journey with React. We will be looking at :
- [.map()](#array-map)
- [.filter()](#array-filter)
- [.reduce()](#array-reduce)
- [.includes()](#array-includes)
- [.find()](#array-find)
- [.findIndex()](#array-findIndex)
- [.some()](#array-some)
- [.every()](#array-every)

I love to eat and try to remember each method by associating it with food. Let me show you how I remember these array methods.

Let's get started

## .map()  {#array-map}

The [`map()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map "MDN .map documentation") method takes a function and will call the function once for every element in the array and return a new array with the updated values.

Let's say you are served five dishes but you like eggs with everything, so you decide to fry eggs and put them on all the dishes. After all, eggs make everything good.

So the dishes are our elements inside an array. Frying the egg and putting it on a dish is the function. And `.map()` will repeat the process for us for each dish.

```javascript
// array-map.js

// dishes
const dishesToMap = ['steak', 'fried rice', 'clear soup'];

// function to add fried egg
const addEggs = (dish) => 'fried egg + ' + dish;

// updated dishes
const updatedDishesToMap = dishesToMap.map(addEggs);
console.log(updatedDishesToMap);

// output: ["fried egg + steak", "fried egg + fried rice", "fried egg + clear soup"]
```

Remember
- `.map()` will not run the test function on empty elements.
- `.map()` returns a new array, the original array is not changed.

## filter  {#array-filter}

The [`.filter()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter "MDN .filter documentation") method takes a test function and will call the function once on each element in the array and returns a new array of elements that pass the test.

This time you are served a few dishes but you are in no mood to eat vegetables. So you check each dish and see if they have vegetables, if they do you don't eat them.

Again the dishes are our elements inside an array. Checking each dish if it has vegetables is a function. And `.filter()` will repeat the process on each dish and return all the dishes without vegetables.

```javascript
//array-filter.js

// dishes
const dishesToFilter = [
  { name: 'steak', hasVeggies: false },
  { name: 'fried rice', hasVeggies: false },
  { name: 'stir fried vegetables', hasVeggies: true },
];

// function to filter dishes with vegetables
const removeDishesWithVeggies = (dish) => !dish.hasVeggies;

// filtering dishes
const updatedDishesToFilter = dishesToFilter.filter(removeDishesWithVeggies);
console.log(updatedDishesToFilter);

// output: [{ name: "steak", hasVeggies: false }, { name: "fried rice", hasVeggies: false }]
```

Remember
- `.filter()` will return an empty array if non of the elements pass the test.
- `.filter()` returns a new array, the original array is not changed.

## reduce  {#array-reduce}
The [`.reduce()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce "MDN .reduce documentation") method takes a function (called reducer) and uses it on every element of the array and outputs a single value.

Alright so after eating a huge spread at the restaurant you want to calculate the total you will have to pay. So you take the price of each dish and keep adding till you are done with all the dishes and the final number is the total you will have to pay.

Once again, the dishes are our elements inside an array. Adding up cost of each dish is the reducer. You pass this reducer to `.reduce()` and it gives you the total.

```javascript
// array-reduce.js

// cost of each dish
const dishesToTotal = [30, 20, 15, 40];

// reducer: accumulator => stores the total, currentValue => price of the current dish
const reducer = (accumulator, currentValue) => accumulator + currentValue;

// calculate the total
const total = dishesToTotal.reduce(reducer);
console.log(total);

// output: 105
```

## includes  {#array-includes}
The [`.includes()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes "MDN .includes documentation") method can be used when you want to check if a value exists in an array.

Say you want to check if a restaurant serves your favourite dish.

This time the dishes served by the restaurant are the items inside an array. You tell `.includes()` which dish you are looking for and it will tell you yes(`true`) if the restaurant serves the dish or no(`false`) if it does not.

```javascript
// array-includes.js

// dishes served by a restaurant
const restaurantMenu = ['steak', 'biryani', 'kebbabs'];

// checking if it serves your favourite dish
console.log(restaurantMenu.includes('biryani'));

// output: true
```

## find  {#array-find}
The [`.find()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find "MDN .find documentation") method takes a test function and returns the value of the first element that passes the test.

Where `.includes()` tells you if a restaurant serves your favourite dish, `.find()` will get you the dish if the restaurant serves it.

Again, the dishes served by the restaurant are the items inside an array. Checking if the restaurant serves your favourite dish is a function. And `.find()` check each dish and the first instance it comes across your favourite dish it will get it for you.

```javascript
// array-find.js

// dishes served by a restaurant
const restaurant2Menu = ['steak', 'biryani', 'kebbabs'];

// dish you want to find
const findBiryani = (dish) => dish === 'biryani';

// find the dish
console.log(restaurant2Menu.find(findBiryani));

// output: biryani
```

## findIndex  {#array-findIndex}
The [`.fndIndex()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex "MDN .findIndex documentation") method takes a test function and returns the index of the first element that passes the test.

This time you are at a buffet and want to eat chocolate cake. So you ask one of the waiters to point you in the direction of chocolate cake.

All the dishes on the buffet are our elements inside an array. `.findIndex()` is the waiter who takes in what you want and points you to the location where it is.

```javascript
// array-findIndex.js

// dishes on the buffet
const dishesOnTheBuffet = [
  'steak',
  'biryani',
  'kebbabs',
  'vanilla cake',
  'chocolate cake',
];

// dish you want to find
const findChocolateCake = (dish) => dish === 'chocolate cake';

// getting the location of the dish
console.log(dishesOnTheBuffet.findIndex(findChocolateCake));

// output: 4
```

## some  {#array-some}
The [`.some()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some "MDN .some documentation") method takes a test function and returns true if at-least one element in the array passes the test.

Today you are in the mood to eat some potato dishes. So you check if a restaurant has some potato based dishes. You check the ingredients of each of the items on the menu to find dishes that have potatoes in them.

The dishes are our elements inside an array. Checking if a dish has potato is the function. `.some()` will take this function and test each of the dishes and in the end if at least one dish passes the test(has potato) it will return `true`.

```javascript
// array-some.js

// dishes
const restaurant4Menu = [
  { name: 'fried rice', hasPotatoes: false },
  { name: 'french fries', hasPotatoes: true },
  { name: 'stir fried vegetables', hasPotatoes: true },
];

// function to check if a dish has potato
const hasDishesWithPotatoes = (dish) => dish.hasPotatoes;

// checking all the dishes in the restaurant
console.log(restaurant4Menu.some(hasDishesWithPotatoes));

// output: true
```

## every  {#array-every}
The [`.every()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every "MDN .every documentation") method takes a test function and returns true only if all the element in the array pass the test.

This time a friend has invited you for a dinner but you have a condition, you will only go if all the dishes are meat based. You confirm the menu with your friend and only when you are sure all the dishes are meat based you go for dinner.

The dishes are our elements inside an array. Checking if a dish is meat based is the function. `.every()` will take this function and test each of the dishes and only if all the dishes pass the test it will return `true`.

```javascript
// array-every.js

// dishes served at dinner
const dinnerDishes = [
  { name: 'biryani', hasMeat: true },
  { name: 'french fries', hasMeat: false },
  { name: 'jeera rice', hasMeat: false },
  { name: 'butter chicken', hasMeat: true },
];

// function to check if they have meat.
const dishesWithMeat = (dish) => dish.hasMeat;

// checking if all dishes have meat.
console.log(dinnerDishes.every(dishesWithMeat));

// output: false
```

That's all for today, until next time take care :).

Lastly you can find the code on [github](https://github.com/dsouzaalfred/blogdemos/tree/master/a-foodies-guide-to-javascript-array-methods "A foodies guide to JavaScript array methods repo").

<hr>
> <span>Cover photo by <a href="https://unsplash.com/photos/yvzzemH8-J0">Haryo Setyadi</a> on <a href="https://unsplash.com/">Unsplash</a></span>
