# Command Line

* ```ls``` shows all of the contents of the current folder we're inside of
* ```ls dirname``` to see the contents of specific folder
* ```cd``` is used to change directories
* ```cd ..``` to go back one level
* you can start writing the name of a directory and hit ```tab``` to autocomplete it
* ```touch orange.txt``` touch is used to create new files
* ```mkdir FavColors``` mkdir is used to create a new folder
* ```rm orange.txtrm``` rm is used to delete a specific file
* ```rm -rf colors/``` rm -rf allows us to remove entire directories
* ```rm -rf /``` deletes everything!
* ```-rf``` is a flag, a way to change what the command does. it stands for 'recursive force'
------------------------------------------------------------------------------------------------------------
# FOR INSTALLING EXPRESS IN NODE:
>In the Gitbash of the project folder write(IN NODE):
```
$ npm init -y
$ npm i express
```
>In app.js:
```
const express = require('express');
const app = express();
```
```
app.get/post/put/delete('/campgrounds', async (req, res) => {
    const camps = await Campground.find({});
    res.render('campgrounds/index', { camps })
})
```
```
app.listen(3000, () => {
    console.log('Serving on port 3000');
})
```
------------------------------------------------------------------------------------------------------------
# FOR INSTALLING EJS IN NODE:
>In the Gitbash of the project folder write(IN NODE):
```
$ npm i ejs
```
>In app.js:
```
app.set('view engine', 'ejs');
app.set('views', path.join(__dirname, 'views'));

(We Need "const path = require('path');" for path.join to work)
```
------------------------------------------------------------------------------------------------------------
# FOR INSTALLING MONGOOSE IN NODE:
>In the Gitbash of the project folder write(IN NODE):
```
$ npm i mongoose
```
>In app.js:
```
const mongoose = require('mongoose');
```
```
mongoose.connect('mongodb://localhost:27017/yelp-camp');
```
```
const db = mongoose.connection;
db.on('error', console.error.bind(console, 'connection error:'))
db.once('open', () => {
    console.log('Database connected')
})
```
------------------------------------------------------------------------------------------------------------
# FOR CREATING SCHEMA AND MODEL:
```
const mongoose = require('mongoose');
```
```
const CampgroundSchema = new mongoose.Schema({
    title: String,
    price: String,
});
```
```
const Campground = mongoose.model('Campground', CampgroundSchema)
```
```
const camp = new Campground({
    title: Malnad,
    price: 250$,
});
```
------------------------------------------------------------------------------------------------------------

# FOR INSTALLING METHOD OVERRIDE IN NODE:
>In the Gitbash of the project folder write(IN NODE):
```
$ npm install method-override
```
>In app.js:
```
const methodOverride = require('method-override');
```
```
app.use(methodOverride('_method'))
```
>In show.js(We can use PUT other than POST and GET by Method Overrideing):
```
<body>
    <form action="/campgrounds/<%=camps._id%>?_method=PUT" method="POST">
    </form>
</body>
```
------------------------------------------------------------------------------------------------------------
# FOR INSTALLING EJS-MATE ON NODE:
>In Node:
```
$ npm i ejs-mate
```
>In App.js:
```
const ejsMate = require('ejs-mate');
```
```
app.engine('ejs', ejsMate);
```
>Create views/layouts/boilerplate.ejs and write:
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Boilerplate!!!</title>
</head>

<body>
    <%- body %>
</body>

</html>
```
>In show.ejs
```
<% layout('layouts/boilerplate') %>

    <body>
        <h1></h1>
    </body>
```
------------------------------------------------------------------------------------------------------------
# PARSES INCOMMING REQUESTS WITH JSON PAYLOADS:
>In App.js:
```
app.use(express.urlencoded({ extended: true }));
```
