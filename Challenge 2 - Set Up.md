# Challenge 2 - Set Up

## 1.  Create new APP and set up the Git

- Create new app 
```
$ rails new apartment_us -d postgresql -T
$ cd apartment_us
$ rails db:create
```

- Add the remote from GitHub, created default branch
```
$git remote add origin GitHubLink
$git checkout -b main
$git push origin main
```

注意：如果remote add的repository不是空的，一定要记得fetch and pull，让本地和远程同步了，才能把修改的内容push。切记：一定要注意建立main branch，后续pull request要与main进行compare。

- Add React to the Rails application and adding Webpacker to compile JavaScript.
```
$ bundle add react-rails
$ rails webpacker:install
$ rails webpacker:install:react
$ rails generate react:install
```
## 2. Create a full-stack application

There are many ways to create a full-stack application. Once we have a Rails application we can **add a React component** using a generate command.
```
$ rails generate react:component App
```
The install commands created a directory in `app` called `javascript`. In `app/javascript` there will be another directory called `components` that will contain `App.js` React component with some basic code

**app/javascript/components/App.js**
- Add an `h1` tag to the React component
```javascript
  render () {
    return (
      <React.Fragment>
        <h1>hello world!</h1>
      </React.Fragment>
    );
  }
```

## 3. Generate a controller
Generate a controller so that we can route the React component can be rendered in a Rails view. This is the only Rails view we will make. Everything else will come from the React components.
```
$ `rails g controller Home`
```
- Add a file in app/views/home called index.html.erb By calling the React Component in `erb` tags the component will be rendered in the browser through the Rails view

**app/views/home/index.html.erb**
```javascript
 <%= react_component 'App' %>
```
Now we need to make sure we route to the appropriate file for our views.

- Create a route so the React component will be rendered in a Rails view.

**config/routes.rb**
```ruby
Rails.application.routes.draw do
  root 'home#index'
end
```
- Add Reactstrap to the application allows for the use of a library of pre-built components. 

Reactstrap works in conjunction with Bootstap's core CSS. To add these libraries requires a little bit of setup to make the React styles compatible with Rails. There are many ways to add bootstrap to a Rails app, all of which will work equally well. 

Here is going to modify the Rails stylesheet to be a stylesheet with an `.scss` extension. This will allow us to write regular `css` code as well as import necessary dependencies. *scss* stands for Syntactially Awesome Styles Sheet and is a superset of css. It contains all of the functionality available in css with the addition of features such as imports and mixins(Mixins allow you to define styles that can be re-used throughout your stylesheet. They make it easy to avoid using non-semantic classes like . float-left , and to distribute collections of styles in libraries.).

```
$ bundle add bootstrap
$ mv app/assets/stylesheets/application.css app/assets/stylesheets/application.scss
$ yarn add reactstrap
```

- Add an import to the `scss` file. Make sure to stop your server and restart after the performing these commands.

**app/assets/stylesheets/application.scss**
```css
@import 'bootstrap';
```

At this point, there is only one React component in the application. Just like in a regular React App, this project will have many, many components. To keep the files organized, it is a good practice to create three directories in your React application: assets, components, and pages.

1. **assets**
The assets directory is used to store image files used in your application.

2. **components**
The components directory is for helper components such as headers, footers, and buttons.

3. **pages**
The pages directory is for full views. The full view can consist of items from the assets and components directory as well a code unique to a page.

Due to Rails convention, the React file structure lives in the **app/javascript/components** directory. 

**Note:** While it may seem a bit confusing, the React components directory will be nested inside of the Rails components directory. The Rails component directory takes the place of the `src` directory in a typical React application.

- Add Pages
For this application, we are going to have three pages:

1. `Home.js`
2. `AboutUs.js`
3. `AddApartment.js`

- Add an `<h3>` to each describing their intent
- 
**app/javascript/components/pages/Home.js**
```javascript
import React from "react"
class Home extends React.Component {
  render() {
    return(
      <h3>This is the Home Page</h3>
    )
  }
}
export default Home
```

The other two are mostly the same.

- In order to have multiple pages we need to add the React Router.

```
$ yarn add react-router-dom
```

Import the React-router and appropriate pages.

**app/javascript/components/App.js**
```javascript
import {
  BrowserRouter as  Router,
  Route,
  Switch
} from "react-router-dom"
import Home from "./pages/Home"
import AboutUs from "./pages/AboutUs"
import AddApartment from "./pages/AddApartment"
```

- Add the basic routes to allow for navigation.

**app/javascript/components/App.js**
```javascript
<Router>
  <Switch>
    <Route exact path="/" component={ Home } />
    <Route path="/about" component={ AboutUs } />
    <Route path="/add" component={ AddApartment } />
  </Switch>
</Router>
```

## 4. Routing Constraints

Rails has a router, and now added React Router. These two routers could come into conflict. Reals路由会和React路由发生冲突。Here need to clearly separate the Rails routing responsibilities, and the React routing responsibilities. 

Here to build a single page app. This, by definition, means that all HTML traffic goes to just one page. All other types of requests though, will need to be routed by the Rails app. 

Most important of these, is the JSON and JavaScript traffic that the Rails app must handle, these requests can be thought as API requests from the frontend app to the backend one.

The Rails Router has a convenient feature that can be used to achieve this separation of traffic, all HTML requests go to React app, and everything else be handled normally.
**config/routes.rb**
```ruby
Rails.application.routes.draw do
  get '*path', to: 'home#index', constraints: ->(request){ request.format.html? }
  root 'home#index'
end
```
Notice the "constraints" section. This states that all HTML traffic goes to `home#index` React app.

- Add Navigation Components
Using Reactstrap to add the navigation code.
*app/javascript/components/App.js*
```javascript
import React from "react"
import PropTypes from "prop-types"
import {
  BrowserRouter as  Router,
  NavLink,
  Route,
  Switch
} from "react-router-dom"
import { Nav, NavItem } from "reactstrap"
import Home from "./pages/Home"
import AboutUs from "./pages/AboutUs"
import AddApartment from "./pages/AddApartment"

class App extends React.Component{
  render(){
    return(
      <Router>
        <h1>This is a React Component</h1>
        <Nav>
          <NavItem>
            <NavLink to="/">Home</NavLink>
          </NavItem>
          <NavItem>
            <NavLink to="/about">About Us</NavLink>
          </NavItem>
          <NavItem>
            <NavLink to="/add">Add Apartment</NavLink>
          </NavItem>
        </Nav>
        <Switch>
          <Route exact path="/" component={ Home } />
          <Route path="/about" component={ AboutUs } />
          <Route path="/add" component={ AddApartment } />
        </Switch>
      </Router>
    )
  }
}
export default App
```
.[setup](https://github.com/yanxu2021/ApartmentUs/blob/main/img/1.png)

## 5. Git add/commit/push to new branch-setup
```
$ git status
$ git checkout -b setup
$ git add .
$ git commit -m "complete setup"
$ git push origin setup
```
- Pull request and review or waiting for review, then merge and delete the branch"

[ Go Back ](https://github.com/yanxu2021/ApartmentUs/blob/main/README.md)
