---
layout: post
title: React - Props
date: 2020-09-14 09:47 +0100
author: alfred_dsouza
categories:
  - blog
  - react
share: true
image:
  path: /images/react-props-hero-image.jpg
  caption: "React - Props"
---

## What are props?
Props or properties are data passed to a component. A parent component will pass data to a child component as a prop.
There are a couple of things to note about Props:
- `props` is a keyword in React and cannot be used as a variable name.
- `props` are immutable i.e. they are read-only

_When we define a component, props are like function arguments in JavaScript._

Let's start with a simple component.
```javascript
import React from 'react';

const PropsExample = (props) => {
  return <h1>{props.title}</h1>;
};

export default PropsExample;
```

Our `PropsExample` component is expecting a parent component to pass data for the title props and it will display the value for title as a h1.

The next step would be to use the `PropsExample` component in our `App` component and pass it some data.

```javascript
import React from 'react';

import PropsExample from './PropsExample';

import './App.css';

function App() {
  return (
    <div className="app">
      <PropsExample title="App title" />
    </div>
  );
}

export default App;

```

In our App comment we are importing the `PropsExample` component and _use it as an HTML tag then pass the title like an attribute_.

## Types of props
In the above example the prop title is of type string, but we can use other types too, like:
- Numbers
- Arrays
- Objects
- Boolean

Let's update our component to use different types of props:

```javascript
import React from 'react';

const PropsExample = (props) => {
  return (
    <>
      <h1>User details</h1>
      <p>
        <strong>Name</strong>: {props.name}
      </p>
      <p>
        <strong>User Id</strong>: {props.userId}
      </p>
      <p>
        <strong>Roles</strong>:
      </p>
      <ul>
        {props.roles.map((role, index) => (
          <li key={index}>{role}</li>
        ))}
      </ul>
      <p>
        <strong>Last login</strong>:
      </p>
      <ul>
        <li>Date :{props.lastLogin.date}</li>
        <li>Location :{props.lastLogin.location}</li>
      </ul>
      <p>
        <strong>Status</strong>: {props.isActive ? 'Active' : 'Not active'}
      </p>
    </>
  );
};

export default PropsExample;
```

We have updated `PropsExample` component and added a few more props.
- `name` as a string
- `userId` as a number
- `roles` as a array of strings
- `lastLogin` as a object
- `isActive` as a bollean

Thinks to note:
- `roles` is an array, we can `map` over it and display it's values, the previous post explains more about [`map()`](/blog/react/jsx-what-is-that/#jsx-array-map).
- `lastLogin` is an object and we can access the keys of this object like in normal JS.

And, now let's update our `App` component to pass all the required values to the `PropsExample` component.

```javascript
import React from 'react';

import PropsExample from './PropsExample';

import './App.css';

function App() {
  return (
    <div className="app">
      <PropsExample
        name="Alfred DSouza"
        userId={3}
        roles={['editor', 'admin']}
        lastLogin={ { date: '20/07/2020', location: 'London' } }
        isActive
      />
    </div>
  );
}

export default App;
```

## Function as props
Sometimes we would like our component to handle some functionality like handling a click event or any other event. In such cases we can pass a function/method as a prop. Let's update `PropsExample` component to expect a function as one of the props to handle a button click.

```javascript
import React from 'react';

const PropsExample = (props) => {
  return (
    <>
      <h1>User details</h1>
      <p>
        <strong>Name</strong>: {props.name}
      </p>
      <p>
        <strong>User Id</strong>: {props.userId}
      </p>
      <p>
        <strong>Roles</strong>:{' '}
      </p>
      <ul>
        {props.roles.map((role, index) => (
          <li key={index}>{role}</li>
        ))}
      </ul>
      <p>
        <strong>Last login</strong>:{' '}
      </p>
      <ul>
        <li>Date :{props.lastLogin.date}</li>
        <li>Location :{props.lastLogin.location}</li>
      </ul>
      <p>
        <strong>Status</strong>: {props.isActive ? 'Active' : 'Not active'}
      </p>
      <div>
        <button onClick={props.handleDisableClick}>Disable User</button>
      </div>
    </>
  );
};

export default PropsExample;
```

