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


