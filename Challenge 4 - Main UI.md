# Challenge 4 - Main UI
Implement main UI pages in the single page application and use data mocks to work with real data, but without the complexity of API integration.

- Passing content from Devise to the React components(将内容从 Devise 传递给 React 组件)
- Differentiating the React pages from the Devise forms(将 React 页面与 Devise 表单区分开来)

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
...
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
...
```

This is good foundational code, **but** ultimately `App.js` is going to be in charge of "big picture" functionality like routing and fetch calls so it would make more sense to move the sign_in and sign_out routes to another component like a Header or Nav.

**app/javascript/components/components/Header.js**
```
import React, { Component } from 'react'
import { NavLink } from 'react-router-dom'
...

class Header extends Component {
render() {
    const {
      logged_in,
      new_user_route,
      sign_in_route,
      sign_out_route
    } = this.props
    return (
      <header>
        <div className="nav-bar">
          <NavLink to="/" className="nav-link">Home</NavLink>
          {logged_in && <a href={sign_out_route} className="nav-link">Sign Out</a>}
          {!logged_in && <a href={sign_in_route} className="nav-link">Sign In</a>}
          {!logged_in && <a href={new_user_route} className="nav-link">Register</a>}
        </div>
      </header>
    )
  }
}
export default Header
```
**/app/assets/stylesheets/application.scss** 
```
@import 'bootstrap'

/* ---HEADER--- */
header {
  display: flex;
  justify-content: space-between;
  background-color: #A2F84B;
  position: fixed;
  width: 100%;
  top: 0
}

.nav-bar {
  display: flex;
  align-items: flex-end;
  padding-bottom: 10px;
}
.nav-link {
  margin: 10px;
  color: #8B0000;
  text-decoration: none;
}
.nav-link:hover {
  text-decoration: underline;
}
```

To use header, edit **app/javascript/components/App.js**
```
...
import Header from "./components/Header"
...
<Router>
  <Header/>
  ...
</Router>
...
```

## 5. CRUD Functionality

### Adding the CRUD "create" functionality using mock data
- Apartment create form

Utilize Reactstap to help with form styling. Reactstrap has an element called `<FormGroup>`. Nested in each `<FormGroup>` tag there will be a label and an input. Each input tag will take two attributes. The first is `type` that describes what information can be entered into the field. The second is `name` that matches the appropriate cat attribute. In this example the name of the input is "name" in reference to our cat name attribute.

Each cat attribute will have its own `<FormGroup>` inside of a single `<Form>` tag.

**components/pages/New.js**
```javascript
<Form>
  <FormGroup>
    <Label>Name</Label>
    <Input
      type="text"
      name="name"
    />
  </FormGroup>
</Form>
```

Complete the process by importing the Reactstrap components.

**components/pages/New.js**
```javascript
import {
  Form,
  FormGroup,
  Input,
  Label
} from 'reactstrap'
```

Here need to collect the user input and transmit the data as a set. Add a `value`, and an `onChange` attribute to the inputs. By adding a form object to state with reference `this.state.form` and have a complete apartment object that can be passed to `App.js` as a single unit rather than as individual values.

To set the inputs to state need a `handleChange` method to be called on every input.

- Passing Apartments to App.js

### Adding the CRUD "read" functionality using mock data
### Adding the CRUD "update" functionality using mock data
### Adding the CRUD "delete" functionality using mock data

## 6. API Validation

## 7. Testing

## 8. Git add/commit/push to new branch-setup
```
$ git status
$ git checkout -b main-ui
$ git add .
$ git commit -m "complete main ui"
$ git push origin main-ui
```
Pull request and review or waiting for review, then merge and delete the branch


[ Go to Next Step ](https://github.com/yanxu2021/ApartmentUs/blob/main/Challenge%205%20-%20API.md)

[ Go Back ](https://github.com/yanxu2021/ApartmentUs/blob/main/README.md)
