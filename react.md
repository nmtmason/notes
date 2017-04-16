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
