# <img src="https://github.com/yanxu2021/ApartmentUs/blob/main/img/%23A2F84B.JPG" width="200" />ApartmentUs-Apartment App Challenge

This project uses **Ruby on Rails** to host **React components** in a monolithic(/ˌmɑːnəˈlɪθɪk/adj. 整体的；完全统一的) application, and **Devise**, a Ruby gem to create user login.
```
app_name: ApartmentUs
slogan: Find apartment, Life community

We create a community for all people own or looking for an apartment, 
not only a location but also a life style.

**Community designed for Place, Purpose, and Profitability.**

It can be tough to find the right place to call your next home, 
and finding it before it gets snapped up by another renter can be even tougher. 
In a competitive market, available apartments come and go in a moment's notice, 
and a rental open house can feel more like a face-off with other renters than a tour of the space.

Fortunately, we are here to provide more accurate availabilities and better search options, 
which benefits you as more useful information becomes available with a tap of a finger. 
We are not only making it easier to sign a lease, 
but also sharing you more information about the community you are going to be invoved.
```
As a developer, I have been commissioned to create an application where a user can see apartments that are available for rent. As a user, I can see a list of apartments. I can click on an apartment listing and see more information about that apartment. As a user, I can create an account and log in to the application. If I am logged in, I can add an apartment to the list. As a logged in user, I can see a list of all the apartments as well as just the apartments I added. If my work is acceptable to my client, I may also be asked to add the ability to remove an apartment from the list as well as edit the apartment information.
- As a developer, I can create a Rails application with Devise functionality
- As a developer, I can create an Apartment resource with the appropriate attributes
- As a developer, I can create an association between User and Apartments
- As a developer, I can add React components to my apartment app
- As a developer, I ensure my app distinguishes the difference between JSON and HTML payloads in my routes

## User Stories
**Story:** As an un-registered guest on the website, I can go to a web page and see a list of available apartments. Apartments have: a street designation, a city, state, a manager's name, manager's contact email, monthly rental price, bedrooms, bathrooms, and whether they allow pets

**Story:** As an un-registered guest on the website, I can click on an apartment to view its details

**Story:** As an un-registered guest on the website, I can see a header element at the top of each page containing navigation to the other pages

**Story:** As a un-registered guest, I can go to registration page with a form and register as a new user

**Story:** As a registered user who has not logged in, I can go to a login page (navigate to a log in page)

**Story:** As a logged in user, I should be able to log out

**Story:** As a logged in user, I can go to a new apartment page with a form and create a new apartment

**Story:**: As a logged in user, I can edit the information for any apartment I have created, but I cannot edit the information for apartments that belong to someone else

## Process

[ Challenge 1 - Planning ](https://github.com/yanxu2021/ApartmentUs/blob/main/Challenge%201%20-%20Planning.md)

Q&A, user stories, data schema, wireframe, 

[ Challenge 2 - Set Up ](https://github.com/yanxu2021/ApartmentUs/blob/main/Challenge%202%20-%20Set%20Up.md)

**Troubleshooting Tips** Becuase now we are working in a new stack, the way we find error messages is going to look a little bit different. we are used to getting a browser display when something goes wrong. With this particular stack, we need to look for errors in the console and in the terminal. Any syntax errors or incorrect code anywhere in the React components will prevent `App.js` from compiling. So a mistake is likely to lead to a blank page.
- Stop the server and start it again.
- Did all the setup commands run properly? The commands can be rerun if something isn't working.
- Did you create your database?
- Did you migrate?
- Seeing a blank page? Look for errors in the terminal or inspect your page.
- Errors? Always look at the first error in the list.

[ Challenge 3 - Authentication ](https://github.com/yanxu2021/ApartmentUs/blob/main/Challenge%203%20-%20Authentication.md)

Implement your authentication code, with stubbed out main pages

[ Challenge 4 - Main UI ](https://github.com/yanxu2021/ApartmentUs/blob/main/Challenge%204%20-%20Main%20UI.md)

Implement your main UI pages in your single page application

Use data mocks to work with real data, but without the complexity of API integration

[ Challenge 5 - API ](https://github.com/yanxu2021/ApartmentUs/blob/main/Challenge%205%20-%20API.md)

Finish off your application by hooking up the Database via API endpoints

Is everything secure?
