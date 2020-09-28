---
layout: post
title: React - Styling
date: 2020-09-17 12:01 +0100
author: alfred_dsouza
categories:
  - blog
  - react
share: true
---
In the last two post we covered JSX and Props, now it’s time to move forward in our journey in learning React and the next stop is styling the components.

There are various ways a component can be styled:
- Inline styles
- CSS file
- SASS file
- CSS modules
- CSS-in-JS libraries

## Inline styles

In HTML when we use inline styles you would do something like this:

```html
<p style="color: green" >This text will be green</p>
```

The same can be achieved with JSX. In JSX instead of passing the style as a string we pass it as a object.

```javascript
<p style={ {color: 'green'} }>This text will be green</p>
```

When we want to pass a value to a prop we use {} braces, this is exactly what we are doing, we are passing value to the style prop. To demostrate this we can write the above example as:

```javascript
const pTagStyle = {color: 'green'};

<p style={pTagStyle}>This text will be green</p>
```

Let's see some more css properties:

```javascript
<p
  style={ {
    padding: 20,
    margin: '20px 15px',
    fontSize: '2rem',
    color: 'darkorange',
    border: '1px solid darkgrey',
  } }
>
  Multiple CSS Properties
</p>
```

Lot of things going on there:
- Like we seen before you have to pass values as strings
- If you want to pass a `px` value to a CSS property just pass the number value. Like we are doing for `padding`.
- If you have to pass multiple values with `px` then you have to mention the whole things as a string like `margin`
- CSS properties that have a `-`, have to be written in camel case. That's why we have `fontSize` instead of `font-size`. So, if you want to use the `margin-bottom` property, we will have to use `marginBottom`.
- We can pass multiple values as a string when required like the `border` or `margin` properties in our example.

We can also set styling based on conditions, here is an example

```javascript
<p style={ { color: isActive ? 'yellowgreen' : 'darkgrey' } }>
  Based on condition
</p>
```

We are setting the `color` property based on a condition. But, you can see the disadvantage of this right, we have use the condition on every property. Classes would be very helpful here.  

## CSS files

Out of the box, CRA supports importing CSS files. We can import a CSS file directly into our component and all the classes defined in our CSS file will be available to us in JSX.

And it's very easy too. Make a css file and import it into your component.

Let's say we had a css file called `CssFileComponent.css`.

```css
.wrapper {
  background-color: antiquewhite;
  padding: 15px;
}

.greenText {
  color: green;
}

.multiple-properties {
  padding: 20px;
  margin: 20px 15px;
  font-size: 2rem;
  color: darkorange;
  border: 1px solid darkgrey;
}

.active {
  color: blue;
  cursor: pointer;
}

.disabled {
  color: grey;
}
```
It's a normal CSS file nothing fancy going on here.
Now import this css file into our component file

```javascript
import React from 'react';
import './CssFileComponent.css';

const CssFileComponent = ({ isActive }) => {
  return (
    <div className="wrapper">
      <p className="greenText">This text will be green</p>
      <p className="multiple-properties">Multiple CSS Properties</p>
      <p className={isActive ? 'active' : 'disabled'}>Based on condition</p>
    </div>
  );
};

export default CssFileComponent;
```

