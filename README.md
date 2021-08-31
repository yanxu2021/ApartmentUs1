# <img src="https://github.com/yanxu2021/ApartmentUs/blob/main/img/%23A2F84B.JPG" width="200" />ApartmentUs 
## Apartment App Challenge

```
This project uses Ruby on Rails to host React components in a monolithic application,
and Devise, a Ruby gem to create user login.
```

```
app_name: ApartmentUs
slogan: Find apartment, Life community
打造新社区概念，提供在线寻找新型公寓，并建立公寓社区
Main color code: #A2F84B

```
As a developer, I have been commissioned to create an application where a user can see apartments that are available for rent. As a user, I can see a list of apartments. I can click on an apartment listing and see more information about that apartment. As a user, I can create an account and log in to the application. If I am logged in, I can add an apartment to the list. As a logged in user, I can see a list of all the apartments as well as just the apartments I added. If my work is acceptable to my client, I may also be asked to add the ability to remove an apartment from the list as well as edit the apartment information.

## Troubleshooting Tips
- Did you create your database?
- Did you migrate?
- Errors? Always look at the first error in the list.

## User Stories
**Story:** As an un-registered guest on the website, I can go to a web page and see a list of available apartments. Apartments have: a street designation, a city, state, a manager's name, manager's contact email, monthly rental price, bedrooms, bathrooms, and whether they allow pets

**Story:** As an un-registered guest on the website, I can click on an apartment to view its details

**Story:** As an un-registered guest on the website, I can see a header element at the top of each page containing navigation to the other pages

**Story:** As a un-registered guest, I can go to registration page with a form and register as a new user

**Story:** As a registered user who has not logged in, I can go to a login page

**Story:** As a logged in user, I should be able to log out

**Story:** As a logged in user, I can go to a new apartment page with a form and create a new apartment

**Story:**: As a logged in user, I can edit the information for any apartment I have created, but I cannot edit the information for apartments that belong to someone else

## Process
#### Challenge 1 - Planning
- Draw out a proposed database schema
- What tables do you anticipate you will need?
- What associations do your tables have?
- Explore some of the free Bootstrap themes available, which one do you want to use?
- Wireframe the main pages in the application.
- What forms will you need?
- What fields are on those forms?
- Do your forms match your database schema?
- What are the user flows?
- Protected vs. unprotected pages?
- What is the most important user flow of the application?
- Is this flow easy and intuitive for the user?
#### Challenge 2 - Set Up
- The setup includes **adding React to the Rails application and adding Webpacker to compile JavaScript.**
```
$ git clone GitHubRepositoryLink
```

```
$ rails new apartment_us -d postgresql -T
$ cd apartment_us
$ rails db:create
$ bundle add react-rails
$ rails webpacker:install
$ rails webpacker:install:react
$ rails generate react:install
```
记住：因为先git clone了repository，所以建立的git是在上一层目录里。每一次git add、commit、push都要到上一层目录里去操作。每一次git之前都git status check 一下。另外养成习惯，完成一项任务push一次，每一次操作之前确认所在目录。
- **Troubleshooting Tips**
Now that we are working in a new stack, the way we find error messages is going to look a little bit different. We are used to getting a browser display when something goes wrong. With this particular stack, we need to look for errors in the console and in the terminal. Any syntax errors or incorrect code anywhere in the React components will prevent `App.js` from compiling. So a mistake is likely to lead to a blank page.
```
- Stop the server and start it again.
- Did all the setup commands run properly? The commands can be rerun if something isn't working.
- Seeing a blank page? Look for errors in the terminal or inspect your page.
- Errors? Always look at the first error in the list.
```
<hr>

There are many ways to create a full-stack application.  Once we have a Rails application we can **add a React component** using a generate command.
```
$ `rails generate react:component App`
```

The install commands created a directory in `app` called `javascript`. In `app/javascript` there will be another directory called `components` that will contain our `App.js` React component with some basic code

*app/javascript/components/App.js*

Add an `h1` tag to the React component
```javascript
  render () {
    return (
      <React.Fragment>
        <h1>hello world!</h1>
      </React.Fragment>
    );
  }
```

- **generate a controller** so that we can route the React component can be rendered in a Rails view. This is the only Rails view we will make. Everything else will come from the React components.
```
$ `rails g controller Home`
```
- **Add a file in app/views/home called index.html.erb** By calling the React Component in `erb` tags the component will be rendered in the browser through the Rails view
*app/views/home/index.html.erb*
```javascript
 <%= react_component 'App' %>
```
Now we need to make sure we route to the appropriate file for our views.

- **Create a route** so the React component will be rendered in a Rails view.
*config/routes.rb*
```ruby
Rails.application.routes.draw do
  root 'home#index'
end
```
- **Adding Reactstrap to the application** allows for the use of a library of pre-built components. Reactstrap works in conjunction with Bootstap's core CSS. To add these libraries requires a little bit of setup to make the React styles compatible with Rails. There are many ways to add bootstrap to a Rails app, all of which will work equally well. 

Here is going to modify the Rails stylesheet to be a stylesheet with an `.scss` extension. This will allow us to write regular `css` code as well as import necessary dependencies. *scss* stands for Syntactially Awesome Styles Sheet and is a superset of css. It contains all of the functionality available in css with the addition of features such as imports and mixins.
```
$ bundle add bootstrap
$ mv app/assets/stylesheets/application.css app/assets/stylesheets/application.scss
$ yarn add reactstrap
```