Here we have a button to disable the user and the `handleDisableClick` which comes from the props will be called on button click.

Next step would be to pass the `handleDisableClick` function as prop to the `PropsExample` component.

```javascript
import React from 'react';

import PropsExample from './PropsExample';

import './App.css';

function App() {
  const handleDisableClick = () => {
    console.log('Some action to disable user.');
  };
  return (
    <div className="app">
      <PropsExample
        name="Alfred DSouza"
        userId={3}
        roles={['editor', 'admin']}
        lastLogin={ { date: '20/07/2020', location: 'London' } }
        isActive
        handleDisableClick={handleDisableClick}
      />
    </div>
  );
}

export default App;
```

We have defined the `handleDisableClick` function, it's a simple function that logs to the console. We pass this function as a prop to `PropsExample`.

## Component as props
Components can also be passed as props to other components. For example, we can have a `Card` component which will take in three more components and render them.

```javascript
import React from 'react';

const Card = (props) => {
  return (
    <div>
      <div>{props.cardHeader}</div>
      <div>{props.cardBody}</div>
      <div>{props.cardFooter}</div>
    </div>
  );
};

export default Card;
```

The `Card` component expects three components
- `cardHeader`
- `cardBody`
- `cardFooter`

Next, let's build three components, we will pass these components to the `Card` component.

The first one is the `Header` component, we will pass this to the `cardHeader` prop. This is a simple component that will take a prop `title` and display it inside a `h3`.
```javascript
import React from 'react';

const Header = (props) => {
  return <h3>{props.title}</h3>;
};

export default Header;
```

Next, is the `Content` component, we will pass this to the `cardBody` prop. This component expects another component as `children`.
```javascript
import React from 'react';

const Content = (props) => {
  return <div>{props.children}</div>;
};

export default Content;
```

And lastly, the `Footer` component, we will pass this to the `cardFooter` prop. This component takes two props `handleClick` a function to handle click and `buttonText`.
```javascript
import React from 'react';

const Footer = (props) => {
  return <button onClick={props.handleClick}>{props.buttonText}</button>;
};

export default Footer;
```

With the three components built, it's time to pass them to the `Card` component.
Let's use the `Card` component in our `PropsExample` component:

```javascript
import React from 'react';

import Card from './Card';
import Header from './Header';
import Content from './Content';
import Footer from './Footer';

const PropsExample = (props) => {
  return (
    <>
      <h1>User details</h1>
      <Card
        cardHeader={<Header title={props.name} />}
        cardBody={
          <Content>
            <>
              <p>
                <strong>User Id</strong>: {userId}
              </p>
              <p>
                <strong>Roles</strong>:
              </p>
              <ul>
                {roles.map((role, index) => (
                  <li key={index}>{role}</li>
                ))}
              </ul>
              <p>
                <strong>Last login</strong>:
              </p>
              <ul>
                <li>Date :{lastLogin.date}</li>
                <li>Location :{lastLogin.location}</li>
              </ul>
              <p>
                <strong>Status</strong>: {isActive ? 'Active' : 'Not active'}
              </p>
            </>
          </Content>
        }
        cardFooter={
          <Footer
            handleClick={props.handleDisableClick}
            buttonText="Disable User"
          />
        }
      />
    </>
  );
};

export default PropsExample;
```

