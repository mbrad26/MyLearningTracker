## What Is a REST API

**API** is an application programming interface. 

It is a set of rules that allow programs to talk to each other. 
The developer creates the API on the server and allows the client to talk to it.

**REST** determines how the API looks like. 

It stands for “Representational State Transfer”. 
It is a set of rules that developers follow when they create their API. 
One of these rules states that you should be able to get a piece of data (called a resource) when you link to a specific URL.

### **The Anatomy Of A Request**

It’s important to know that a request is made up of four things:

* The **endpoint**
* The **method**
* The **headers**
* The **data (or body)**

#### **The endpoint** (or route) is the url you request for. 

It follows this structure:
```
root-endpoint/?
```

The **root-endpoint** is the starting point of the API you’re requesting from. The root-endpoint of Github’s API is ```https://api.github.com``` while the root-endpoint Twitter’s API is ```https://api.twitter.com.```

The **path** determines the resource you’re requesting for. 

To understand what paths are available to you, you need to look through the API documentation. For example, let’s say you want to get a list of repositories by a certain user through Github’s API. The docs tells you to use the the following path to do so:

```/users/:username/repos```

Any colons **(:)** on a path denotes a *variable*. You should replace these values with actual values of when you send your request. In this case, you should replace :username with the actual username of the user you’re searching for.

The endpoint to get a list of my repos on Github is this:

```https://api.github.com/users/mbrad26/repos```

The final part of an endpoint is **query parameters**. Technically, query parameters are not part of the REST architecture, but you’ll see lots of APIs use them. 

**Query parameters** give you the option to modify your request with key-value pairs. They always begin with a question mark **(?)**. Each parameter pair is then separated with an ampersand **(&)**, like this:

```?query1=value1&query2=value2```

#### **The method** is the type of request you send to the server. 

`GET`	is used to get a resource from a server. If you perform a `GET` request, the server looks for the data you requested and sends it back to you. In other words, a `GET` request performs a `READ` operation. This is the default request method.

`POST` is used to create a new resource on a server. If you perform a `POST` request, the server creates a new entry in the database and tells you whether the creation is successful. In other words, a `POST` request performs an `CREATE` operation.

`PUT` and `PATCH`	are used to update a resource on a server. If you perform a `PUT` or `PATCH` request, the server updates an entry in the database and tells you whether the update is successful. In other words, a `PUT` or `PATCH` request performs an `UPDATE` operation.

`DELETE` is used to delete a resource from a server. If you perform a `DELETE` request, the server deletes an entry in the database and tells you whether the deletion is successful. In other words, a `DELETE` request performs a `DELETE` operation.

#### The Headers

Headers are used to provide information to both the client and server. 
It can be used for many purposes, such as authentication and providing information about the body content. 

You can find a list of valid headers on MDN’s HTTP Headers Reference.
HTTP Headers are property-value pairs that are separated by a colon. The example below shows a header that tells the server to expect JSON content.

```"Content-Type: application/json". Missing the opening ".```

#### The Data (Or “Body”)

The data (sometimes called “body” or “message”) contains information you want to be sent to the server. This option is only used with `POST`, `PUT`, `PATCH` or `DELETE` requests.

## HTTP Status Codes And Error Messages

**200+** means the request has succeeded

**300+** means the request is redirected to another URL

**400+** means an error that originates from the client has occurred

**500+** means an error that originates from the server has occurred


### **In REST, URLs map onto a *resource*.**

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

### **Routing for a real application**

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