- **Add an import to the `scss` file**. Make sure to stop your server and restart after the performing these commands.
*app/assets/stylesheets/application.scss*
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

Due to Rails convention, the React file structure lives in the *app/javascript/components* directory. 

**Note:** While it may seem a bit confusing, the React components directory will be nested inside of the Rails components directory. The Rails component directory takes the place of the `src` directory in a typical React application.

- **Add Pages**
For this application, we are going to have three pages:
`Home.js`
`AboutUs.js`
`AddApartment.js`

- **Add an `<h3>` to each describing their intent**
*app/javascript/components/pages/Home.js*
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

- In order to have multiple pages we need to **add the React Router**.
```
$ yarn add react-router-dom
```
Import the React-router and appropriate pages.
*app/javascript/components/App.js*
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
- **Add the basic routes to allow for navigation**.
*app/javascript/components/App.js*
```javascript
<Router>
  <Switch>
    <Route exact path="/" component={ Home } />
    <Route path="/about" component={ AboutUs } />
    <Route path="/add" component={ AddApartment } />
  </Switch>
</Router>
```
- **Routing Constraints**
Rails has a router, and now added React Router. These two routers could come into conflict. Reals路由会和React路由发生冲突。Here need to clearly separate the Rails routing responsibilities, and the React routing responsibilities. 

Here to build a single page app. This, by definition, means that all HTML traffic goes to just one page. All other types of requests though, will need to be routed by the Rails app. 

Most important of these, is the JSON and JavaScript traffic that the Rails app must handle, these requests can be thought as API requests from the frontend app to the backend one.

The Rails Router has a convenient feature that can be used to achieve this separation of traffic, all HTML requests go to React app, and everything else be handled normally.
*config/routes.rb*
```ruby
Rails.application.routes.draw do
  get '*path', to: 'home#index', constraints: ->(request){ request.format.html? }
  root 'home#index'
end
```
Notice the "constraints" section. This states that all HTML traffic goes to `home#index` React app.

- **Add Navigation Components**
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
<hr>

#### Challenge 3 - Authentication
- Implement your authentication code, with stubbed out main pages
#### Challenge 4 - Main UI
- Implement your main UI pages in your single page application
- Use data mocks to work with real data, but without the complexity of API integration
#### Challenge 5 - API
- Finish off your application by hooking up the Database via API endpoints
- Is everything secure?

## Implement
#### Setup
- Made a Rails app, and db
```
$ rails new apartment_app -d postgresql -T
$ cd apartment_app
$ rails db:create
```
- Added the remote from github, created default branch
```
$git remote add origin GitHubLink
$git checkout -b main
$git push origin main
```
#### Installs
- Branch: adding-devise
- Adding RSpec:
```
$ bundle add rspec-rails
$ rails generate rspec:install
```
- Adding Devise:
```
$ bundle add devise
$ rails generate devise:install
$ rails generate devise User
$ rails db:migrate
```

#### Apartment Model
```
$ rails g resource Apartment street:string city:string state:string manager:string email:string 
price:string bedrooms:integer bathrooms:integer pets:string user_id:integer
```
- Define relationship between User and Apartment
- Created seeds

#### Adding React
- Branch: adding-react
```
$ bundle add react-rails
$ rails webpacker:install
$ rails webpacker:install:react
$ rails generate react:install
$ rails generate react:component App
$ rails generate controller Home
```
- Created index.hmtl.erb in the view folder for home
- Call react component in index.html.erb
- Added root in routes file
- Passed in devise info to App.js
```
$ yarn add react-router-dom
```
- Configured the devise signout route to be a get request
- Checked the sign in and sign out routes with conditional rendering

#### User Stories

- **Devise and Header Stories**
- Story: As a un-registered guest, I can go to registration page with a form and register as a new user
  - Devise, navigation from Header component
- Story: As a registered user who has not logged in, I can go to a login page
  - Devise, navigation from Header component
- Story: As a logged in user, I should be able to log out
  - Devise, navigation from Header component
- Story: As an un-registered guest on the website, I can see a header element at the top of each page containing navigation to the other pages
  - Header component
- Process:
  - Header component (done)
  - Styling (added to the TODO items)
  - Navigation to Devise (done)
  - Navigation Index (done)
    - Create index page, basic code
    - Define the route to index page
  - Testing the Header
    - $ yarn add jest
    - $ yarn add -D enzyme react-test-renderer enzyme-adapter-react-16
    - Add this to the package.json:
     "jest": {
        "roots": [
          "app/javascript/components"
        ]
      }

TODO: More styling on the header
TODO: Testing the header


- **Read**
- Story: As an un-registered guest on the website, I can go to a web page and see a list of available apartments. Apartments have: a street designation, a city, state, a manager's name, manager's contact email, monthly rental price, bedrooms, bathrooms, and whether they allow pets
  - Index
    - Have an index page but nothing on it yet
    -
- Story: As an un-registered guest on the website, I can click on an apartment to view its details
  - Show

- **Create**
- Story: As a logged in user, I can go to a new apartment page with a form and create a new apartment
  - Create, only if you are logged_in, Desive

- **Update**
- Story: As a logged in user, I can edit the information for any apartment I have created, but I cannot edit the information for apartments that belong to someone else
  - Edit, only apartments with the foreign key of the current user

- $ rails db:seed
