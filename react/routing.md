# React

## Routing

The most-used routing solution for React is [React Router](https://github.com/ReactTraining/react-router). A number of alternatives exist, some which leverage [Redux](https://github.com/reactjs/redux), including [redux-little-router](https://github.com/FormidableLabs/redux-little-router) and [redux-tiny-router](https://github.com/Agamennon/redux-tiny-router). For small apps, you could even use [history](https://github.com/reacttraining/history) to roll your own solution.

### Redirecting

In React Router 4, this is now as simple as using the Redirect component.

```javascript
import { Redirect } from 'react-router-dom'

const Home = ({ loggedIn }) => {
  if (!loggedIn) {
    return (
      <Redirect to="/login" />
    )
  }
  return (
    ...
  )
}

export default Home
```

### Providing routing context

It may be necessary to match the routing context in a component that hasn't been created with `<Route>`. React Router provides the `withRouter` higher order function for these situations. It provides the `match`, `location` and `history` props.

```javascript
import { withRouter } from 'react-router-dom'

const ComponentNotMountedWithRoute = ({ match, location, history }) => (
  <p>
    You're at {location.pathname}!
  </p>
)

export default withRouter(ComponentNotMountedWithRoute)
```
