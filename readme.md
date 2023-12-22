# Instructions

1. Open a new terminal and run the following commands
```
go get .
go build
```
2. To run the store, in the terminal type
```
go run .
```

# About Go Get
go get installs any dependencies, the program has. Dependencies are external code packages used by the program to build more complex software. One package we are using is [gin](https://github.com/gin-gonic/gin).

# Task 1

You have three endpoints 
- / (the root)
- /products
- /products/:id

the /products endpoint accepts GET and POST requests
the /products/:id accepts a GET request where the :id element is replaced by a number relating to a product, eg /products/1

# Video - HTTP Methods / Verbs
Hang on, what do you mean GET and POST? Why are they in capitals? What are they?

Essentially they are how the internet works - sending requests for information, or requests with information.

Here's a short [video](https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/HTTP-methods) that explains in more depth.

## Step 1
Install Thunder Client from the extensions on the left in VS Code. Thunder Client is a Rest API Client extension for VS Code that allows you to issue GET, POST, PUT, and other HTTP requests. We are going to use it to test our store.

## Step 2
With the store running, open Thunder Client :

![Open Thunder Client](/images/thunderclient.png "Open")

Click the New Request button, and fill in the details as below and click Send:

![Send request to hearbeat](/images/sendGet.png "Send")

Congratulations! You have now sent an HTTP GET request to your webserver running on your computer!

## Task 2
Now, create a new GET request to the /products endpoint to ensure the list of products are returned.

## Task 3
Now, create a GET request to the /products/:id endpoint, replacing ```:id``` with a number from 1-4.
### Question
What happens when you send a GET request for a number bigger than 4 or smaller than 1? What happens when you send a request where you replace :id with text, such as ```hello```?

## Task 4
Open a browser and navigate to the address ```http://127.0.0.1```

That's right, your browser sends GET requests, just like Thunder Client does.

## Task 5
However, your browser *cannot* send POST requests. In order to add a new product, we need to send JSON to the /products endpoint.

What is JSON? There's detailed explanation [here](https://www.w3schools.com/js/js_json_intro.asp), but it's a data structure in key-value pairs. In the JSON below, the first part is the 'key' (for example "name"), and the second part after the colon if the 'value' (so for the key "name", the value is "My New Product").

```
{
    "name": "My New Product",
    "Description": "It's my new product!", 
    "longdescription":"It's a longer description of my new product!",
    "image": "",
    "price": 49.99
}
```

This JSON is a representation of the [struct](https://dev.to/avinashtechlvr/understanding-structs-in-go-a-comprehensive-guide-for-beginners-1aki) in the items/items.go file:

![Products struct](/images/productStruct.PNG "Products")

You'll notice that our struct has a JSON mapping like `json:"id"` - this is important in Go and allows us to deserialize a JSON object to a struct, and also serialize a struct *to* JSON, which is what gin is doing for us when it returns the list of products.

You'll also notice we don't send the ```id``` attribute. Mostly when POSTing to and endpoint to create or insert a new object, the 'back end' is responsible for the *indexing* or unique numbering of objects, most normally in a database. At the moment we are not using a database, but we will in the future.

Create a new POST request in Thunder Client, adding the JSON above to the Body tab:

![Post part 1](/images/postpart1.PNG "Post 1")

When you click Send, you will see the record you just added, with a new ID.

Now if you go back to your GET request for /prodcuts endpoint, you will see it has been added to the list of products!

Have a play around changing the name, description and so on and checking that they are added to the products list.





