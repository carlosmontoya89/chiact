# chiact

***WARNING: Much Refactoring Underway***

Up Next: 
1. add Redux to manage application state
2. Add user account view page and edit functionality
3. Add a meetings model and CRUD routes on the server to create a list of meetings (blogs are so overdone)
4. Incorporate the meetings into the client app

## Overview 

The goal of this project is to create a boilerplate for developing full-stack web applications using [Golang](https://golang.org) (Go) on the server side and [React](https://facebook.github.io/react/) on the client side.

chiact includes:
* Server side routing with [Chi](https://github.com/pressly/chi)
* Database connection
* Static directory serving
* API structure and starter methods
* Authentication and JWT
* User Storage and editing
* Server-side Rendering of React Pages as unregistered visitor for public routes

## Please Note
The server-side rendering relies on [PhantomJS](http://phantomjs.org/) which must be installed and in the PATH on the machine where this will run. If you don't want this feature, simply remove helpers/prerender.go and remove r.Use(helpers.PrerenderMiddleWare) in main.go

### Instructions
1. Make sure you have Go, NPM, PhantomJS, and Mongo installed and accessible in PATH
2. cd $GOHOME/src/github.com/your-github-username
3. Clone Repo - git clone https://github.com/tutley/chiact myprojectname
4. Search and replace in the directory for tutley/chiact, replace with your-github-username/myprojectname
      1. (you will need to edit the name chiact in other places for display purposes)
5. glide install
6. npm install
7. npm start
8. http://localhost:3333/ - Create an account and login to test that it's working

To build for production: npm run production

### Go Structure
The server side, written with Go, uses glide for vendoring (dependency management) and can be run locally with "go run main.go". The glide.yaml file holds the dependencies, which can be installed with 'glide install'.

* The handlers directory contains the various local packages for handling routes.
* The helpers directory contains packages with functions to assist along the way.
* The models directory contains data models with methods included.
* The vendor directory contains the local copies of dependencies.

We have included mgo for storing data in MongoDB but if you prefer another database that could be changed by editing the models as well as the db init in main and helpers.

#### Server-Side Rendering
I created a middleware for this project (prerender) that uses PhantomJS and MongoDB to create and save a string representation of an entire rendered-page. Based on some logic in the middleware, the Go application will either serve the entire page from the string (stored in the database), or pass through and serve the react app and let react router figure out what to do. The static assets and the API routes are excluded from this. The prerender middleware checks the database to see if the page is already there, and if not it kicks off a goroutine to have PhantomJS create the string so the page can be stored. This also happens if the page is older than 1 hour. 

### React Structure
The client application is written in React, which requires a few files in the main directory for development purposes. The files that will be served for the client are in the client directory. The development is done on the files in the client/src directory, then webpack builds the final version.

These files are used with React:
* package.json - contains dependency configurations (use npm install to set it up)
* node_modules - this directory will be created by npm install to hold local dependencies
* webpack.config.js - this file is used to setup the dev environment for react
* client/js ; client/img ; client/css - these static directories serve assets
* client/src - react development directory
* client/index.html - this is generated by webpack when you build the client
* client/index_bundle.js - this is generated by webpack when you build the client

## Wishlist
* A simple meeting planning system
* Navigation Bar

