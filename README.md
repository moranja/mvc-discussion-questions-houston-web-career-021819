# MVC, Routes and params discussion questions
Take 30 minutes to discuss the following questions with your table group.

## MVC
* What is the MVC Pattern?
  -Model View Controller
* What are the distinct responsibilities of the Model, View and Controller?
  -See below
* What advantages and trade-offs do you see in the MVC pattern?
  -Basic, but regimented
* Who within the MVC pattern is responsible for:
  - knowing how to create database records?
    -Model
  - Provide a visual representation of the data that can be sent to the user?
    -View
  - Connect the business logic with the visual representation?
    -Controller
* What do you find confusing about the MVC pattern?

## Routing
* Map the CRUD actions to the appropriate Sinatra route to the appropriate view, if any. What kind of HTTP request is sent for each CRUD action (`GET`, `POST`, etc)
  C POST
  R GET
  U PATCH/PUT
  D DELETE

* Let's say you have build a Sinatra app that is a news platform. You have an Article and an Author model and you have controllers and routes for the CRUD actions of each model. You sit down at your computer and visit www.youramazingsinatranews.com/articles:
  - What kind of web request is this making? (i.e. is it a `GET`, `POST`, etc request?)
    -A GET request for all articles
  - What controller action (i.e. which route in which controller) will recieve that web request?
    get '/articles' do
    erb :show
    end
  - What is the response that your Sinatra app will send back to the client, i.e. the browser?
    -200, a list of all articles
* You have the following form for a new article:

```html
<form action="?" method="?">

  <label>Title</label>
  <input type="text" name="article[title]">

  <label>Author</label>
  <input type="text" name="article[author]">

  <label>Content</label>
  <input type="text" name="article[content]">

  <input type="submit">

</form>
```

  - What action and what method should the form be defined to have?
    -Action should be "POST", method should be the controller route
  - Given the correct action and method, what controller action will this form submit the form data to?
    -Could be a create or update, post '/article/:id/new', put '/article/:id'
  - Draw out the params that would be created by submitting this form?
    -params = {:article => {:title => ?, :author => ?, :content => ?}}
  - Bonus: Currently, the form is structured such that the author field is a simple text field, and the user will have to input the name of an existing author. Can you change the form so that it offers a drop down menu of all of the existing authors from the database? What would the resulting params look like? How would you use these params to make a new article and associate it to the selected author?
    <li class='dropdown'>
      <%= link_to '#', class: 'dropdown-toggle', data: { toggle: 'dropdown'} do %>
        <%= article.author %>
        <b class="caret"></b>
      <% end %>
      ???

* Spend a few minutes mapping out a domain model for a parking lot. How would you model the relationship between cars and spaces? How would you keep track of how long a car had been parked in a space? How would you keep track of how much money someone would need to pay for having parked a certain amount of time?
      Cars  -<  ParkingLot   >-   Spaces, some method in the ParkingLot model, if you know how long they were in the space, charge them for that time.


* Discuss the REST-ful routes of a Sinatra app. For which routes would you `render` a view and for which would you `redirect to` another route? Why?
  -index, new, create, show, edit, update, delete. Render a view for index, show, new, edit. Redirect for create, update, delete

## params
* Where does the params hash come from?
  -Sinatra
* What utility does the params hash provide?
  -Translates the part of the path we can use into something workable
* Given the two Sinatra scenarios below how would the params hash look like (What keys will the hash contain)?
  - Scenario 1: Sinatra route (get '/books/:name') and URL (/books/Just-for-Fun-The-Story-of-an-Accidental-Revolutionary)
    -params = {:name => Just-for-Fun-The-Story-of-an-Accidental-Revolutionary}
  - Scenario 2: Sinatra route (get '/search/') and URL (/search?article=Just-for-Fun-The-Story-of-an-Accidental-Revolutionary&author=Adam)
    -params = {:article => Just-for-Fun-The-Story-of-an-Accidental-Revolutionary, :author => Adam}
