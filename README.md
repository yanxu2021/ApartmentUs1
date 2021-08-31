# Apartment App Challenge--ApartmentUs
```
This project uses Ruby on Rails to host React components in a monolithic application,and Devise, a Ruby gem to create user login.
```

```
app_name: ApartmentUs
slogan: Find apartment, Life community
打造新社区概念，提供在线寻找新型公寓，并建立公寓社区

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
