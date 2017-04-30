# React

## Styling

React provides a number of ways to style it's components.

### Inline styles

You can modify the style of a component using inline styles in JavaScript. Specify the styles you would like to apply using a plain JavaScript object. Where in CSS you would hyphenate keywords, instead use camel case for the object properties. The object will be applied directly on the element using its `style` attribute.

Unfortunately it's not possible to use pseudo selectors with inline styles, nor are you able to use media queries.

```javascript
const style = {
  backgroundColor: 'goldenrod',
  color: 'white'
}

function StyledLink (props) {
  return (
    <a style={style} href={props.href}>{props.children}</a>
  )
}
```

### Radium

[Radium](https://github.com/FormidableLabs/radium) extends the use of inline styles in React. It overcomes the shortcomings of pure inline styles allowing you to use both pseudo selectors and media queries. It uses JavaScript to detect events and is able to switch styles accordingly.

```javascript
import Radium from 'radium'

const style = {
  backgroundColor: 'goldenrod',
  color: 'white',
  ':hover': {
    backgroundColor: 'white',
    color: 'goldenrod'
  }
}

function StyledLink (props) {
  return (
    <a style={style} href={props.href}>{props.children}</a>
  )
}

export default Radium(StyledLink)
```

### CSS Modules

[CSS Modules](https://github.com/css-modules/css-modules) move away from the CSS in JS approach and leverage vanilla CSS. They attempt to solve the problem of global CSS selectors by loading CSS scoped to a particular document. Unique class names are generated at the time of loading the document and are automatically referenced in your code. The webpack css-loader is used to generate class names without the need for additional plugins.

The following `webpack.config.js` configuration is used to turn on the feature.

```javascript
{
  test: /\.(css)$/,
  use: [
    'style-loader',
    {
      loader: 'css-loader',
      query: {
        modules: true,
        localIdentName: '[name]__[local]___[hash:base64:5]'
      }
    }
  ]
}
```

Styles are then loaded directly from your component.

```css
.styledLink {
  background-color: goldenrod;
  color: white;
}

.styledLink:hover {
  background-color: white;
  color: goldenrod;
}
```

```javascript
import styles from './StyledLink.css'

function StyledLink (props) {
  return (
    <a className={styles.styledLink} href={props.href}>{props.children}</a>
  )
}

export default StyledLink
```

This example generates CSS similar to to this:

```html
<a className="StyledLink_styledLink_36wru" href="#">I'm a styled link!</a>
```

### Styled Components

[Styled Components](https://github.com/styled-components/styled-components) take a different approach, combining the benefits of both CSS-in-JS and CSS Modules. Tagged template literals allow CSS to be written directly inside a JavaScript file. There are no limitations to the CSS that you can write - media queries and pseudo selectors are all valid. It's also possible to access JavaScript variables (using props) in your CSS. Similar to CSS Modules, the CSS that you write is hashed into a unique class name for a component taking it out of global scope.

```javascript
import styled from 'styled-components'

const StyledLink = styled.a`
  background-color: goldenrod;
  color: white;

  &:hover {
    background-color: white;
    color: goldenrod;
  }
`

export default StyledLink
```

In the example above, StyledLink behaves exactly like an `<a>` tag allowing you to pass props as you would normally. However, the StyledLink now has a className associated to it which refers back to the CSS it was created with.

You are not limited to default HTML elements when creating Styled Components. For example you could choose to style the Link component provided by React Router.

```javascript
import styled from 'styled-components'
import { Link } from 'react-router-dom'

const StyledLink = styled(Link)`
  background-color: goldenrod;
  color: white;

  &:hover {
    background-color: white;
    color: goldenrod;
  }
`

export default StyledLink
```

### Component State and Variations

It's often useful to encompass different states of a component. An input field for example may need to show an error state (perhaps a red border) when something has been entered incorrectly. You may also wish to create variations of components, such as smaller or larger versions of a button. This is achievable using both inline styles and CSS Modules.

Take a button component for example. As well as a single object, the `style` attribute will accept an array of styles. Any which evaluate to truthy are merged into the overall style for the component. We can take advantage of the logical `&&` operator which will short circuit if the `small` property hasn't been supplied.

```javascript
const style = {
  padding: '0.5rem 1rem',
  fontSize: '1rem'
}

const smallStyle = {
  padding: '0.25rem 0.5rem',
  fontSize: '0.8rem'
}

function StyledButton ({small, children ...props}) {
  return (
    <button style={[
      style,
      small && smallStyle
    ]} {...props}>{children}</button>
  )
}

export default StyledButton

// Usage:
// <StyledButton>
// <StyledButton small>
```

Whilst the `className` attribute doesn't accept an array of class names, we can still simulate the same trick in CSS Modules using a function.

```css
.styledButton {
  padding: 0.5rem 1rem;
  fontSize: 1rem;
}

.small {
  padding: 0.25rem 0.5rem;
  fontSize: 0.8rem;
}
```

```javascript
import style from './StyledButton.css'

function classes (...styles) {
  return styles.filter(function (style) {
    return !!style
  }).join(' ')
}

function StyledButton ({small, children ...props}) {
  return (
    <button className={classes(
      style.styledButton,
      small && style.small
    )}{...props}>{children}</button>
  )
}

export default StyledButton
```
Or we can use the handy [classnames](https://github.com/JedWatson/classnames) module for this!