As you can see we can import the css file directly into our component and then use our classes. And the other thing is that we use `className` instead of `class` when we have to apply the a CSS class. You can read this post on [Quora](https://www.quora.com/Why-do-I-have-to-use-className-instead-of-class-in-ReactJs-components-done-in-JSX-JSX-is-preprocessed-so-shouldnt-that-conversion-happen-when-JSX-is-converted-to-JavaScript?share=1 "Quora link") to understand why.

## SASS files

[SASS](https://sass-lang.com/documentation) stands for Syntactically Awesome Stylesheet.
> Sass is a stylesheet language that’s compiled to CSS

You can check out more about SASS on it's [official page](https://sass-lang.com/documentation "SAS documentation").
To start using SASS in a CRA project you will only have to install one dependency `node-sass`;

Run the following command in your project directly:
`npm install node-sass` or `yarn add node-sass`

Once the installation is done we can start using SASS in our project. SASS files have `.scss` extension. Here is an example of a `.scss` file let's call it `SassStyleComponent.scss`

```scss
@import './variables.scss';

ul {
  margin: 0;
  padding: 0;
  list-style: none;
  li {
    display: inline-block;

    a {
      display: block;
      padding: 6px 12px;
      text-decoration: none;
      color: $primary-color;
      &:hover {
        color: $secondary-color;
      }
    }
  }
}
```

And here is the code for the `variable.scss` file we are importing. We are just declaring variables here.

```scss
$primary-color: #b2d534;
$secondary-color: #ff8c00;
```

Now to use this in our component file.

```javascript
import React from 'react';
import './SassStyleComponent.scss';

const SassStyleComponent = () => {
  return (
    <div>
      <ul>
        <li>
          <a href="#">This is a link</a>
        </li>
        <li>This is not a link</li>
      </ul>
    </div>
  );
};

export default SassStyleComponent;
```

We import the `scss` file just like we would a `css` file.

## CSS modules

With CSS modules we can define styles that are scoped at component level. This solves the problem of styles defined using `css` or `scss` file being global and applied to all components.

> CSS Modules allows the scoping of CSS by automatically creating a unique classname of the format [filename]\_[classname]\_\_[hash].

CRA supports CSS modules out of the box.

To start using CSS module use the following naming convention `[name].module.css`.

Let's create a CSS module file and call it `CSSModule.module.css`.

```css
.container {
  display: flex;
  flex-flow: column;
  align-items: center;
  justify-content: center;
}

.text {
  color: rgb(95, 158, 160);
  font-size: 16px;
}
```

Let's see how to include this file into our component.

```javascript
import React from 'react';
import styles from './CSSModule.module.css';

const CSSModuleComponent = () => {
  return (
    <div className={styles.container}>
      <p className={styles.text}>Test</p>
    </div>
  );
};

export default CSSModuleComponent;
```

We get a JavaScript object style from CSS module, hence we have to specify what we want to call this object. I have called it `styles` you can call it anything you want.
Inside this object we will have access to all our classes.

If you have a look at the DOM using the browser dev tools, our component will look something like this.

```html
<div class="CSSModule_container__2iMh-">
  <p class="CSSModule_text__37hvW">Test</p>
</div>
```
Note that I had named the component `CSSModuleComponent.js` hence the first part of the class name.

We can combine the power of SASS and CSS modules. Make sure you have `node-sass` installed as a dependency and name the file `.scss` instead of `.css`.

### CLSX
Earlier in this post we had seen how to apply classes based on a condition. But what if we have multiple conditions instead of one. For example we have a `Alert` component and this component takes in two props `text` and `type`. Now `type` can be `success`, `error` or `warning`.

Let's start with the component first.
```javascript
import React from 'react';

const Alert = ({ text, type }) => {
  return <div>{text}</div>;
};

export default Alert;
```
And the CSS.
```css
.container {
  display: flex;
  flex-flow: column;
  align-items: center;
  justify-content: center;
  padding: 20px;
}

.alert-success {
  border: 1px solid green;
  color: green;
  background-color: greenyellow;
}

.alert-error {
  border: 1px solid red;
  color: red;
  background-color: salmon;
}

.alert-warning {
  border: 1px solid orange;
  color: orange;
  background-color: orangered;
}

```
We can handle the condition inside our component like this:

```javascript
import React from 'react';
import './Alert.css';

const Alert = ({ text, type }) => {
  const classToApply = (type) => {
    if (type === 'success') return 'alert-success';
    if (type === 'error') return 'alert-error';
    if (type === 'warning') return 'alert-warning';
    return '';
  };

  return <div className={`container ${classToApply(type)}`}>{text}</div>;
};

export default Alert;
```

And this works perfectly fine but we will have to write these conditions in every component we want to have classes based on conditions. Or we could use the [`clsx`](https://www.npmjs.com/package/clsx "CLSX npm page") npm package to help us with it. `clsx` allows us to apply classes based on conditions.

First let's install `clsx` as a dependency in our project.

`npm install clsx` or `yarn add clsx`

Next we update our `Alert` component.

```javascript
import React from 'react';
import clsx from 'clsx';
import './Alert.css';

const Alert = ({ text, type }) => {
  return (
    <div
      className={clsx('container', {
        'alert-success': type === 'success',
        'alert-error': type === 'error',
        'alert-warning': type === 'warning',
      })}
    >
      {text}
    </div>
  );
};

export default Alert;
```

We have a default class `container` that is applied always. The other tree classes are applied based on if they meet the condition.

## CSS-in-JS libraries
CSS-in-JS libraries let you write CSS using JavaScript syntax. They allow you to write CSS in the same file as the component file and another advantage is they abstract CSS to the component level.
They are quite a few libraries that can be used to wirte CSS-in-JS.
We will have a look at [`styled-components`](https://styled-components.com/ "Styled components").

We will start with installingn`styled-components`

`npm install styled-components` or `yarn add styled-components`

Let's start with a component that renders a button.

```javascript
import styled from 'styled-components';
import React from 'react';

const Container = styled.div`
  display: flex;
  flex-flow: column;
  align-items: center;
  justify-content: center;
`;

const Text = styled.p`
  color: rgb(95, 158, 160);
  font-size: 16px;
`;

const ScComponent = () => {
  return (
    <Container>
      <Text>Not Primary</Text>
    </Container>
  );
};

export default ScComponent;
```

`Container` and `Text` are components we define using styled components. As you see we are using CSS in JS.

Component style can be changed based on props the component gets/

```javascript
import styled, { css } from 'styled-components';
import React from 'react';

const Container = styled.div`
  display: flex;
  flex-flow: column;
  align-items: center;
  justify-content: center;
`;

const Text = styled.p`
  color: rgb(95, 158, 160);
  font-size: 16px;

  ${(props) =>
    props.primary &&
    css`
      color: rgb(177 218 54);
      font-size: 18px;
    `};
`;

const ScComponent = () => {
  return (
    <Container>
      <Text>Not Primary</Text>
      <Text primary>Primary</Text>
    </Container>
  );
};

export default ScComponent;

```
