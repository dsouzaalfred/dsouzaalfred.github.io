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

Let’s start by setting up a new project using CRA. Open a terminal/command prompt and navigate to the folder you want to setup the new project and use the following command:

`npx create-react-app react-styling`

Once all the dependencies are installed, navigate into the react-styling folder and start the local dev server using yarn start.

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
    padding: '20px',
    marginBottom: '20px',
    fontSize: '2rem',
    color: 'darkorange',
    border: '1px solid darkgrey',
  } }
>
  Multiple CSS Properties
</p>
```

Adding condition

```javascript
<p style={ { color: isActive ? 'yellowgreen' : 'darkgrey' } }>
  Based on condition
</p>
```

## CSS files
We can import a CSS file directly into our component and all the classes defined in our CSS file will be available to us in JSX.

className instead of class, that is the JSX syntax ([Read more here](https://www.quora.com/Why-do-I-have-to-use-className-instead-of-class-in-ReactJs-components-done-in-JSX-JSX-is-preprocessed-so-shouldnt-that-conversion-happen-when-JSX-is-converted-to-JavaScript?share=1 "Quora link"))

## SASS files

CRA supports SASS files out of the box.

## CSS modules

CRA supports CSS modules out of the box.

## CLSX

## CSS-in-JS libraries
