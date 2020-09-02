---
layout: post
title: Getting started with React
date: 2020-08-26 11:15 +0100
author: alfred_dsouza
categories:
  - blog
  - react
share: true
comments: true
image:
  path: /images/getting-started-with-react-hero-image.jpg
  caption: "Getting started with React"
---

## What is react?
React or ReactJS is a component-based JavaScript library for building user interfaces. It is one of the most popular JavaScript UI libraries.
*Component-based* means a complex UI is broken down into small pieces called components. These small components can manage their own state and encapsulate their own logic.

## CRA - Create React App
[Create React App](https://github.com/facebook/create-react-app) makes getting started with React very easy.
You will need to have [**Node >= 8.10 and npm >= 5.6**](https://nodejs.org/en/) installed on your machine. If you don't already have it installed on your machine you can head over to [nodejs.org](https://nodejs.org/en/) and download & install it before moving forward.

Once you are done installing `Node`, you can either use the `npm` (comes bundled with node) or `yarn` package manager. I prefer [`yarn`](https://www.npmjs.com/package/yarn), let's go ahead and install it. Run the following command on your terminal/command line:

`npm install --global yarn`

Assuming that you have [`Node >= 8.10 and npm >= 5.6`](https://nodejs.org/en/) and [`yarn`](https://www.npmjs.com/package/yarn) installed on your machine, open terminal/command line and run the following command.

`npx create-react-app my-first-react-app`

This will install
- create a folder called _my-first-react-app_
- install all the dependencies required

Once the installation is complete run the following commands

`cd my-first-react-app`

To move into the newly created folder

`yarn start`

This will start a local dev server on your local host at port 3000 `http://localhost:3000/`


## Our first component  {#our-first-component}
Open the *my-first-react-app* folder in your an editor of your choice. Under the **src** folder create a new file `FirstComponent.js`.

Add the following code to this file and save it:

```javascript
import React from 'react';

const FirstComponent = () => {
  return <h1>This is my first component</h1>;
};

export default FirstComponent;
```
As you can see, the component code is all JavaScript. We are importing react as it is required to render the component. We are using [arrow function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) in our code but you can use normal function syntax too.

That HTML content we are returning from is [JSX](https://reactjs.org/docs/introducing-jsx.html), it looks very much like HTML but it is not.

Now open `App.js` and remove all the code in the file and replace it with the following code.

```javascript
import React from 'react';
import FirstComponent from './FirstComponent';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <FirstComponent />
      </header>
    </div>
  );
}

export default App;
```

`import FirstComponent from './FirstComponent';` is used to import the component into the `App.js` file.
`<FirstComponent />` is how we use the component, basically telling react to render our component.

Now if you visit `http://localhost:3000/` you should see **This is my first component** on the screen.

Couple of things to note before we move forward:
- `App` is also a component.
- Both `App` and `FirstComponent` are function components.

We can use the same component multiple times, add another `<FirstComponent />` below the first one so our `App.js` file will look like this:

```javascript
import React from 'react';
import FirstComponent from './FirstComponent';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <FirstComponent />
        <FirstComponent />
      </header>
    </div>
  );
}

export default App;
```

Our component is static as in it will show the same text everywhere, we can make dynamic by using **props**.

## props
We can pass data to a component using props. In our case we want we would like our component to display some text that we want. Let's update the `FirstComponent.js` file:

```javascript
import React from 'react';

const FirstComponent = ({ text }) => {
  return <h1>{text}</h1>;
};

export default FirstComponent;
```

Now our component will take a props called **text** and display the value that is passed to it within the `h1` tags.
So let's update `App.js` to reflect the changes we have made to `FirstComponent`.

```javascript
import React from 'react';
import FirstComponent from './FirstComponent';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <FirstComponent text="First Header" />
        <FirstComponent text="Second Header" />
      </header>
    </div>
  );
}

export default App;
```
Now if you visit `http://localhost:3000/` you will see you different headings.

In our next post we will have detailed look at [JSX](/blog/react/jsx-what-is-that/).

You can find the code on [GitHub](https://github.com/dsouzaalfred/blogdemos/tree/master/getting-started-with-react)
