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
