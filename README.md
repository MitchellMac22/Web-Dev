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
