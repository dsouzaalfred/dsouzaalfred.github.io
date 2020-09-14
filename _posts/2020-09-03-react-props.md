---
layout: post
title: React - Props
date: 2020-09-03 09:47 +0100
author: alfred_dsouza
categories:
  - blog
  - react
share: true
---

## What are props?
Props or properties is data passed to a component. A parent component will pass data to a child component as a prop.
Couple of thinks to note about Props:
- `props` is keyword is react and cannot be used as a variable name.
- `props` are immutable i.e. they are read-only

When we define a component, props are like function arguments in JavaScript.

Let's start with a simple component.
```javascript
import React from 'react';

const PropsExample = (props) => {
  return <h1>{props.title}</h1>
}

export default PropsExample;
```

Our `PropsExample` component is expecting a parent component to pass data for the title props and it will display the value for title as a h1.

The next step would be to use the `PropsExample` component in our `App` component and pass it some data.

```javascript
import React from 'react';
import PropsExample from './PropsExample';

const App = () => {
  return (
    <div>
      <PropsExample title="App title" />
    </div>
  );
}

export default App;
```

In our App comment we are importing the PropsExample component and use it as an HTML tag then pass the title like an attribute.

## Types of props
In the above example the prop title is of type string but we can use other types too, like:
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
      <p><strong>Name</strong>: {props.name}</p>
      <p><strong>User Id</strong>: {props.userId}</p>
      <p><strong>Roles</strong>: </p>
      <ul>
        {props.roles.map((role, index) => (<li key={index}>{role}</li>))}
      </ul>
      <p><strong>Last login</strong>: </p>
      <ul>
        <li>Date :{props.lastLogin.date}</li>
        <li>Location :{props.lastLogin.location}</li>
        <li>Device: {props.lastLogin.device}</li>
      </ul>
      <p><strong>Status</strong>: {props.isActive ? 'Active' : 'Not active'}
    </>
  )
}

export default PropsExample;
```

And, now let's update our `App` component to pass all the required values to the `PropsExample` component.
```javascript
import React from 'react';
import PropsExample from './PropsExample';

const App = () => {
  return (
    <div>
      <PropsExample Name="dsouzaalfred" userId={3} roles=["editor", "admin"] lastLogin={{date: "20/07/2020", location: "London"}} status  />
    </div>
  );
}

export default App;
```

## Function as props
This takes care of the data, but what is we want to add some functionality to our component, like handling a button click or some other event. In such cases we can pass a function/method as a prop. Let's update `PropsExample` component to we expect a function in it's props to handle a button click.

```javascript
import React from 'react';

const PropsExample = (props) => {
  return (
    <>
      <h1>User details</h1>
      <p><strong>Name</strong>: {props.name}</p>
      <p><strong>User Id</strong>: {props.userId}</p>
      <p><strong>Roles</strong>: </p>
      <ul>
        {props.roles.map((role, index) => (<li key={index}>{role}</li>))}
      </ul>
      <p><strong>Last login</strong>: </p>
      <ul>
        <li>Date :{props.lastLogin.date}</li>
        <li>Location :{props.lastLogin.location}</li>
        <li>Device: {props.lastLogin.device}</li>
      </ul>
      <p><strong>Status</strong>: {props.isActive ? 'Active' : 'Not active'}
      <div><button onClick={props.handleDisableClick}>Disable User</button></div>
    </>
  )
}

export default PropsExample;
```

Here we have a button to disable the user and the `handleDisableClick` which comes from the props will be called on button click.

Next step would be to pass the `handleDisableClick` function as prop to the `PropsExample` component.

```javascript
import React from 'react';
import PropsExample from './PropsExample';

const App = () => {
  const handleDisableClick = () => {
    console.log('Some action to disable user.');
  };
  return (
    <div>
      <PropsExample Name="dsouzaalfred" userId={3} roles=["editor", "admin"] lastLogin={{date: "20/07/2020", location: "London"}} status handleDisableClick={handleDisableClick}  />
    </div>
  );
}

export default App;
```

## Components as props
Components can be passed as props to other components. For example we can have a `Card` component which will take in three more components and render them.

```javascript
import React from 'react';

const Card = (props) => {
  return (
    <div>
      <div>
        {props.cardHeader}
      </div>
      <div>
        {props.cardBody}
      </div>
      <div>
        {props.cardFooter}
      </div>
    </div>
  );
}

export default Card;
```

Next we will build the three components required by the `Card` component.

```javascript
import React from 'react';

const Header = (props) => {
  return (
    <h1>{props.title}</h1>
  );
}

export default Header;
```

```javascript
import React from 'react';

