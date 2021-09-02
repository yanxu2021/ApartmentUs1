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

<img src="https://github.com/yanxu2021/ApartmentUs/blob/main/img/database%20%20schema.JPG" width="600"/>

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
1. user table 
2. apartment table

## :thought_balloon: What associations do your tables have?
User **has_many** apartments and apartment **belong_to** user.

## :thought_balloon: Explore some of the free Bootstrap themes available, which one do you want to use?
**Bootstrap** is a free and open-source CSS framework directed at responsive, mobile-first front-end web development. It contains CSS- and JavaScript-based design templates for typography, forms, buttons, navigation, and other interface components.

## :thought_balloon: Wireframe the main pages in the application.
A **wireframe** is a schematic or blueprint that is useful for helping you, your programmers and designers think and communicate about the structure of the software or website you're building.

Tools: Wireframe.cc

 1. Home.js

<img src="https://github.com/yanxu2021/ApartmentUs/blob/main/img/homepagewireframe.JPG" width="600"/>

 2. AboutUs.js
 3. NotFound.js
 
 4. New.js
 5. Index.js
 6. Show.js

  
 7. Header.js
 8. Footer.js
## :thought_balloon: What forms will you need? What fields are on those forms? Do your forms match your database schema?
1. sign up form-support by **Devise**, a Ruby gem to create user login.
2. create form(3. update form)

```javaScript
import React, { Component } from 'react'
import { Button, Form, FormGroup, Label, Input, FormText } from 'reactstrap'
import { Redirect } from 'react-router-dom'


class New extends Component {
    constructor(props){
        super(props)
        this.state = {
        form:{
            street: "",
            city: "",
            state: "",
            manager: "",
            email: "",
            price: "",
            bedrooms: "",
            bathrooms: "",
            pets: "",
            user_id: this.props.current_user.id
        },
        submitted: false
        }
    }
    
    handleChange = (e) => {
        let { form } = this.state
        form[e.target.name] = e.target.value
        this.setState({form: form})
    }

    handleSubmit = () => {
        this.props.createApartment(this.state.form)
        this.setState({submitted: true})
    }
    
    render() {
        const { street, city, state, manager, email, price, bedrooms, bathrooms, pets } = this.state.form
        return (
            <div >
                <Form>
                    <FormGroup>
                        <Label for="street">
                            Street
                        </Label>
                        <br />
                        <Input
                            type="text"
                            name="street"
                            onChange={this.handleChange}
                            value={street}
                        />
                    </FormGroup>
                    <br />
                    
                    <FormGroup>
                    ...
                    </FormGroup>
                    <br/>
                    
                    ...
                    
                    <Button onClick={this.handleSubmit}>Submit</Button>
                </Form>
                {this.state.submitted && <Redirect to="/myapartments" />}
            </div>
        )
    }
}

export default New
```

## :thought_balloon: What are the user flows? What is the most important user flow of the application? Is this flow easy and intuitive for the user?
**User flow** is the path taken by a prototypical user on a website or app to complete a task. The user flow takes them from their entry point through a set of steps towards a successful outcome and final action, such as purchasing a product.

**User flow design:** 

<img src="https://github.com/yanxu2021/ApartmentUs/blob/main/img/UserFlowDesign.png" />

**ApartmentUs User Flow**

![image](https://github.com/yanxu2021/ApartmentUs/blob/main/img/userflow.png)

## :thought_balloon: Protected vs. Unprotected pages?

**A protected page** is a page where normal users are prevented from editing and/or moving at all. 

Almost every web application require some form of authentication to prevent unauthorized users from having access to the inner workings of the applications.

**Set up an authentication route and protect other routes from been accessed by unauthorized users.**
Require authentication for users to access pages to restrict user access to certain pages or have the whole application behind a login.
1. React-router will handle routing, i.e switching from one page to another within the web application. Installed react-router-dom for routing.
2. Protected Routes are routes that can only be accessed if a condition is met(usually, if user is properly authenticated). It returns a Route that either renders a component or redirects a user to another route based on a set condition.

[ Go to Next Step ](https://github.com/yanxu2021/ApartmentUs/blob/main/Challenge%202%20-%20Set%20Up.md)

[ Go Back ](https://github.com/yanxu2021/ApartmentUs/blob/main/README.md)
