# Challenge 5 - API

Finish off apartment application by hooking up the Database via API endpoints. It is time to create new apartments by users in database! Also need to think about: is everything secure?

Rails use Active Record to post that information to the database. 

We already have a method that logs the form data for our new apartment, so we can convert that method into a post request. We are making a request to the post route of our Rails app. Remembering RESTful routes, we know that we need to make a **POST** request to a route called "/apartments" to create a new cat.

Format the request: send the information in the body of the request, and specify the header to accept JSON, and specify the HTTP method.

The fetch call will return a Promise. If the Promise is resolved successfully then call the `readApartment` method to reload the apartments array that will include the new apartment.

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

- `creatApartment` Method

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
    .catch(errors => console.log("create errors:", errors))
  }
```

- `editApartment` Method

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
    .catch(errors => console.log("edit errors:", errors))
  }
```




[ Go Back ](https://github.com/yanxu2021/ApartmentUs/blob/main/README.md)
