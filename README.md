# <img src="https://github.com/yanxu2021/ApartmentUs/blob/main/img/%23A2F84B.JPG" width="200" />ApartmentUs-Apartment App Challenge

This project uses Ruby on Rails to host React components in a monolithic application, and Devise, a Ruby gem to create user login.
```
app_name: ApartmentUs
slogan: Find apartment, Life community
打造新社区概念，提供在线寻找新型公寓，并建立公寓社区
Main color code: #A2F84B
```
As a developer, I have been commissioned to create an application where a user can see apartments that are available for rent. As a user, I can see a list of apartments. I can click on an apartment listing and see more information about that apartment. As a user, I can create an account and log in to the application. If I am logged in, I can add an apartment to the list. As a logged in user, I can see a list of all the apartments as well as just the apartments I added. If my work is acceptable to my client, I may also be asked to add the ability to remove an apartment from the list as well as edit the apartment information.

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
- [ Challenge 1 - Planning ](./Challenge 1 - Planning.md)

#### Challenge 2 - Set Up
[ Challenge 2 - Set Up ](./tools_and_resources/assessments.md)
**Troubleshooting Tips** Becuase now we are working in a new stack, the way we find error messages is going to look a little bit different. we are used to getting a browser display when something goes wrong. With this particular stack, we need to look for errors in the console and in the terminal. Any syntax errors or incorrect code anywhere in the React components will prevent `App.js` from compiling. So a mistake is likely to lead to a blank page.
- Stop the server and start it again.
- Did all the setup commands run properly? The commands can be rerun if something isn't working.
- Seeing a blank page? Look for errors in the terminal or inspect your page.
- Errors? Always look at the first error in the list.

#### Challenge 3 - Authentication
[ Challenge 3 - Authentication ](./tools_and_resources/assessments.md)
- Implement your authentication code, with stubbed out main pages

#### Challenge 4 - Main UI
[ Challenge 4 - Main UI ](./tools_and_resources/assessments.md)
- Implement your main UI pages in your single page application
- Use data mocks to work with real data, but without the complexity of API integration

#### Challenge 5 - API
[ Challenge 5 - API ](./tools_and_resources/assessments.md)
- Finish off your application by hooking up the Database via API endpoints
- Is everything secure?
