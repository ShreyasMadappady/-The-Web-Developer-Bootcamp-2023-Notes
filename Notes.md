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
>To install a package (In the Gitbash of the project folder in Node):
```
$ npm i ejs
```
>App file:
```
app.set('view engine', 'ejs');
app.set('views', path.join(__dirname, 'views'));

(We Need "const path = require('path');" for path.join to work)
```
```
app.get('/fallinlovewith/:thing'), function(req, res) {
    var thing = req.params.thing;
    res.render('love.ejs', {thingVar: thing}); // we're passing the variable into the .ejs file; we can put multiple pieces of data to be used in our template
});
```
>EJS file:
```
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
>To install a package (In the Gitbash of the project folder in Node):
```
$ npm i method-override
```
>App file:
```
const methodOverride = require('method-override');
```
```
app.use(methodOverride('_method'))
```
>EJS file:(We can use PUT other than POST and GET by Method Overriding):
```
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
```
const ejsMate = require('ejs-mate');
```
```
app.engine('ejs', ejsMate);
```
>Create ```views/layouts/boilerplate.ejs``` and write:
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
>EJS file:
```
<% layout('layouts/boilerplate') %>

    <body>
        <h1>Demo code</h1>
    </body>
```
------------------------------------------------------------------------------------------------------------
# PARSES INCOMMING REQUESTS WITH JSON PAYLOADS:
>App file:
```
app.use(express.urlencoded({ extended: true }));
```
------------------------------------------------------------------------------------------------------------
# TO CREATE PARTIALS FOR NAVBAR AND FOOTER
>Create a file ```views/partials/navbar.ejs``` and create navbar
```
<nav class="navbar sticky-top navbar-expand-lg navbar-dark bg-dark">
    <div class="container-fluid">
    </div>
</nav>
```
>In boilerplate.ejs paste  ```<%- include('../partials/navbar') %>``` inside ```<body>```
```
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
```
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
```
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
```
const express = require('express');
const path = require('path');

const app = express();


app.set('view engine', 'ejs');
app.set('views', path.join(__dirname, 'views'))

>>>THIS WILL HIT FIRST ALWAYS WHEN THE ANY REQUEST IS CALLED(MAKE SURE TO ADD "next()"):<<<
app.use((req, res, next) => {
    console.log('23d323232e32e32e')
    next();
})

app.get('/dogs', (req, res) => {
    res.render('home')
})

>>>THIS WILL HIT IF ANY THE REQUEST OTHER THAN ABOVE ARE HIT LIKE : http://localhost:3000/dewewwcdcceccccwcwc <<<
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
```
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
```
module.exports = func => {
    return (req, res, next) => {
        func(req, res, next).catch(next);
    }
}
```
>Create file ``views/error.ejs```
```
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
```
const catchAsync = require('./utils/catchAsync');
const ExpressError = require('./utils/ExpressError');
```
```
app.post('/campgrounds', validateCampground, catchAsync(async (req, res, next) => {
    // if (!req.body.campground) throw new ExpressError('Invalid Campground Data', 400);
    const campground = new Campground(req.body.campground);
    await campground.save();
    res.redirect(`/campgrounds/${campground._id}`)
}))
```
The below codes should be after all request methods like get,post,put,delete:
```
app.all('*', (req, res, next) => {
    next(new ExpressError('Page Not Found', 404))
})
```
```
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
```
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
```
const { campgroundSchema } = require('./schemas.js');
```
```
const validateCampground = (req, res, next) => {
    const { error } = campgroundSchema.validate(req.body);
    if (error) {
        const msg = error.details.map(el => el.message).join(',')
        throw new ExpressError(msg, 400)
    } else {
        next();
    }
}
```
```
app.put('/campgrounds/:id', validateCampground, catchAsync(async (req, res) => {
    const { id } = req.params;
    const campground = await Campground.findByIdAndUpdate(id, { ...req.body.campground });
    res.redirect(`/campgrounds/${campground._id}`)
}));
```
The Updating and Posting will complete only if the ```validateCampground``` will not put error.
------------------------------------------------------------------------------------------------------------
# DATA RELATIONSHIPS WITH MONGO:
>One To Few:
```
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
```
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
```
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
>Create file ```routes/reviews.js``` and write:
```
const express = require('express');
const router = express.Router({ mergeParams: true });
```
```
const Campground = require('../models/campground');
const Review = require('../models/review');
```
```
const { reviewSchema } = require('../schemas.js');
```
```
const ExpressError = require('../utils/ExpressError');
const catchAsync = require('../utils/catchAsync');
```
```
const validateReview = (req, res, next) => {
    const { error } = reviewSchema.validate(req.body);
    if (error) {
        const msg = error.details.map(el => el.message).join(',')
        throw new ExpressError(msg, 400)
    } else {
        next();
    }
}
```
```
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
```
```
module.exports = router;
```
>App file:
```
const reviews = require('./routes/reviews');
```
```
app.use('/campgrounds/:id/reviews', reviews)
```
------------------------------------------------------------------------------------------------------------


