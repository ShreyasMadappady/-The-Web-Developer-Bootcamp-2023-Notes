# In Node:
## -npm i ejs-mate

# In App.js
## -const ejsMate = require('ejs-mate');
## -app.engine('ejs', ejsMate);

# Create views/layouts/boilerplate.ejs
## <!DOCTYPE html>
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
