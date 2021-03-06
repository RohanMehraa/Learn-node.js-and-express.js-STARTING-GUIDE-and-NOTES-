# Learn-node.js-and-express.js-STARTING-GUIDE-and-NOTES-
These are the notes I made while learning Node.js - Express.js and APIs: 

[Please note that the repository consists of the folders for node.js and express.js starting files, which can be refered with the notes.]

- Command to make a folder:
mkdir my-express-server

- Command to go into created folder:
cd my-express-server

- Command to create a new file
touch server.js

- Command to initialise npm
npm init

Then it'll ask for the following info to create a json file---
package name: (my-express-server)
version: (1.0.0)
description: 
entry point: 
author:
git repository:
keywords:
license: (ISC)

and it'll create a package.json file with the following content:
{
  "name": "my-express-server",
  "version": "1.0.0",
  "description": "My first express server.",
  "main": "server.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node server.js"
  },
  "author": "Rohan Mehra",
  "license": "ISC",
  "dependencies": {
    "express": "^4.17.1"
  }
}



- Command to install express:
npm install express

after installing express it will add express to the dependencies in the package.json



----------------------------------------------------------------------------------------------------

const express = require("express");
//To use express in our code, we have to add it by using require();
//const is used as the value is never going to change.


cont app = express();
// it is a good practice to use the name app for our const variable as it is a common practice among the devs.
// express(); is a function which refers to the express module.


app.listen(3000, function () {
    console.log("Server started on port 3000.");
});

//listen() is a function which tells to listen on a specific port for any HTTP request that get sent to our server.
// listen(3000); 3000 is the port no.
// listen(3000, function () {                           //here function() is the callback function.
    console.log("Server started on port 3000.");
});



app.get("/", function(request, response){

});

//get() is a method provided by express  that allows us to specify what should happen when a browser gets in touch with our server or make a GET request.  

get("/", function(request, response){

});

first parameter takes the location of the get request. i.e what should happen when someone makes a GET request to the HOME ("/")
Then, the callback function tells the server what to do in that case.


app.get("/", function(request, response){
    console.log(request);
    response.send("<h1> HELLO WORLD! </h1>");
});

by console.log(request);
// we can see what request the browser has made to the server.

by response.send("....");
//we can send response to the browser with send method.

response.sendFile(__dirname + "/index.html");
sendFile is used to send a particular file or webpage doc.
here __dirname is a constant which returns the exact file path of the current file in which __dirname is called, where ever we've hosted the server.




----------------------------------------------------------------------------------------------------

APIs:

npm install request
//request is a module through which we can use make a request to an external api.

const request = require("request");

app.post("/", function(req, res) {
    request("https://apiv2.bitcoinaverage.com/indices/global/ticker/BTCUSD", function(error, response, body) {
        console.log(body);
    });
});


// request("https://apiv2.bitcoinaverage.com/indices/global/ticker/BTCUSD", function(error, response, body) {
        console.log(body);
    });

is a function with request module, it takes 1st parameter as the cURL of the external api, and 2nd parameter as a callback function with arguments as: error, response, body.
here the body returns an JSON format.

a javascript object can be converted into a JSON format using the following function:

JSON.stringify(objectName);

viceversa, a JSON type can be converted into a javascript object using the following function:

JSON.parse(variableContainingJsonFlatPack);
eg. body in this case.


res.send("<h1> HELLO </h1>");

send is the last function to be included in the post function. As it sends and exits the post function.

if we'd need to need to use multiple line send statements, then it is not possible. But we can use the write() function.

the write() function creates a buffer and we can add all of the things we need to send using this buffer and finally call the send() method to send all the items in the buffer.

eg:
res.write("<h1> hello </h1>");
res.write("<h2> world! </h2>");
res.send();


npm install body-parser
//command to install body parser module.

const bodyParser = require("body-parser");
app.use(bodyParser.urlencoded({extended: true}));
// this is how we can require bodyParser in our code and use it.
// by using body parser we can have access to the html body elements such as form data. The form data can be recognised by it's name. for eg:
<input name="firstName" id="" class="btn btn-primary" type="text" value="">
we can use it in our js code using:
req.body.firstName; inside the post function. Please note that the form should have a method of POST type and action should be the same as we defined in the post function in our js code.
