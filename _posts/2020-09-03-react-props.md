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

Props or properties is data passed to a component. A parent component will pass data to a child component as a prop.
Couple of thinks to note about Props:
- `props` is keyword is react and cannot be used as a variable name.
- `props` are immutable i.e. they are read-only

Now that we know a bit more about props lets start using it. When we define a component props are like function arguments in JavaScript.
```javascript
import React from 'react';

const PropsExample = (props) => {
  return <h1>{props.title}</h1>
}

export default PropsExample;
```

In the above component is expecting a parent component to pass data for the title props and it will display the value for title as a h1.

And when we have use our component in a parent component props will be like attributes in HTML.
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

We can pass any type of data as a prop.
- Strings
- Numbers
- Arrays
- Objects
- Boolean

We covered using JSX in our [last post](/blog/react/jsx-what-is-that/).
- Data
- Methods
- Other components
  - Children
- Proptypes
    - Types
    - isRequired
    - https://reactjs.org/docs/typechecking-with-proptypes.html
- Default props