The `Header` & the `Footer` components can be assigned props like any other component. The `Content` component is like a wrapper around its content. And the content should have only one parent component, that is the reason we have wrapped the content in a [react fragment](https://reactjs.org/docs/fragments.html).

## Destructuring props
Instead of writing `props` repeatedly, we can use [Destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment). Destructuring helps us unpack values that are inside the props object.

```javascript
import React from 'react';

import Card from './Card';
import Header from './Header';
import Content from './Content';
import Footer from './Footer';

const PropsExample = ({
  name,
  userId,
  handleDisableClick,
  roles,
  lastLogin,
  isActive,
}) => {
  return (
    <>
      <h1>User details</h1>
      <Card
        cardHeader={<Header title={name} />}
        cardBody={
          <Content>
            <>
              <p>
                <strong>User Id</strong>: {userId}
              </p>
              <p>
                <strong>Roles</strong>:
              </p>
              <ul>
                {roles.map((role, index) => (
                  <li key={index}>{role}</li>
                ))}
              </ul>
              <p>
                <strong>Last login</strong>:
              </p>
              <ul>
                <li>Date :{lastLogin.date}</li>
                <li>Location :{lastLogin.location}</li>
              </ul>
              <p>
                <strong>Status</strong>: {isActive ? 'Active' : 'Not active'}
              </p>
            </>
          </Content>
        }
        cardFooter={
          <Footer handleClick={handleDisableClick} buttonText="Disable User" />
        }
      />
    </>
  );
};

export default PropsExample;
```

As you can see, instead of using `props` all over the component we can destructure props and use the prop names directly. What we are essentially doing is this:

```javascript
const { name, userId, handleDisableClick, roles, lastLogin, isActive } = props;
```

## Type checking props
It is always a good idea to validate that the props a component gets are of the correct type. [`prop-types`](https://www.npmjs.com/package/prop-types) makes this very easy for us.
First make sure you install the `prop-types` package in your project. Use the following command to install `npm i prop-types`, you might need to restart the dev server.

Let's add some type checking to the `PropsExample` component.

```javascript
import React from 'react';
import PropTypes from 'prop-types';

import Card from './Card';
import Header from './Header';
import Content from './Content';
import Footer from './Footer';

const PropsExample = ({
  name,
  userId,
  handleDisableClick,
  roles,
  lastLogin,
  isActive,
}) => {
  return (
    <>
      <h1>User details</h1>
      <Card
        cardHeader={<Header title={name} />}
        cardBody={
          <Content>
            <>
              <p>
                <strong>User Id</strong>: {userId}
              </p>
              <p>
                <strong>Roles</strong>:
              </p>
              <ul>
                {roles.map((role, index) => (
                  <li key={index}>{role}</li>
                ))}
              </ul>
              <p>
                <strong>Last login</strong>:
              </p>
              <ul>
                <li>Date :{lastLogin.date}</li>
                <li>Location :{lastLogin.location}</li>
              </ul>
              <p>
                <strong>Status</strong>: {isActive ? 'Active' : 'Not active'}
              </p>
            </>
          </Content>
        }
        cardFooter={
          <Footer handleClick={handleDisableClick} buttonText="Disable User" />
        }
      />
    </>
  );
};

// add type checks here
PropsExample.propTypes = {
  name: PropTypes.string,
  userId: PropTypes.number,
  handleDisableClick: PropTypes.func,
  roles: PropTypes.array,
  lastLogin: PropTypes.object,
  isActive: PropTypes.bool,
};

export default PropsExample;
```

We can do the same for our `Card` component.

```javascript
import React from 'react';
import PropTypes from 'prop-types';

const Card = (props) => {
  return (
    <div>
      <div>
        {props.cardHeader}
      </div>
      <div>
        {props.cardHeader}
      </div>
      <div>
        {props.cardFooter}
      </div>
    </div>
  );
}

// add type checks here
Card.propTypes = {
  cardHeader: PropTypes.element,
  cardHeader: PropTypes.element,
  cardFooter: PropTypes.element,
};

export default Card;
```

Couple of things to note
- if an invalid value is provided for a prop, a warning will be shown in the JavaScript console of the browser developer tools.
- the `propTypes` are only checked in development mode

Now that we can type checking on props, we can mark some props as required, using `isRequired`.

```javascript
import React from 'react';
import PropTypes from 'prop-types';

const Footer = (props) => {
  return <button onClick={props.handleClick}>{props.buttonText}</button>;
};

// add type checks here
Footer.propTypes = {
  handleClick: PropTypes.func.isRequired,
  buttonText: PropTypes.string.isRequired,
};

export default Footer;
```

In the above `Footer` component we have defined the types of both the props and marked them as required. Again is the values are not provided we will see a warning in the JavaScript console of the browser developer tools.

Using `prop-types` does not only help us with type checking but it's also a type of documentation for our components.

That's all we got time for this time. And as always you can find the code on [GitHub](https://github.com/dsouzaalfred/blogdemos/tree/master/react-props)