const Content = (props) => {
  return (
    <p>{props.text}</p>
  );
}

export default Content;
```

```javascript
import React from 'react';

const Footer = (props) => {
  return (
    <button onClick={props.handleClick}>{props.buttonText}<button>
  );
}

export default Footer;
```

With the three components built, it's time to see how we pass them to the `Card` component.
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
      <Card cardHeader={<Header title={props.name} /> } cardBody={<Content text={props.userId} />} cardFooter={<Footer handleClick={props.handleDisableClick} buttonText="Disable User" />}  />
      // <p><strong>Name</strong>: {props.name}</p>
      // <p><strong>User Id</strong>: {props.userId}</p>
      <p><strong>Roles</strong>: </p>
      <ul>
        {props.roles.map((role, index) => (<li key={index}>{role}</li>))}
      </ul>
      <p><strong>Last login</strong>: </p>
      <ul>
        <li>Date :{props.lastLogin.date}</li>
        <li>Location :{props.lastLogin.location}</li>
        <li>Device: {props.lastLogin.device}</li>
      </ul>
      <p><strong>Status</strong>: {props.isActive ? 'Active' : 'Not active'}
      // <div><button onClick={props.handleDisableClick}>Disable User</button></div>
    </>
  )
}

export default PropsExample;
```

## Destructuring
Instead of writing `props` over and over again we can use [Destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment). Destructuring helps us unpack values inside the props object.

```javascript
import React from 'react';

import Card from './Card';
import Header from './Header';
import Content from './Content';
import Footer from './Footer';

const PropsExample = ({name, userId, handleDisableClick, roles, lastLogin, isActive}) => {
  return (
    <>
      <h1>User details</h1>
      <Card cardHeader={<Header title={name} /> } cardBody={<Content text={userId} />} cardFooter={<Footer handleClick={handleDisableClick} buttonText="Disable User" />}  />
      // <p><strong>Name</strong>: {props.name}</p>
      // <p><strong>User Id</strong>: {props.userId}</p>
      <p><strong>Roles</strong>: </p>
      <ul>
        {roles.map((role, index) => (<li key={index}>{role}</li>))}
      </ul>
      <p><strong>Last login</strong>: </p>
      <ul>
        <li>Date :{lastLogin.date}</li>
        <li>Location :{lastLogin.location}</li>
        <li>Device: {lastLogin.device}</li>
      </ul>
      <p><strong>Status</strong>: {isActive ? 'Active' : 'Not active'}
      // <div><button onClick={props.handleDisableClick}>Disable User</button></div>
    </>
  )
}

export default PropsExample;
```

As you can see, instead of using `props` all over the component we can Descruture props and use the prop names directly. What we are essitially doing is this:

```javascript
const {name, userId, handleDisableClick, roles, lastLogin, isActive} = props;
```

## Type checking
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

const PropsExample = ({name, userId, handleDisableClick, roles, lastLogin, isActive}) => {
  return (
    <>
      <h1>User details</h1>
      <Card cardHeader={<Header title={name} /> } cardBody={<Content text={userId} />} cardFooter={<Footer handleClick={handleDisableClick} buttonText="Disable User" />}  />
      <p><strong>Roles</strong>: </p>
      <ul>
        {roles.map((role, index) => (<li key={index}>{role}</li>))}
      </ul>
      <p><strong>Last login</strong>: </p>
      <ul>
        <li>Date :{lastLogin.date}</li>
        <li>Location :{lastLogin.location}</li>
        <li>Device: {lastLogin.device}</li>
      </ul>
      <p><strong>Status</strong>: {isActive ? 'Active' : 'Not active'}
    </>
  )
}

// add type checks here
PropsExample.propTypes = {
  name: PropTypes.string,
  userId: PropTypes.number,
  handleDisableClick: PropTypes.func,
  roles: PropTypes.array,
  lastLogin: PropTypes.object,
  isActive: PropTypes.bool
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

Additionally we can mark some props as required, using `isRequired`.

```javascript
import React from 'react';
import PropTypes from 'prop-types';

const Footer = (props) => {
  return (
    <button onClick={props.handleClick}>{props.buttonText}<button>
  );
}

// add type checks here
Footer.propTypes = {
  handleClick: PropTypes.func.isRequired,
  buttonText: PropTypes.string.isRequired,
};

export default Footer;
```

Using `prop-types` does not only help us with type checking but it's also a type of documentation for our components.

That's all we got time for this time. And as always you can find the code on [GitHub](https://github.com/dsouzaalfred/blogdemos/tree/master/getting-started-with-react)
