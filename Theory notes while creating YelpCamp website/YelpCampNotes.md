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
>To install a package (In the Gitbash of the project folder in Node):
```
$ npm init -y
$ npm i express
```
>App file:
```js
const express = require('express');
const app = express();

app.get/post/put/delete('/campgrounds', async (req, res) => {
    const camps = await Campground.find({});
    res.render('campgrounds/index', { camps })
})

app.listen(3000, () => {
    console.log('Serving on port 3000');
})
```
------------------------------------------------------------------------------------------------------------
# FOR INSTALLING EJS IN NODE:
>To install a package (In the Gitbash of the project folder in Node):
```
$ npm i ejs
```
>App file:
```js
app.set('view engine', 'ejs');
app.set('views', path.join(__dirname, 'views'));

//(We Need "const path = require('path');" for path.join to work)

app.get('/fallinlovewith/:thing'), function(req, res) {
    var thing = req.params.thing;
    res.render('love.ejs', {thingVar: thing}); // we're passing the variable into the .ejs file; we can put multiple pieces of data to be used in our template
});
```
>EJS file:
```html
<h1>You fell in love with: <%= thingVar.toUpperCase() %> <h1>
<!-- everything inside of the '<%= %>' brackets will be treated as a JS code -->
```
* ```<%``` 'Scriptlet' tag, for control-flow, no output
* ```<%=``` Outputs the value into the template (HTML escaped)
* ```<%-``` Outputs the unescaped value into the template

------------------------------------------------------------------------------------------------------------
# FOR INSTALLING MONGOOSE IN NODE:
>To install a package (In the Gitbash of the project folder in Node):
```
$ npm i mongoose
```
>App file:
```js
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost:27017/yelp-camp');

const db = mongoose.connection;
db.on('error', console.error.bind(console, 'connection error:'))
db.once('open', () => {
    console.log('Database connected')
})
```
------------------------------------------------------------------------------------------------------------
# FOR CREATING SCHEMA AND MODEL:
```js
const mongoose = require('mongoose');

const CampgroundSchema = new mongoose.Schema({
    title: String,
    price: String,
});

const Campground = mongoose.model('Campground', CampgroundSchema)

const camp = new Campground({
    title: Malnad,
    price: 250$,
});
```
------------------------------------------------------------------------------------------------------------

# FOR INSTALLING METHOD OVERRIDE IN NODE:
>To install a package (In the Gitbash of the project folder in Node):
```
$ npm i method-override
```
>App file:
```js
const methodOverride = require('method-override');

app.use(methodOverride('_method'))
```
>EJS file:(We can use PUT other than POST and GET by Method Overriding):
```html
<body>
    <form action="/campgrounds/<%=camps._id%>?_method=PUT" method="POST">
    </form>
</body>
```
------------------------------------------------------------------------------------------------------------
# FOR INSTALLING EJS-MATE ON NODE:
>To install a package (In the Gitbash of the project folder in Node):
```
$ npm i ejs-mate
```
>App file:
```js
const ejsMate = require('ejs-mate');

app.engine('ejs', ejsMate);
```
>Create ```views/layouts/boilerplate.ejs``` and write:
```html
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
>EJS file:
```html
<% layout('layouts/boilerplate') %>

    <body>
        <h1>Demo code</h1>
    </body>
```
------------------------------------------------------------------------------------------------------------
# PARSES INCOMMING REQUESTS WITH JSON PAYLOADS:
>App file:
```js
app.use(express.urlencoded({ extended: true }));
```
------------------------------------------------------------------------------------------------------------
# TO CREATE PARTIALS FOR NAVBAR AND FOOTER
>Create a file ```views/partials/navbar.ejs``` and create navbar
```html
<nav class="navbar sticky-top navbar-expand-lg navbar-dark bg-dark">
    <div class="container-fluid">
    </div>
</nav>
```
>In boilerplate.ejs paste  ```<%- include('../partials/navbar') %>``` inside ```<body>```
```html
<body>
    <%- include('../partials/navbar') %>
        <main>
        <h1>demo code</h1>
        </main>
