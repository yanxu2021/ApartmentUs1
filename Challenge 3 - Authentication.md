# Challenge 3 - Authentication
A key component of web applications is the ability for a user to log in. This requires using the Devise gem to create authentication and authorization for a Rails application.
- Add RSpec
```
$ bundle add rspec-rails
$ rails generate rspec:install
```
- Add Devise
```
$ bundle add devise
$ rails generate devise:install
$ rails generate devise User
$ rails db:migrate
```
- Add mailer settings

Here need to set up the default URL options for the Devise mailer in each environment. 

**config/environments/development.rb** , add the following code at the end of the previous code inside the file:
```
config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }
```

Devise is a Rails gem that gives developers a collection of methods that create authorization and authentication. Using Devise to create a special model called User that gets Devise code injected into each new model instance. Just by running the setup commands to get Devise *sign in* and *sign up* forms as well as a lot of additional functionality.

Navigate to `http://localhost:3000/users/sign_in` and see a log in page.

Navigate to `http://localhost:3000/users/sign_up` and see a sign up page.

- Apartment Resource

The Devise User model is going to have an association with the Apartment model. In this situation, the User will have many apartments and the Apartments will belong to a User.
```
$ rails g resource Apartment street:string city:string state:string manager:string email:string 
price:string bedrooms:integer bathrooms:integer pets:string user_id:integer
$ rails db:migrate
```

- User and Apartment Associations

The Apartments will belong to a User and a User will have many apartments.

**app/models/apartment.rb**
```ruby
class Apartment < ApplicationRecord
  belongs_to :user
end
```

**app/models/user.rb**
```ruby
class User < ApplicationRecord
  # Include default devise modules. Others available are:
  # :confirmable, :lockable, :timeoutable, :trackable and :omniauthable
  devise :database_authenticatable, :registerable,
         :recoverable, :rememberable, :validatable
  has_many :apartments
end
```

- Devise Code

Devise gets added to a few different spots. 

1. The User model, which we already looked at. 
2. The controller. This code is predominantly /prɪˈdɑːmɪnəntli/adv. 主要地；显著地  behind the scenes. 
3. The routes. We can see that we have a resource for apartments and Devise routes for users.

**config/routes.rb**
```ruby
Rails.application.routes.draw do
  resources :apartments
  devise_for :users
end
```

- Git add/commit/push to new branch-setup
```
$ git status
$ git checkout -b authentication
$ git add .
$ git commit -m "complete authentication"
$ git push origin authentication
```
- Pull request and review or waiting for review, then merge and delete the branch
<hr>
