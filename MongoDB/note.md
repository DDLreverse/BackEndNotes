- Configuration
  MongoDB Atlas Tutorial: `https://www.freecodecamp.org/news/get-started-with-mongodb-atlas/`
  connect in the application:
  ```
  mongodb+srv://<username>:<password>@<cluster-name>.kirpxxr.mongodb.net/<db-name>?retryWrites=true&w=majority
  ```
- CRUD Part
    Create a Model
    Schema: each schema maps tp a MongoDB collection, it defines the shape of the documents within that collection. Schemas are building blocks for Models. They can be nested to create complex models.

    The `done()` function is a callback that tells us that we can proceed after completing an asynchronous operation such as inserting, searching, updating, or deleting. (success: `done(null, data)`, error: `done(error)`).

    ```
    /* Example */
    const someFunc = function(done) {
    //... do something (risky) ...
    if (error) return done(error);
    done(null, result);
    };
    ```
    Example for creating a model
    ```
    let mongoose = require('mongoose');
    mongoose.connect(process.env.MONGO_URI, { useNewUrlParser: true, useUnifiedTopology: true });

    const personSchema = new mongoose.Schema({
    name: {
        type: String,
        required: true
    },
    age: {
        type: Number,
        required: true
    },
    favoriteFoods: [String]
    });

    let Person = mongoose.model('Person', personSchema);
    ```
    Basic operations
    ```Model.find()```
    ```Model.findOne()```
    ```Model.findById()```

    ```Model.update()```: It can bulk-edit many documents matching certain criteria, but it doesn’t send back the updated document, only a 'status' message.
    
IMPORTANT: newer versions of mongoose do not support callback functions in queries (e.g., find()) any more, use the following instead:
1. ```Model.find().then((result) => {})```
2. ```result = await Model.find()```, be sure this is used in async function, e.g., ```app.post('/', async (req, res) => {})```