</body>
```
------------------------------------------------------------------------------------------------------------
# CLIENT-SIDE FORM VALIDATIONS USING BOOTSTRAP
>EJS file:
* Add ```required```in the form inputs
* Add ```novalidate```in the form header
* Add ```class="needs-validation"```in the form header
Example:
```html
 <div class="row">
            <form action="/campgrounds" method="POST" novalidate class="needs-validation">
                <div class="mb-3">
                    <label class="form-label" for="title">Title</label>
                    <input class="form-control" type="text" id="title" name="campground[title]" required>
                </div>
                <div class="mb-3">
                    <label class="form-label" for="location">Location</label>
                    <input class="form-control" type="text" id="location" name="campground[location]" required>
                </div>
            </form>
            <a href="/campgrounds">All Campgrounds</a>
        </div>
    </div>
```
>Add Script from the bootstrap to EJS file or boilerplate:
(The class name of the form and script should be same as shown below)
```html
    <script>
        (function () {
            'use strict'

            // Fetch all the forms we want to apply custom Bootstrap validation styles to
            var forms = document.querySelectorAll('.needs-validation')

            // Loop over them and prevent submission
            Array.prototype.slice.call(forms)
                .forEach(function (form) {
                    form.addEventListener('submit', function (event) {
                        if (!form.checkValidity()) {
                            event.preventDefault()
                            event.stopPropagation()
                        }

                        form.classList.add('was-validated')
                    }, false)
                })
        })()
    </script>
```
------------------------------------------------------------------------------------------------------------
# PLACEMENT OF APP.USE AND ERROR HANDLER IN EXPRESS:
```js
const express = require('express');
const path = require('path');

const app = express();


app.set('view engine', 'ejs');
app.set('views', path.join(__dirname, 'views'))

// >>>THIS WILL HIT FIRST ALWAYS WHEN THE ANY REQUEST IS CALLED(MAKE SURE TO ADD "next()"):<<<
app.use((req, res, next) => {
    console.log('23d323232e32e32e')
    next();
})

app.get('/dogs', (req, res) => {
    res.render('home')
})

// >>>THIS WILL HIT IF ANY THE REQUEST OTHER THAN ABOVE ARE HIT LIKE : http://localhost:3000/dewewwcdcceccccwcwc <<<
app.use((req, res) => {
    res.send('ERRORRRRR')
})

>>>ERROR HANDLER SHOULD BE PLACED AT THE END:<<<
app.use((err, req, res, next) => {
    res.status(500).send('Something broke!')
})

