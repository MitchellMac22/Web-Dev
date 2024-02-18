# Final website for CS401

Name: Mitchell Peterson
email: mitchellpeterson304@u.boisestate.edu

## How to run this website

- npm install
- node ./bin/www

Browse to localhost:3000

## Bugs

There appears to be a refresh issue when changing routes on Safari. Perhaps I have an out of date version, but this has been a reported bug of Node.js.  
When launching using `node ./bin/www` I appear to get the following warning: Invalid 'main' field in '/Users/mac/Documents/GitHub/spring22-final-project-MitchellMac525/node_modules/string-sanitizer/package.json' of 'node.js'.

## Features

Review all the features of your app here and note anything that is missing or
not implemented.

I have implemented a SQlite3 database to hold all blog posts.
I have implemented the functionaility to Create, Edit, Delete, and View all blog posts. 
I have constructed a nice top navigation that allows users to change from one .pug depending on what they would like to do.
I have also added my own little stylistic touches to the website, including a funny gif.
I have implemented a level of sanitization that only accepts spaces and numbers.
**********************************************************************************

## Lab Walk through

- [Video](https://youtu.be/225U5tRswEw)

## Task 0 - Install Nodejs

Before we even start working on our lab we need to install NodeJS. The NodeJS project has created
installers for all major operating systems so all you need to do is download the correct installer
and install as normal. NOTE: You should install the **64bit version** of node NOT the 32 bit
version. 

- Install Node - [https://nodejs.org/en/download/](https://nodejs.org/en/download/)


## Task 1 - Basic routing

In web development routing refers to how an application responds to a client request to a particular
endpoint, which is a URI (or path) and a specific HTTP request method (GET, POST, and so on).
Application routing can get extremely complex on large apps so it is important to know the
fundamentals. Each route can have one or more handler functions, which are executed when the route
is matched.

Route definition takes the following structure:

```javascript
app.METHOD(PATH, HANDLER)
```

Where:

- app is an instance of express.
- METHOD is an HTTP request method, in lowercase.
- PATH is a path on the server.
- HANDLER is the function executed when the route is matched.


Lets create a simple homepage that displays a form that we can send requests to. The root page of
our app will display a form that will send a `POST` request to the URI `/addblog`. First, lets
update the default template in the file `routes/index.js` to the following:


```javascript
const express = require('express');
const router = express.Router();
const path = require('path');
const fs = require('fs');

/* GET home page. */
router.get('/', function(req, res, next) {
  res.render('index', { title: 'My Cool Website' });
});

/* POST to add a new blog update */
router.post('/addblog', function(req, res, next) {
  const blogtitle = req.body.blogtitle;
  const blogtext = req.body.blogtext;
  const directoryPath = path.join(appRoot, 'posts', blogtitle);
  fs.writeFileSync(directoryPath,blogtext);
  res.redirect('/blog');
});

/* GET list of all blogs */
router.get('/blog', function(req,res,next){
  const directoryPath = path.join(appRoot, 'posts');
  fs.readdir(directoryPath, function (err, files) {
    if (err) {
        return console.log('Unable to access directory: ' + err);
    }
    var posts = [ ];

    files.forEach(function (file) {
      posts.push({title: file});
    });
    res.render('blog', {title: "All blog posts", allposts: posts});
  });
  
}); 

module.exports = router;
```

In your **app.js** file you will need to add the following line:

```javascript
global.appRoot = path.resolve(__dirname);
```

This allows your code to save and load posts from a directory called **posts**.

## Task 2 - Update index

Now that we have our basic routing set we need to update our **index.pug** template to add in a
form. One quick way to write **pug** is to write it in HTML and then convert it to **pug**. In
fact there is even a [cool site](https://html2jade.org/) that will do it for us!

Finally we want to make the homepage fancy! You need to find a fun picture that is safe for work and
display it on the homepage. Make sure and add image in the `/public/images` folder in your express
site and then modify the homepage **index.pug** to display it. You then need to update the style
sheet in `/public/stylesheets` and add in **2 new CSS rules**. They rules can be whatever you want
to make your webpage look fancy!

Here is an example index.pug to get you started

```pug
extends layout

block content
  h1= title
  p Welcome to #{title}
  form(method="POST", action="/addblog")
      label(for = "blogtitle") Title:
      input(type = "text", id="blogtitle" ,name = "blogtitle")
      br
      textarea(name="blogtext", cols="30", rows="10") 
      br
      input(type = "submit", name = "submit", value = "submit")
```

## Task 3 - Create new View

In our post request we simple take the post data and write it out to a file. As of now there is no
way to see what posts we have. So now we need to create the file **blog.pug** and then display all
the posts that we have saved!

Create a new file named *blog.pug** and put it in the views folder.

```pug
extends layout

block content
  h1= title
  ul
  each val in allposts
    li= val.title
```

## Task 4 - Test your site

We now have a very simple site that accepts data and displays data! However, our site is not very
robust as we don't do hardly any error handling. For example what happens if you try to use an
illegal character to save the file? You might want to check the [reserved characters and
words](https://en.wikipedia.org/wiki/Filename#Reserved_characters_and_words) list and make sure
that you are using a valid file name!

## Task 5 - Add Features

Add the rest of the requried features to your site.


## Sources Used
Bruce Alighty Gif: https://gfycat.com/gifs/search/bruce+almighty+funny+coffee+typing+prayers+essay   
W3Schools How to Build a Navbar: https://www.w3schools.com/howto/howto_js_topnav.asp   
Establish a SQlite Connection in Node.js: https://stackoverflow.com/questions/50411135/i-am-sending-a-sqlite3-query-result-through-node-js-to-the-browser-as-json  
