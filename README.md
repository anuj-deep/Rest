#REST Architecture

##What is REST

REST is acronym for REpresentational State Transfer. It is an architectural style for providing standards between computer systems on the web, making it easier for systems to communicate with each other. REST-compliant systems, often called RESTful systems, are characterized by how they are stateless and separate the concerns of client and server.  It was first presented by Roy Fielding in 2000 in his famous dissertation.


##Separation of Client and Server

In the REST architectural style, the implementation of the client and the implementation of the server can be done independently without each knowing about the other. This means that the code on the client side can be changed at any time without affecting the operation of the server, and the code on the server side can be changed without affecting the operation of the client.

As long as each side knows what format of messages to send to the other, they can be kept modular and separate. Separating the user interface concerns from the data storage concerns, we improve the flexibility of the interface across platforms and improve scalability by simplifying the server components. Additionally, the separation allows each component the ability to evolve independently.

By using a REST interface, different clients hit the same REST endpoints, perform the same actions, and receive the same responses. 


##Statelessness

Systems that follow the REST paradigm are stateless, meaning that the server does not need to know anything about what state the client is in and vice versa. In this way, both the server and the client can understand any message received, even without seeing previous messages. This constraint of statelessness is enforced through the use of resources, rather than commands. Resources are the nouns of the Web - they describe any object, document, or thing that you may need to store or send to other services.

Because REST systems interact through standard operations on resources, they do not rely on the implementation of interfaces.

These constraints help RESTful applications achieve reliability, quick performance, and scalability, as components that can be managed, updated, and reused without affecting the system as a whole, even during operation of the system.


##Communication between Client and Server

In the REST architecture, clients send requests to retrieve or modify resources, and servers send responses to these requests. Let’s take a look at the standard ways to make requests and send responses.


##Making Requests

REST requires that a client make a request to the server in order to retrieve or modify data on the server. A request generally consists of:

    *an HTTP verb, which defines what kind of operation to perform
    *a header, which allows the client to pass along information about the request
    *a path to a resource
    *an optional message body containing data


##HTTP Verbs

There are 4 basic HTTP verbs we use in requests to interact with resources in a REST system:

    *GET — retrieve a specific resource (by id) or a collection of resources
    *POST — create a new resource
    *PUT — update a specific resource (by id)
    *DELETE — remove a specific resource by id

##Paths

Requests must contain a path to a resource that the operation should be performed on. In RESTful APIs, paths should be designed to help the client know what is going on.

Conventionally, the first part of the path should be the plural form of the resource. This keeps nested paths simple to read and easy to understand.

A path like fashionboutique.com/customers/223/orders/12 is clear in what it points to, even if you’ve never seen this specific path before, because it is hierarchical and descriptive. We can see that we are accessing the order with id 12 for the customer with id 223.


##Examples of Requests and Responses

Let’s say we have an application that allows you to view, create, edit, and delete customers and orders for a small clothing store hosted at fashionboutique.com. We could create an HTTP API that allows a client to perform these functions:

If we wanted to view all customers, the request would look like this:

```
GET http://fashionboutique.com/customers
Accept: application/json
```

A possible response header would look like:
```
Status Code: 200 (OK)
Content-type: application/json
```

followed by the customers data requested in application/json format.

Create a new customer by posting the data:

```
POST http://fashionboutique.com/customers
Body:
{
  “customer”: {
    “name” = “Anuj Deep”,
    “email” = anujdeepktr@gmail.com”
  }
}
```

The server then generates an id for that object and returns it back to the client, with a header like:

```
201 (CREATED)
Content-type: application/json
```

To view a single customer we GET it by specifying that customer’s id:

```
GET http://fashionboutique.com/customers/123
Accept: application/json
```

A possible response header would look like:

```
Status Code: 200 (OK)
Content-type: application/json
```

followed by the data for the customer resource with id 23 in application/json format.

We can update that customer by PUT ting the new data:

```
PUT http://fashionboutique.com/customers/123
Body:
{
  “customer”: {
    “name” = “Anuj Deep”,
    “email” = “anujdeepktr@gmail.com”
  }
}
```

A possible response header would have Status Code: 200 (OK), to notify the client that the item with id 123 has been modified.

We can also DELETE that customer by specifying its id:

```
DELETE http://fashionboutique.com/customers/123
```

The response would have a header containing Status Code: 204 (NO CONTENT), notifying the client that the item with id 123 has been deleted, and nothing in the body.
