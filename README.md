# Authentication-DatabseEncryption
using Encryption and dotenv modules to encrypt our data

## Description:
A very simple login/registration page which exncypts the password by the help of 'encryption' npm package. In this project, Encironment Variables have been used to keep Secrets safe.

## Technology used in the project
Database: Mongodb  
programming language: Node Js  

## Server Staring code
```
require('dotenv').config();
const express = require("express");
const bodyParser = require("body-parser");
const ejs = require("ejs");
const mongoose = require("mongoose");
const encrypt = require("mongoose-encryption");

const app = express();

app.set('view engine', 'ejs');

app.use(bodyParser.urlencoded({
    extended: true
}));
app.use(express.static("public"));

//create a database
mongoose.connect('mongodb://localhost:27017/userDB',{ useNewUrlParser: true, useUnifiedTopology: true  });
const userSchema = new mongoose.Schema({
    email: String,
    password: String
});

userSchema.plugin(encrypt, {secret: process.env.SECRET, encryptedFields: ['password']});
const User = mongoose.model('User', userSchema);

//TODO

app.listen(3000, function() {
    console.log("Server started on port 3000");
});

```