app.listen(3000, () => {
    console.log('SERVER RUNNING ON 3000')
})
```
------------------------------------------------------------------------------------------------------------
# HANDLING ERRORS IN EXPRESS APPS:
>Create file ```utils/ExpressError.js```
```js
class ExpressError extends Error {
    constructor(message, statusCode) {
        super();
        this.message = message;
        this.statusCode = statusCode;
    }
}
module.exports = ExpressError;
```
>Create file ```utils/catchAsync.js```
```js
module.exports = func => {
    return (req, res, next) => {
        func(req, res, next).catch(next);
    }
}
```
>Create file ``views/error.ejs```
```html
<% layout('layouts/boilerplate')%>
<div class="row">
    <div class="col-6 offset-3">
        <div class="alert alert-danger" role="alert">
            <h4 class="alert-heading"><%=err.message%></h4>
            <p><%= err.stack %></p>
        </div>
    </div>
</div>
```
>App file:
```js
const catchAsync = require('./utils/catchAsync');
const ExpressError = require('./utils/ExpressError');

app.post('/campgrounds', validateCampground, catchAsync(async (req, res, next) => {
    // if (!req.body.campground) throw new ExpressError('Invalid Campground Data', 400);
    const campground = new Campground(req.body.campground);
    await campground.save();
    res.redirect(`/campgrounds/${campground._id}`)
}))

//The below codes should be after all request methods like get,post,put,delete:

app.all('*', (req, res, next) => {
    next(new ExpressError('Page Not Found', 404))
})

app.use((err, req, res, next) => {
    const { statusCode = 500 } = err;
    if (!err.message) err.message = 'Oh No, Something Went Wrong!'
    res.status(statusCode).render('error', { err })
})
```
------------------------------------------------------------------------------------------------------------
# SERVER-SIDE VALIDATIONS (JOI SCHEMA VALIDATIONS): VALIDATE THE DATA WHEN YOU POST, CREATE OR UPDATE THE DATA:
>To install a package (In the Gitbash of the project folder in Node):
```
>$ npm i joi
```
>Create file```YelpCamp/schemas.js```
```js
const Joi = require('joi');

module.exports.campgroundSchema = Joi.object({
    campground: Joi.object({
        title: Joi.string().required(),
        price: Joi.number().required().min(0),
        image: Joi.string().required(),
        location: Joi.string().required(),
        description: Joi.string().required()
    }).required()
});
```
>App file:
```js
const { campgroundSchema } = require('./schemas.js');

const validateCampground = (req, res, next) => {
    const { error } = campgroundSchema.validate(req.body);
    if (error) {
        const msg = error.details.map(el => el.message).join(',')
        throw new ExpressError(msg, 400)
    } else {
        next();
    }
}

app.put('/campgrounds/:id', validateCampground, catchAsync(async (req, res) => {
    const { id } = req.params;
    const campground = await Campground.findByIdAndUpdate(id, { ...req.body.campground });
    res.redirect(`/campgrounds/${campground._id}`)
}));

//The Updating and Posting will complete only if the ```validateCampground``` will not put error.
```
------------------------------------------------------------------------------------------------------------
# DATA RELATIONSHIPS WITH MONGO:
>One To Few:
```js
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost:27017/relationshipDemo', { useNewUrlParser: true, useUnifiedTopology: true })
    .then(() => {
        console.log("MONGO CONNECTION OPEN!!!")
    })
    .catch(err => {
        console.log("OH NO MONGO CONNECTION ERROR!!!!")
        console.log(err)
    })

const userSchema = new mongoose.Schema({
    first: String,
    last: String,
    addresses: [
        {
            _id: { id: false },
            street: String,
            city: String,
            state: String,
            country: String
        }
    ]
})

const User = mongoose.model('User', userSchema);

const makeUser = async () => {
    const u = new User({
        first: 'Harry',
        last: 'Potter'
    })
    u.addresses.push({
        street: '123 Sesame St.',
        city: 'New York',
        state: 'NY',
        country: 'USA'
    })
    const res = await u.save()
    console.log(res)
}

const addAddress = async (id) => {
    const user = await User.findById(id);
    user.addresses.push(
        {
            street: '99 3rd St.',
            city: 'New York',
            state: 'NY',
            country: 'USA'
        }
    )
    const res = await user.save()
    console.log(res);
}
```
>One To Many:
```js
const mongoose = require('mongoose');
const { Schema } = mongoose;

mongoose.connect('mongodb://localhost:27017/relationshipDemo', { useNewUrlParser: true, useUnifiedTopology: true })
    .then(() => {
        console.log("MONGO CONNECTION OPEN!!!")
    })
    .catch(err => {
        console.log("OH NO MONGO CONNECTION ERROR!!!!")
        console.log(err)
    })

const userSchema = new Schema({
    username: String,
    age: Number
})

const tweetSchema = new Schema({
    text: String,
    likes: Number,
    user: { type: Schema.Types.ObjectId, ref: 'User' }
})

const User = mongoose.model('User', userSchema);
const Tweet = mongoose.model('Tweet', tweetSchema);

// const makeTweets = async () => {
//     // const user = new User({ username: 'chickenfan99', age: 61 });
//     const user = await User.findOne({ username: 'chickenfan99' })
//     const tweet2 = new Tweet({ text: 'bock bock bock my chickens make noises', likes: 1239 });
//     tweet2.user = user;
//     tweet2.save();
// }

// makeTweets();

const findTweet = async () => {
    const t = await Tweet.find({}).populate('user')
    console.log(t);
}

findTweet();
```
>One to "Bajillions":
```js
const mongoose = require('mongoose');
const { Schema } = mongoose;

mongoose.connect('mongodb://localhost:27017/relationshipDemo', { useNewUrlParser: true, useUnifiedTopology: true })
    .then(() => {
        console.log("MONGO CONNECTION OPEN!!!")
    })
    .catch(err => {
        console.log("OH NO MONGO CONNECTION ERROR!!!!")
        console.log(err)
    })


const productSchema = new Schema({
    name: String,
    price: Number,
    season: {
        type: String,
        enum: ['Spring', 'Summer', 'Fall', 'Winter']
    }
});

const farmSchema = new Schema({
    name: String,
    city: String,
    products: [{ type: Schema.Types.ObjectId, ref: 'Product' }]
})

const Product = mongoose.model('Product', productSchema);
const Farm = mongoose.model('Farm', farmSchema);

// Product.insertMany([
//     { name: 'Goddess Melon', price: 4.99, season: 'Summer' },
//     { name: 'Sugar Baby Watermelon', price: 4.99, season: 'Summer' },
//     { name: 'Asparagus', price: 3.99, season: 'Spring' },
// ])

const makeFarm = async () => {
    const farm = new Farm({ name: 'Full Belly Farms', city: 'Guinda, CA' });
    const melon = await Product.findOne({ name: 'Goddess Melon' });
    farm.products.push(melon)
    await farm.save()
    console.log(farm);
}

const addProduct = async () => {
    const farm = await Farm.findOne({ name: 'Full Belly Farms' });
    const watermelon = await Product.findOne({ name: 'Sugar Baby Watermelon' });
    farm.products.push(watermelon);
    await farm.save();
    console.log(farm);
}


Farm.findOne({ name: 'Full Belly Farms' })
    .populate('products')
    .then(farm => console.log(farm))
```
------------------------------------------------------------------------------------------------------------
# ROUTER
Express Routers are a way to organize your Express application such that your primary app. js file does not become bloated and difficult to reason about. 
>Create file ```routes/reviews.js``` and write:
```js
const express = require('express');
const router = express.Router({ mergeParams: true });

//Add { mergeParams: true } to get access to all the params fron app.js to reviews.js
//Ex: Now the Id params can be accessed in the reviews.js from app.use('/campgrounds/:id/reviews', reviews)

const Campground = require('../models/campground');
const Review = require('../models/review');

const { reviewSchema } = require('../schemas.js');

const ExpressError = require('../utils/ExpressError');
const catchAsync = require('../utils/catchAsync');

const validateReview = (req, res, next) => {
    const { error } = reviewSchema.validate(req.body);
    if (error) {
        const msg = error.details.map(el => el.message).join(',')
        throw new ExpressError(msg, 400)
    } else {
        next();
    }
}

router.post('/', validateReview, catchAsync(async (req, res) => {
    const campground = await Campground.findById(req.params.id);
    const review = new Review(req.body.review);
    campground.reviews.push(review);
    await review.save();
    await campground.save();
    req.flash('success', 'Created new review!');
    res.redirect(`/campgrounds/${campground._id}`);
}))

router.delete('/:reviewId', catchAsync(async (req, res) => {
    const { id, reviewId } = req.params;
    await Campground.findByIdAndUpdate(id, { $pull: { reviews: reviewId } });
    await Review.findByIdAndDelete(reviewId);
    req.flash('success', 'Successfully deleted review')
    res.redirect(`/campgrounds/${id}`);
}))

module.exports = router;
```
>App file:
```js
const reviews = require('./routes/reviews');

app.use('/campgrounds/:id/reviews', reviews)
```
------------------------------------------------------------------------------------------------------------
# SESSION
express-session is a middleware module in Express. js that allows you to create sessions in your web application. It stores session data on the server side, using a variety of different storage options, and allows you to track the activity of a user across requests.
> To install a package (In the Gitbash of the project folder in Node):
```
$ npm i express-session
```
> App file:
```js
const session = require('express-session');

const sessionConfig = {
    secret: 'thisshouldbeabettersecret!',
    resave: false,
    saveUninitialized: true,
    cookie: {
        httpOnly: true,
        expires: Date.now() + 1000 * 60 * 60 * 24 * 7,
        maxAge: 1000 * 60 * 60 * 24 * 7
    }
}

app.use(session(sessionConfig))
```
------------------------------------------------------------------------------------------------------------
# FLASH (AFTER INSTALLING SESSION ABOVE) 
The connect-flash module in NodeJS allows developers to render a pop-up message whenever a user is redirected to a particular webpage. For example, in your Nodejs demo application, you want to notify your users on logging in and logging out.
> To install a package (In the Gitbash of the project folder in Node):
```
$ npm i connect-flash
```
> App file:
```js
const flash = require('connect-flash');

app.use(flash());

app.use((req, res, next) => {
    res.locals.success = req.flash('success');
    res.locals.error = req.flash('error');
    next();
})
//Above code should be before the route handlers
//res.locals is an object that provides a way to pass data through the application during the request-response cycle. It allows you to store variables that can be accessed by your templates and other middleware functions.
```

