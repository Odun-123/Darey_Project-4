# MEAN STACK DEPLOYMENT TO UBUNTU IN AWS

#Step 1: Creating an AWS instance & Connecting to it using Windows Terminal

Created an Amazon account and provisioned an Ubuntu Server 22.04 LTS (HVM), SSD Volume Type EC2 Instance with a free tier option.

Step 2: Install NodeJs

I updated ubuntu with the command sudo update and upgrade with sudo apt upgrade

Then i now ran 

sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates

curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -

Then I now ran the code below to install nodejs

' sudo apt install -y nodejs'

#Step 3: Install MongoDB

Before install MongoDB, we must run the following commands

sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6

echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list

we will now install mongodb with sudo apt install -y mongodb and then start the server with sudo service mongodb start

Install npm – Node package manager by running the code below:

'sudo apt install -y npm'

Install body-parser package by running the code below. We need ‘body-parser’ package to help us process JSON files passed in requests to the server. 'sudo npm install body-parser'

Create a folder named ‘Books’

'mkdir Books && cd Books'

In the Books directory, Initialize npm project 'npm init'

Add a file to it named server.js by running the code below

'vi server.js'

Copy and paste the web server code below into the server.js file.
'var express = require('express'); var bodyParser = require('body-parser'); var app = express(); app.use(express.static(__dirname + '/public')); app.use(bodyParser.json()); require('./apps/routes')(app); app.set('port', 3300); app.listen(app.get('port'), function() { console.log('Server up: http://localhost:' + app.get('port')); });'

#Step 4:INSTALL EXPRESS AND SET UP ROUTES TO THE SERVER

We also will use Mongoose package which provides a straight-forward, schema-based solution to model your application data. We will use Mongoose to establish a schema for the database to store data of our book register.

'sudo npm install express mongoose'

In ‘Books’ folder, create a folder named apps

'mkdir apps && cd apps'

Create a file named routes.js

'vi routes.js'

Copy and paste the code below into routes.js

var Book = require('./models/book'); module.exports = function(app) { app.get('/book', function(req, res) { Book.find({}, function(err, result) { if ( err ) throw err; res.json(result); }); }); app.post('/book', function(req, res) { var book = new Book( { name:req.body.name, isbn:req.body.isbn, author:req.body.author, pages:req.body.pages }); book.save(function(err, result) { if ( err ) throw err; res.json( { message:"Successfully added book", book:result }); }); }); app.delete("/book/:isbn", function(req, res) { Book.findOneAndRemove(req.query, function(err, result) { if ( err ) throw err; res.json( { message: "Successfully deleted the book", book: result }); }); }); var path = require('path'); app.get('*', function(req, res) { res.sendfile(path.join(__dirname + '/public', 'index.html')); }); };

In the ‘apps’ folder, create a folder named models

'mkdir models && cd models'

Create a file named book.js

vi book.js

Copy and paste the code below into ‘book.js’

'var mongoose = require('mongoose'); var dbHost = 'mongodb://localhost:27017/test'; mongoose.connect(dbHost); mongoose.connection; mongoose.set('debug', true); var bookSchema = mongoose.Schema( { name: String, isbn: {type: String, index: true}, author: String, pages: Number }); var Book = mongoose.model('Book', bookSchema); module.exports = mongoose.model('Book', bookSchema);'
Access the routes with AngularJS by navigating back to the books directory

'cd ../..'

Create a folder named public 'mkdir public && cd public'

Add a file named script.js 'vi script.js'

Copy and paste the Code below (controller configuration defined) into the script.js file.

var app = angular.module('myApp', []); app.controller('myCtrl', function($scope, $http) { $http( { method: 'GET', url: '/book' }).then(function successCallback(response) { $scope.books = response.data; }, function errorCallback(response) { console.log('Error: ' + response); }); $scope.del_book = function(book) { $http( { method: 'DELETE', url: '/book/:isbn', params: {'isbn': book.isbn} }).then(function successCallback(response) { console.log(response); }, function errorCallback(response) { console.log('Error: ' + response); }); }; $scope.add_book = function() { var body = '{ "name": "' + $scope.Name + '", "isbn": "' + $scope.Isbn + '", "author": "' + $scope.Author + '", "pages": "' + $scope.Pages + '" }'; $http({ method: 'POST', url: '/book', data: body }).then(function successCallback(response) { console.log(response); }, function errorCallback(response) { console.log('Error: ' + response); }); }; });

In public folder, create a file named index.html; 'vi index.html'

Copy and paste the code below into index.html file.

<!doctype html>

<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script> <script src="script.js"></script>
Name:

Isbn:	

Author:	

Pages:	

Add

    </tr>
    <tr ng-repeat="book in books">
      <td>{{book.name}}</td>
      <td>{{book.isbn}}</td>
      <td>{{book.author}}</td>
      <td>{{book.pages}}</td>

      <td><input type="button" value="Delete" data-ng-click="del_book(book)"></td>
    </tr>
  </table>
</div>

Change the directory back to Books with command cd ..

and then start the server node server.js

![node js](https://user-images.githubusercontent.com/117018714/207733325-d678e978-dc8a-4edf-9b84-d653f91524f3.png)

The server is now up and running, we can connect it via port 3300

Run curl -s http://169.254.169.254/latest/meta-data/public-ipv4 for Public IP address or curl -s http://169.254.169.254/latest/meta-data/public-hostname for Public DNS name.


