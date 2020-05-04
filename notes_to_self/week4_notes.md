## What Is a REST API

**API** is an application programming interface. 

It is a set of rules that allow programs to talk to each other. 
The developer creates the API on the server and allows the client to talk to it.

**REST** determines how the API looks like. 

It stands for “Representational State Transfer”. 
It is a set of rules that developers follow when they create their API. 
One of these rules states that you should be able to get a piece of data (called a resource) when you link to a specific URL.

### The Anatomy Of A Request

It’s important to know that a request is made up of four things:

* The endpoint
* The method
* The headers
* The data (or body)

### In REST, URLs map onto a *resource*. 

The idea of a *resource* is pretty much the same idea as an object in OOP, 
it's just a **noun** that matches to something in the real world. 

The second idea of REST is that we can use a set of actions that HTTP allow us
to specify when we create a request - verbs like `POST`, `PATCH` and `DELETE`. 

* CREATE - POST /restaurants
* READ - GET /restaurants/123
* UPDATE - PATCH /restaurants/123
* DELETE - DELETE /restaurants/123

Although there's of course much more to REST, understanding that it's all about
***resources*/*nouns*** (like restaurants in this example), and ***verbs***
(POST/GET/PATCH/DELETE) is the main thing you need to understand.

### Routing for a real application

When you want to write a web app, you need a few more routes on top of the basic create, read, update and delete.  You need:

* A route for listing all the records for a certain resource (e.g. all the restaurants).
* A route to show a web form for entering the details of a new record.
* A route to show a web form for entering the new details of an existing record.

Rails has a set of conventions for what URLs to use for these extra things:

```sh
Verb    URI Pattern            Controller#action
------  ---------------------  ------------------
GET     /restaurants           restaurants#index
POST    /restaurants           restaurants#create
GET     /restaurants/new       restaurants#new
GET     /restaurants/:id/edit  restaurants#edit
GET     /restaurants/:id       restaurants#show
PATCH   /restaurants/:id       restaurants#update
PUT     /restaurants/:id       restaurants#update
DELETE  /restaurants/:id       restaurants#destroy
```