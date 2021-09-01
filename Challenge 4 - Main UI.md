# Challenge 4 - Main UI
Implement your main UI pages in your single page application and use data mocks to work with real data, but without the complexity of API integration.

We are going to combine what we've learned about Devise with what we've learned about React to build a React application that offloads authentication responsibilities to Devise.
- Passing content from Devise to the React components
- Differentiating the React pages from the Devise forms

## 1. React Component View
Add a view and add React component. In addition to rendering the "App" component in the view, we can pass information from Rails into React. Here we want to pass information down from Devise into our React App:
1. If user is logged in or not
2. The id of the current user
3. Relative URL of signup screen (from Devise)
2. Relative URL of login screen for users who already have an account (from Devise)
3. Relative URL of logout endpoint (also from Devise)

**app/views/home/index.html.erb**
```
<%= react_component "App", {
  logged_in: user_signed_in?,
  current_user: current_user,
  new_user_route: new_user_registration_path,
  sign_in_route: new_user_session_path,
  sign_out_route: destroy_user_session_path
} %>
```
## 2. Routes and Constraints
We need to clearly separate the Rails routing responsibilities, and the React routing responsibilities. We also need to route the `index.html.erb` page to the root.

**config/routes.rb**
```ruby
Rails.application.routes.draw do
  resources :apartments
  devise_for :users
  get '*path', to: 'home#index', constraints: ->(request){ request.format.html? }
  root 'home#index'
end
```
This route directs all HTML traffic to the 'home#index' route, but ignores non HTML traffic, like our API requests. That is perfect to interact with the React router.

## 3. Login/Logout Button
With login status and routes in our React component, we can now add a button to log the user out or in.

First we need to instruct Devise to listen for logout requests via GET instead of the default DELETE. We do that in Devise's config file:

**config/initializers/devise.rb**
```ruby
# Find this line:
config.sign_out_via = :delete
# and replace it with this:
config.sign_out_via = :get
```

To start, let's look at creating the buttons directly in `App.js` then break them out into another component. The first thing is bringing in the three pieces of information that get passed from devise to "App" in *index.html.erb*.

That is followed with some conditional rendering to display the appropriate link depending on if the user is logged in or logged out.

**app/javascript/components/App.js**
```javascript
import React from "react"
import PropTypes from "prop-types"

class App extends React.Component {
  render() {
    const {
      logged_in,
      current_user,
      new_user_route,
      sign_in_route,
      sign_out_route
    } = this.props
    return (
      <React.Fragment>
        { logged_in &&
          <div>
            <a href={sign_out_route }>Sign Out</a>
          </div>
        }
        { !logged_in &&
          <div>
            <a href={ sign_in_route }>Sign In</a>
          </div>
        }
      </React.Fragment>
    )
  }
}

export default App
```

This is good foundational code, **but** ultimately `App.js` is going to be in charge of "big picture" functionality like routing and fetch calls so it would make more sense to move the sign_in and sign_out routes to another component like a Header or Nav.

Create app logo-logo.jpg, **../assets/logo.jpg**

**app/javascript/components//components/Header.js**
```
import React, { Component } from 'react'
import { NavLink } from 'react-router-dom'
import logo from '../assets/logo.jpg'

class Header extends Component {
  render() {
    const {
      logged_in,
      sign_in_route,
      sign_out_route
    } = this.props
    return (
      <header>
        <NavLink to="/">
          <img src={logo} alt="apartment app logo" className="logo"/>
        </NavLink>
        <div className="nav-bar">
          <ul>
            <NavLink to="/apartmentIndex" className="nav-link">See All the Apartments</NavLink>
          </ul>
          <ul>
            {logged_in &&
              <a href={sign_out_route} className="nav-link">Sign Out</a>
            }
            {!logged_in &&
              <a href={sign_in_route} className="nav-link">Sign In</a>
            }
          </ul>
        </div>
      </header>
    )
  }
}
export default Header
```


[ Go to Next Step ](https://github.com/yanxu2021/ApartmentUs/blob/main/README.md)
[ Go Back ](https://github.com/yanxu2021/ApartmentUs/blob/main/README.md)
