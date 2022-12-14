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