> In ```routes/reviews``` add ```req.flash('success', 'Created new review!');```
```js
router.post('/', validateReview, catchAsync(async (req, res) => {
    const campground = await Campground.findById(req.params.id);
    const review = new Review(req.body.review);
    campground.reviews.push(review);
    await review.save();
    await campground.save();
    req.flash('success', 'Created new review!');
    res.redirect(`/campgrounds/${campground._id}`);
}))
```
> In ```views/layouts/boilerplate.ejs``` add ```<%= success %>```
```html
<body>  
    <main>
        <%= success %>
        <%- body %>
    </main>
</body>

// Now you will get 'Created new review!' message above body when you post something.
```

------------------------------------------------------------------------------------------------------------
# PASSPORT (REGISTER, LOGIN, LOGOUT) 
The Passport is a node package, or library which we can install in any nodeJs project. The Passport provides the functionality for authentication in the app. Also, it provides different encryption strategies to encrypt user information, such as a password.
> To install a package (In the Gitbash of the project folder in Node):
```
$ npm i passport passport-local passport-local-mongoose
```
> Create ```models/user.js``` in write:
```js
const mongoose = require('mongoose');
const passportLocalMongoose = require('passport-local-mongoose');

const UserSchema = new mongoose.Schema({
    email: {
        type: String,
        required: true,
        unique: true
    }
});

UserSchema.plugin(passportLocalMongoose);

module.exports = mongoose.model('User', UserSchema);
```
> App file:
```js
const passport = require('passport');
const LocalStrategy = require('passport-local');
const User = require('./models/user');

const userRoutes = require('./routes/users');

app.use(passport.initialize());
app.use(passport.session());
passport.use(new LocalStrategy(User.authenticate()));

passport.serializeUser(User.serializeUser());
passport.deserializeUser(User.deserializeUser());

app.use((req, res, next) => {
    console.log(req.session)
    res.locals.success = req.flash('success');
    res.locals.error = req.flash('error');
    next();
})
```
> Create ```views/users/register.ejs```and write:
```html
// REGISTER EJS PAGE:

<% layout('layouts/boilerplate')%>
<h1>Register</h1>
<form action="/register" method="POST" class="validated-form" novalidate>
    <div class="mb-3">
        <label class="form-label" for="username">Username</label>
        <input class="form-control" type="text" id="username" name="username" required>
        <div class="valid-feedback">
            Looks good!
        </div>
    </div>
    <div class="mb-3">
        <label class="form-label" for="email">Email</label>
        <input class="form-control" type="email" id="email" name="email" required>
        <div class="valid-feedback">
            Looks good!
        </div>
    </div>
    <div class="mb-3">
        <label class="form-label" for="password">Password</label>
        <input class="form-control" type="password" id="password" name="password" required>
        <div class="valid-feedback">
            Looks good!
        </div>
    </div>
    <button class="btn btn-success">Register</button>
</form>
```
> Create ```views/users/login.ejs```and write:
```html
// LOGIN EJS PAGE:

<% layout('layouts/boilerplate')%>
<h1>Login</h1>
<form action="/login" method="POST" class="validated-form" novalidate>
    <div class="mb-3">
        <label class="form-label" for="username">Username</label>
        <input class="form-control" type="text" id="username" name="username" required>
        <div class="valid-feedback">
            Looks good!
        </div>
    </div>

    <div class="mb-3">
        <label class="form-label" for="password">Password</label>
        <input class="form-control" type="password" id="password" name="password" required>
        <div class="valid-feedback">
            Looks good!
        </div>
    </div>
    <button class="btn btn-success">Login</button>
</form>
```
> Create ```routes/users.js``` and write:
```js
const express = require('express');
const router = express.Router();
const passport = require('passport');
const catchAsync = require('../utils/catchAsync');
const User = require('../models/user');

//FOR REGISTER:

router.get('/register', (req, res) => {
    res.render('users/register');
});

router.post('/register', catchAsync(async (req, res, next) => {
    try {
        const { email, username, password } = req.body;
        const user = new User({ email, username });
        const registeredUser = await User.register(user, password);
        req.login(registeredUser, err => {
            if (err) return next(err);
            req.flash('success', 'Welcome to Yelp Camp!');
            res.redirect('/campgrounds');
        }) // Refer Udemy 528
    } catch (e) {
        req.flash('error', e.message);
        res.redirect('register');
    }
}));

//FOR LOGIN:

router.get('/login', (req, res) => {
    res.render('users/login');
})

router.post('/login', passport.authenticate('local', { failureFlash: true, failureRedirect: '/login' }), (req, res) => {
    req.flash('success', 'welcome back!');
    const redirectUrl = req.session.returnTo || '/campgrounds';
    delete req.session.returnTo;
    res.redirect(redirectUrl);
})

//FOR LOGOUT:

// Add button for logout wherever required!
router.get('/logout', (req, res, next) => {
    req.logout(function (err) {
        if (err) {
            return next(err);
        }
        req.flash('success', 'Goodbye!');
        res.redirect('/campgrounds');
    });
}); 

module.exports = router;
```
------------------------------------------------------------------------------------------------------------
# isLoggedIn MIDDLEWARE 
Middleware to protect from creating new campgrounds when nobody is logged in.
> Create ```YelpCamp/middleware.js``` and write:
```js
module.exports.isLoggedIn = (req, res, next) => {
    if (!req.isAuthenticated()) {
        req.session.returnTo = req.originalUrl
        req.flash('error', 'You must be signed in first!');
        return res.redirect('/login');
    }
    next();
}
```
> In ```routes/campgrounds.js``` add ```isLoggedIn``` middleware:
```js
const { isLoggedIn } = require('../middleware');

//Adding 'isLoggedIn' Middleware to protect from creating new campgrounds when nobody is logged in.
router.get('/new', isLoggedIn, (req, res) => {
    res.render('campgrounds/new');
})
```
------------------------------------------------------------------------------------------------------------
# CURRENT USER HELPER 
To show Login and register button if there is no currentUser else Logout will be showed.
> In ```YelpCamp/app.js``` add ```res.locals.currentUser = req.user;``` so that we can have access in every template :
```js
app.use((req, res, next) => {
    console.log(req.session)
    res.locals.currentUser = req.user;
    res.locals.success = req.flash('success');
    res.locals.error = req.flash('error');
    next();
})
//res.locals is an object that provides a way to pass data through the application during the request-response cycle. It allows you to store variables that can be accessed by your templates and other middleware functions.
// So that we can have access in every template
```
> In ```YelpCamp/views/partials/navbar.ejs``` add if condition:
```html
<div class="navbar-nav ml-auto">
  <% if(!currentUser) {%>
     <a class="nav-link" href="/login">Login</a>
     <a class="nav-link" href="/register">Register</a>
  <% } else {%>
     <a class="nav-link" href="/logout">Logout</a>
  <% } %>
</div>
// Login and register button will be showed if there is no currentUser else Logout will be showed.
```
------------------------------------------------------------------------------------------------------------
# ReturnTo Behavior
To redirect users back to the page they were visiting before being sent to the login page, once they've successfully logged in.
> In ```YelpCamp/middleware.js``` add function ```module.exports.storeReturnTo``` and add line ```req.session.returnTo = req.originalUrl``` to ```module.exports.isLoggedIn```
```js
module.exports.isLoggedIn = (req, res, next) => {
    if (!req.isAuthenticated()) {
        req.session.returnTo = req.originalUrl
        req.flash('error', 'You must be signed in first!');
        return res.redirect('/login');
    }
    next();
}

module.exports.storeReturnTo = (req, res, next) => {
    if (req.session.returnTo) {
        res.locals.returnTo = req.session.returnTo;
    }
    next();
}
```
> In ```YelpCamp/routes/users.js``` add:
```js
const { storeReturnTo } = require('../middleware');

//add the 'storeReturnTo' middleware function before the passport.authenticate middleware
router.post('/login',
    // use the storeReturnTo middleware to save the returnTo value from session to res.locals
    storeReturnTo,
    // passport.authenticate logs the user in and clears req.session
    passport.authenticate('local', {failureFlash: true, failureRedirect: '/login'}),
    // Now we can use res.locals.returnTo to redirect the user after login
    (req, res) => {
        req.flash('success', 'Welcome back!');
        const redirectUrl = res.locals.returnTo || '/campgrounds'; // update this line to use res.locals.returnTo now
        res.redirect(redirectUrl);
    });
```
------------------------------------------------------------------------------------------------------------
# AUTHORIZATION
## After login when creating the new campground the userId of who loggedIn is added to campground as author
> In ```YelpCamp/models/campground.js```
```js
// add `author` to schema
const CampgroundSchema = new Schema({
    title: String,
    image: String,
    price: Number,
    description: String,
    location: String,
    author: {
        type: Schema.Types.ObjectId,
        ref: 'User'
    },
    reviews: [
        {
            type: Schema.Types.ObjectId,
            ref: 'Review'
        }
    ]
});
```
> In ```YelpCamp/routes/campgrounds.js```
```js
// Add "campground.author = req.user._id;" to post
router.post('/', isLoggedIn, validateCampground, catchAsync(async (req, res, next) => {
    const campground = new Campground(req.body.campground);
    campground.author = req.user._id;
    await campground.save();
    req.flash('success', 'Successfully made a new campground!');
    res.redirect(`/campgrounds/${campground._id}`)
}))
```
## Showing of Edit/Delete Button if I am logged in as Owner of that Campground and Hiding of Edit/Delete Button if I am not owner of the content.
> In ```YelpCamp/views/campgrounds/show.ejs```:
```html
// Add if condition to if there is currentUser and that user is owner of the content.
<%  if( currentUser && campground.author.equals(currentUser._id))  {%>
         <div class="card-body">
                <a class="card-link btn btn-info" href="/campgrounds/<%=campground._id%>/edit">Edit</a>
                <form class="d-inline" action="/campgrounds/<%=campground._id%>?_method=DELETE" method="POST">
                    <button class="btn btn-danger">Delete</button>
                </form>
         </div>
<% } %>
```
## Authorization Middleware:
We are succesfully hiding the edit and delete buttons if you don't own the campground But we can still send a request through postmen, for example: /edit, So we definitely want to protect this route as well by using middleware:
> In ```YelpCamp/middleware.js```:
```js
const Campground = require('./models/campground');

//is author middleware
module.exports.isAuthor = async (req, res, next) => {
    const { id } = req.params;
    const campground = await Campground.findById(id);
    if (!campground.author.equals(req.user._id)) {
        req.flash('error', 'You do not have permission to do that!');
        return res.redirect(`/campgrounds/${id}`);
    }
    next();
}
```
> In ```YelpCamp/routes/campgrounds.js```:
```js
// add 'isLoggedIn;
const { isLoggedIn, isAuthor, validateCampground } = require('../middleware');

// Add isAuthor Middleware to routes where you want Authorization
// Now if the Campground is not owned by the owner you can't Edit/Delete from the postman as well.
router.get('/:id/edit', isLoggedIn, isAuthor, catchAsync(async (req, res) => {
    const { id } = req.params;
    const campground = await Campground.findById(id)
    if (!campground) {
        req.flash('error', 'Cannot find that campground!');
        return res.redirect('/campgrounds');
    }
    res.render('campgrounds/edit', { campground });
}))
```
------------------------------------------------------------------------------------------------------------







