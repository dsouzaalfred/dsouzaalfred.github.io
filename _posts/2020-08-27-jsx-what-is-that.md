---
layout: post
title: JSX - What is that?
date: 2020-09-02 11:50 +0100
author: alfred_dsouza
categories:
  - blog
  - react
share: true
---

In the [last post](/blog/react/getting-started-with-react/) I briefly mentioned JSX, in this post we will have a detailed view of JSX.
So what is JXS? JXS is like a template language or a form of markup like HTML that gets complied to JavaScript code by react. React components are all JavaScript, hence we need something that will help us with the markup for our UI that is where JSX comes in. JSX looks like HTML but is incredibly powerful since it is complied down to JavaScript.

You can write [React without using JSX](https://reactjs.org/docs/react-without-jsx.html) but that become very complicated very fast and is not very intuitive.

## Getting started
A very simple example will be `FirstComponent` that we created in the [last post](/blog/react/getting-started-with-react/#our-first-component).

```javascript
import React from 'react';

const FirstComponent = () => {
  return <h1>This is my first component</h1>;
};

export default FirstComponent;
```
This component will always render the same text: _This is my first component_.

## Math
JSX is JavaScript expressions, which means we can do a lot more then just displaying static text. We can do math:
```javascript
import React from 'react';

const MathAdd = () => {
  return <h1>{3 + 4}</h1>;
};

export default MathAdd;
```

Or use JavaScript built-in functions like [Math.random()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/random) to display random number.
```javascript
import React from 'react';

const MathRandom = () => {
  return <h1>{Math.random()}</h1>;
};

export default MathRandom;
```

## Strings
We can use JavaScript [string literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) to display content in our component.
```javascript
import React from 'react';

const StringLiterals = () => {
  return <h1>{`Text using string literals`}</h1>;
};

export default StringLiterals;
```
While this might look useless it can be very powerful when you want to concatenate two strings or display a value stored in a variable.
```javascript
import React from 'react';

const StringLiteralsTwo = () => {
  const randomNumber = Math.random();
  return <h1>{`The random number is ${randomNumber}`}</h1>;
};

export default StringLiteralsTwo;
```
Or use a JavaScript string methods, for example [`toUpperCase()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/toUpperCase).
```javascript
import React from 'react';

const StringLiteralsThree = () => {
  const name = 'alfred';
  return <h1>{`Hello ${name.toUpperCase()}`}</h1>;
};

export default StringLiteralsThree;
```

## Conditions
Want to display text based on some condition we can do that too.
```javascript
import React from 'react';

const Conditions = () => {
  const getNow = new Date();
  const getHour = getNow.getHours();
  return <h1>{getHour < 7 ? 'Sleeping' : 'Awake'}</h1>;
};

export default Conditions;
```
In the above example we are checking what [hour](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getHours) it is and displaying a message accordingly using a [ternary operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator).

## Attributes
We can also specify tag attributes.
```javascript
import React from 'react';

const Attributes = () => {
  return (
    <h1 tabindex="0" id="h1-tag">
      Arributes component
    </h1>
  );
};

export default Attributes;
```

The values for the attributes can also be set using expressions.
```javascript
import React from 'react';

const AttributesTwo = () => {
  const tabIndex = 0;
  return (
    <h1 tabindex={tabIndex} id="h1-tag">
      AttributesTwo component
    </h1>
  );
};

export default AttributesTwo;
```
This is specially useful when we have the values coming from component props(we will cover it in future posts).

## Parent node
Till now we have been using just one tag in our component, what if we want to build a complex component with multiple tags. We can have as many tags/nodes as we want but the component should return only one tag/nodes hence most of the component have one parent tag/nodes that acts as a wrapper to other tags.
```javascript
import React from 'react';

const ParentNode = () => {
  return (
    <div>
      <label>First Name :</label>
      <input type="text" />
    </div>
  );
};

export default ParentNode;
```

But sometimes we don't want an addition `div` or any other tag as a wrapper, in such cases we can use [react fragments](https://reactjs.org/docs/fragments.html). Fragments are special react syntax(`<></>`) which will wrap you content and when the component is rendered only the content is shown and not the fragments.
```javascript
import React from 'react';

const ParentNodeTwo = () => {
  return (
    <>
      <label>Last Name :</label>
      <input type="text" />
    </>
  );
};

export default ParentNodeTwo;
```

This also helps us when we have to handle complex conditions
```javascript
import React from 'react';

const ParentNodeThree = () => {
  const getNow = new Date();
  const getHour = getNow.getHours();
  return (
    <>
      {getHour >= 0 && getHour <= 7 && <h1>Sleeping</h1>}
      {getHour > 7 && getHour <= 9 && <h1>Morning routine</h1>}
      {getHour > 9 && getHour <= 13 && <h1>Work</h1>}
      {getHour > 13 && getHour <= 14 && <h1>Lunch</h1>}
      {getHour > 14 && getHour <= 18 && <h1>Work</h1>}
      {getHour > 18 && getHour <= 22 && <h1>Family Time</h1>}
      {getHour > 22 && <h1>Sleeping</h1>}
    </>
  );
};

export default ParentNodeThree;
```

## Loops
The last thing we will cover is Loops. A lot of times we have display a list of something on the frontend and most of the times the data for the list will come from a service like an API or a JSON file, etc. Again, since we are using JavaScript we can take advantage of JavaScript array methods like [`map()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) or [`filter()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter).

### map()
We can use `map()` when you want to display every element in an array.
```javascript
import React from 'react';

const LoopsMap = () => {
  const data = [
    { id: 1, label: 'One' },
    { id: 2, label: 'Two' },
    { id: 3, label: 'Three' },
    { id: 4, label: 'Four' },
    { id: 5, label: 'Five' },
  ];
  return (
    <ul>
      {data.map((item) => (
        <li key={item.id}>{item.label}</li>
      ))}
    </ul>
  );
};

export default LoopsMap;
```
Our component will display an un-order list. There is a lot going on in our component to achieve this :
- We have a variable data that is an array of object, each object has a `id` and a `label`.
- We loop over data using the `map()` method.
- Each object is referred to as `item`, you can call it anything you want, it's just a variable.
- For each item we are returning an `li`. Note that there is no return statement since we are using [arrow function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions).
- Each tag/node that we return should have a unique `key`, we are using the `id` as key. We can use `index` as the key, while it works most of the time but you can run into bugs specially if you allow addition and deletion to you list.

In the same way we can use the `filter()` method too.
```javascript
import React from 'react';

const LoopsFilter = () => {
  const data = [
    { id: 1, label: 'One' },
    { id: 2, label: 'Two' },
    { id: 3, label: 'Three' },
    { id: 4, label: 'Four' },
    { id: 5, label: 'Five' },
  ];
  return (
    <ul>
      {data
        .filter((item) => item.id % 2 === 0)
        .map((filteredData) => (
          <li key={filteredData.id}>{filteredData.label}</li>
        ))}
    </ul>
  );
};

export default LoopsFilter;
```
In the above example we only want to print labels of values whose id's are divisible 2. So first we filter such values, since filter returns an array we map over the array and then print the values.

Well that's' a lot for one post but I hope it helps you understand how to use JSX. In the next post we will cover props.

You can find the code on [GitHub](https://github.com/dsouzaalfred/blogdemos/tree/master/jsx-what-is-that)
