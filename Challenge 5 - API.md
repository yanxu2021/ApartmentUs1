# Challenge 5 - API

## 1. Finish off apartment application by hooking up the Database via API endpoints. 

It is time to create/read/update new apartments by users in database! 

1. Implementing fetch to request data from Rails API
2. Setting state with the JSON data that is returned from the fetch request

```
Review: what is fetch in React js?
The most accessible way to fetch data with React is using the Fetch API. 
The Fetch API is a tool that's built into most modern browsers on the window object ( window. fetch ) 
and enables us to make HTTP requests very easily using JavaScript promises.
```

There will be a series of fetch requests to match the functionality required in application. To start, load up all the apartments from the database and save them into state. The React lifecycle method `componentDidMount()` will run as soon as the app loads and handle fetching all the apartments.

Rails use Active Record to post that information to the database.

**Format the request:** send the information in the body of the request, and specify the header to accept JSON, and specify the HTTP method.

The fetch call will return a Promise. If the Promise is resolved successfully then call the `readApartment` method to reload the apartments array that will include the new apartment.

**app/javascript/components/App.js**

```
class App extends Component {
  constructor(props){
    super(props)
    this.state = {
      apartments: []//Start with an empty array
    }
  }
  
  componentDidMount(){
    this.readApartment()
  }
```

**app/javascript/components/App.js**

- `readApartment` Method
```
readApartment = () => {
    fetch("/apartments")
    .then(response => response.json())
    .then(payload => this.setState({apartments: payload}))
    .catch(errors => console.log("index errors:", errors))
}
```

- `creatApartment` Method- Make a **POST** request to a route called **"/apartments"** to create a new apartment.

```
  createApartment = (newApartment) => {
    fetch("/apartments", {
      body: JSON.stringify(newApartment),
      headers: {
        "Content-Type": "application/json"
      },
      method: "POST"
    })
    .then(response => {
      if(response.status === 422){
        alert("There is something wrong with your submission.")
      }
      return response.json()
    })
    .then(() => this.readApartment())
    // The fetch call will return a Promise. 
    // If the Promise is resolved successfully then call the `readApartment` method 
    // to reload the apartments array that will include the new apartment.
    .catch(errors => console.log("create errors:", errors))
  }
```

- `editApartment` Method-Make a **PATCH** request to a route called "/apartments/:id" to update an existing cat.

```  
  editApartment = (apartment, id) => {
    fetch(`/apartments/${id}`, {
      body: JSON.stringify(apartment),
      headers: {
        "Content-Type": "application/json"
      },
      method: "PATCH"
    })
    .then(response => {
      if(response.status === 422){
        alert("There is something wrong with your submission.")
      }
      return response.json()
    })
    .then(() => this.readApartment())
    // The fetch call will return a Promise. 
    // If the Promise is resolved successfully then call the `readApartment` method 
    // to reload the apartments array that will include the updated apartment.
    .catch(errors => console.log("edit errors:", errors))
  }
```
## 2. API Validation

As developers we have to think about what happens when things don't go as we expect. What if data is submitted to our API that isn't complete, or has something else that causes it to be invalid? This could cause harm to our database or affect the user experience.

- Implementing model validations
- Implementing model specs in a Rails application
- Implementing request specs in a Rails application

**app/models/apartment.rb**
```
class Apartment < ApplicationRecord
  belongs_to :user
  validates :street, :city, :state, :manager, :email, :price, :bedrooms, :bathrooms, :pets, :user_id, presence: true
end
```

```
$ rspec spec/models
```

## 3. Testing
For testing with Jest and Enzyme:
```
$ yarn add jest
$ yarn add enzyme (the long command from the syllabus)
```

Add this to your package.json
```
  "jest": {
    "roots": [
      "app/javascript/components"
    ]
  }
````

If have images in app, then need to mock them. In package.json add this to the previous code snippet:

```
  "jest": {
    "roots": [
      "app/javascript/components"
    ],
  "moduleNameMapper": {
      "\\.(jpg|ico|jpeg|png|gif|eot|otf|webp|svg|ttf|woff|woff2|mp4|webm|wav|mp3|m4a|aac|oga)$": 
      "<rootDir>app/javascript/components/fileMock.js",
      "\\.(css|less)$": "<rootDir>app/javascript/components/fileMock.js"
    }
  }
```
## 4. Is everything secure?Protected vs. Unprotected pages?

**A protected page** is a page where normal users are prevented from editing and/or moving at all. 

Almost every web application require some form of authentication to prevent unauthorized users from having access to the inner workings of the applications.

**Set up an authentication route and protect other routes from been accessed by unauthorized users.**
Require authentication for users to access pages to restrict user access to certain pages or have the whole application behind a login.
1. React-router will handle routing, i.e switching from one page to another within the web application. Installed react-router-dom for routing.
2. Protected Routes are routes that can only be accessed if a condition is met(usually, if user is properly authenticated). It returns a Route that either renders a component or redirects a user to another route based on a set condition.

**Login/Logout Button** With login status and routes in React component, add a button to log the user out or in.
**app/javascript/components/components/Header.js**
```
...
    const {
      logged_in,
      new_user_route,
      sign_in_route,
      sign_out_route
    } = this.props
...


        <div className="nav-bar">
          <NavLink to="/" className="nav-link">Home</NavLink>
          {logged_in && <a href={sign_out_route} className="nav-link">Sign Out</a>}
          {!logged_in && <a href={sign_in_route} className="nav-link">Sign In</a>}
          {!logged_in && <a href={new_user_route} className="nav-link">Register</a>}
        </div>
...
```

**app/javascript/components/App.js**
```
...
          {this.props.logged_in &&
            <Route path="/new" render={(props) => {
              return <New createApartment={this.createApartment} current_user={this.props.current_user} />
            }}/>
          }
          
          {this.props.logged_in &&
            <Route path="/myapartments" render={(props) => {
              let apartments = this.state.apartments.filter(a => a.id === this.props.current_user.id)
              return <MyApartment apartments={apartments} />
            }}/>
          }
          
          {this.props.logged_in &&
            <Route path="/edit/:id" render={(props) => {
              let apartment = this.state.apartments.find(apartment => apartment.id === +props.match.params.id)
              return (
                <Edit
                  editApartment={this.editApartment}
                  current_user={this.props.current_user}
                  apartment={apartment}
                />
              )
            }}/> 
          }
...
```

## 5. Git add/commit/push to new branch-api
```
$ git status
$ git checkout -b api
$ git add .
$ git commit -m "complete api"
$ git push origin api
```
Pull request and review or waiting for review, then merge and delete the branch

[ Go Back ](https://github.com/yanxu2021/ApartmentUs/blob/main/README.md)
