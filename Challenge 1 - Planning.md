# Challenge 1 - Planning
## :thought_balloon: Draw out a proposed database schema
```
 Story: As an un-registered guest on the website, I can go to a web page and see a list of available apartments. 
 Apartments have: a street designation, a city, state, a manager's name, manager's contact email, 
 monthly rental price, bedrooms, bathrooms, and whether they allow pets.
 
 Story: As an un-registered guest on the website, I can click on an apartment to view its details.
 
 Story: As an un-registered guest on the website, 
 I can see a header element at the top of each page containing navigation to the other pages.
 
 Story: As a un-registered guest, I can go to registration page with a form and register as a new user.
 
 Story: As a registered user who has not logged in, I can go to a login page.
 
 Story: As a logged in user, I should be able to log out.
 
 Story: As a logged in user, I can go to a new apartment page with a form and create a new apartment.
 
 Story:: As a logged in user, I can edit the information for any apartment I have created, 
 but I cannot edit the information for apartments that belong to someone else.
```
**Tool**: Dbdiagram.io is a free online database diagraming tool for developers and data analysts. It uses a code-based user interface, and you can create up to 10 diagrams for free.

![database schema](https://github.com/yanxu2021/ApartmentUs/blob/main/img/database%20%20schema.JPG)

**db/seeds.rb**
```ruby
# This file should contain all the record creation needed to seed the database with its default values.
# The data can then be loaded with the bin/rails db:seed command (or created alongside the database with db:setup).
#
# Examples:
#
#   movies = Movie.create([{ name: 'Star Wars' }, { name: 'Lord of the Rings' }])
#   Character.create(name: 'Luke', movie: movies.first)

users = [
  {
    email: 'xu@apartmentus.com',
    password: 'password1!'
  },
  {
    email: 'yan@apartmentus.com',
    password: 'password2!'
  }
]

users.each do |attr|
  User.create attr
  p "creating user #{attr}"
end

apartments = [
  {
    street: '9130 Nolan St.',
    city: 'Elk Grove',
    state: 'Ca',
    manager: 'manager',
    email: 'manager@sienavillas.com',
    price: '$2,889 / month',
    bedrooms: 2,
    bathrooms: 2,
    pets: 'Pets Welcome!'
  },
  {
    street: '10270 E Taron Dr.',
    city: 'Elk Grove',
    state: 'CA',
    manager: 'info',
    email: 'info@stonelake.com',
    price: '$2,235/ month',
    bedrooms: 2,
    bathrooms: 1,
    pets: 'Large animals not permitted.'
  },
  {
    street: '3300 Renwick Ave.',
    city: 'Elk Grove',
    state: 'CA',
    manager: 'castellino',
    email: 'cast@castellino.com',
    price: '$4,567 / month',
    bedrooms: 3,
    bathrooms: 2,
    pets: 'Pets permitted with deposit'
  },
  {
    street: '9589 Four Winds Dr.',
    city: 'Elk Grove',
    state: 'CA',
    manager: 'Susan',
    email: 'susan@lakepoint.com',
    price: '$2,302 / month',
    bedrooms: 2,
    bathrooms: 2,
    pets: 'Please call for details.'
  }
]

xu = User.where(email: 'xu@apartmentus.com').first
yan = User.where(email: 'yan@apartmentus.com').first

apartments.each_with_index do |attr, index|
  if index < 2
    xu.apartments.create attr
    p "creating apartment #{attr}"
  else
    yan.apartments.create attr
    p "creating apartment #{attr}"
  end
end

```


## :thought_balloon: What tables do you anticipate you will need?
**user table** and **apartment table**
## :thought_balloon: What associations do your tables have?
User can have many apartments and apartment belong to user's.
## :thought_balloon: Explore some of the free Bootstrap themes available, which one do you want to use?
Bootstrap is a free and open-source CSS framework directed at responsive, mobile-first front-end web development. It contains CSS- and JavaScript-based design templates for typography, forms, buttons, navigation, and other interface components.
## :thought_balloon: Wireframe the main pages in the application.
 1. Home.js
 2. AboutUs.js
 3. New.js
 4. Index.js
 5. Show.js
 6. Edit.js
 7. NotFound.js
## :thought_balloon: What forms will you need?
## :thought_balloon: What fields are on those forms?
## :thought_balloon: Do your forms match your database schema?
## :thought_balloon: What are the user flows?
## :thought_balloon: Protected vs. unprotected pages?
## :thought_balloon: What is the most important user flow of the application?
## :thought_balloon: Is this flow easy and intuitive for the user?

[ Go Back ](https://github.com/yanxu2021/ApartmentUs/blob/main/README.md)
