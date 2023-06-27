- Node package manager(npm)
    configuration in ``package.json``.
    dependencies:
    ```
    "dependencies": {
    "express": "^4.14.0",
    "package-name": "version{MAJOR.MINOR.PATCH}",
    }
    ```
    ```~4.14.0``` keeps latest to ```4.14.x```
    ```^4.14.0``` keeps latest to ```4.x.x```
    <br>
- Express
    ```
    let express = require('express');
    let app = express();
    ```

    ```app.METHOD(PATH, HANDLER)```
    `METHOD`: http method in lowercase
    `PATH`: relative path on the server
    `HANDLER`: a function that Express calls when the route is matched, of the form `function(req, res) {...}`
    e.g., 
    ```
    app.get('/', function() {
        res.sendFile(absoluteFilePath);
    });
    ```
    serve a string: ```res.send(string);```
    serve a file: ```res.sendFile(absolutePath);```
    serve a json: ```res.json(object);```


    `__dirname`: the Node global variable, project root path

    `.env` file: a hidden file that is used to pass environment variables to the application. Access from `process.env.VAR_NAME`. E.g., ```MESSAGE_STYLE=uppercase```, no quotes, no spaces around the =. Naming convention: the variable names are all UPPERCASE, with words separated by an underscore _.
    <br>
    Middleware: functions that intercept route handlers, adding some kind of information.

    The middleware ```express.static(absPathOfAssetsFolder)``` serves static assets (images, stylesheets, scripts, etc) needed by the application.
    
    Middleware functions are functions that take 3 arguments: the request object, the response object, and the next function in the application’s request-response cycle. 

    Example:
    ```
    function(req, res, next) {
        console.log("I'm a middleware...");
        next();
    }
    ```

    use this middleware (for all requests): ```app.use(express.static(absPathOfAssetsFolder));```
    for POST method only: ```app.post(<middleware-function>)```

    Chain Middleware:
    ```
    app.get('/user', 
        function(req, res, next) {
            req.user = getTheUserSync();  // Hypothetical synchronous operation
            next();
        },
        function(req, res) {
            res.send(req.user);
        }
    );
    ```
    Example (a time server):
    ```
    app.get('/now', 
        function(req, res, next) {
          req.time = new Date().toString();
          next();
        },
        function(req, res) {
          res.json({'time': req.time});
        }
);
    ```

    <br>