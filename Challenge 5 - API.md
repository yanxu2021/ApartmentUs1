# Challenge 5 - API

Finish off apartment application by hooking up the Database via API endpoints. It is time to create/read/update new apartments by users in database! Also need to think about: is everything secure?

1. Implementing fetch to request data from Rails API
2. Setting state with the JSON data that is returned from the fetch request

```
What is fetch in React js?
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




[ Go Back ](https://github.com/yanxu2021/ApartmentUs/blob/main/README.md)
