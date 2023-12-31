This is a base node js project template, which anyone can use as it has been prepared, by keeping some of the most important code principles and project management recommendations. Feel free to change anything.

`src` -> Inside the src folder all the actual source code regarding the project will reside, this will not include any kind of tests. (You might want to make separate tests folder)

Lets take a look inside the src folder

`config` -> In this folder anything and everything regarding any configurations or setup of a library or module will be done. For example: setting up dotenv so that we can use the environment variables anywhere in a cleaner fashion, this is done in the server-config.js. One more example can be to setup you logging library that can help you to prepare meaningful logs, so configuration for this library should also be done here.

`routes` -> In the routes folder, we register a route and the corresponding middleware and controllers to it.

`middlewares` -> they are just going to intercept the incoming requests where we can write our validators, authenticators etc.

`controllers` -> they are kind of the last middlewares as post them you call you business layer to execute the budiness logic. In controllers we just receive the incoming requests and data and then pass it to the business layer, and once business layer returns an output, we structure the API response in controllers and send the output.

`repositories` -> this folder contains all the logic using which we interact the DB by writing queries, all the raw queries or ORM queries will go here.

`services` -> contains the buiness logic and interacts with repositories for data from the database

`utils` -> contains helper methods, error classes etc.

### Setup the project
- Download this template from github and open it in your favourite text editor.
- Go inside the folder path and execute the following command:
```Javascript
  npm install
```

In the root directory create a .env file and add the following env variables
```Javascript
  PORT=<port number of your choice>
  ex:

  PORT=3000
```
   
go inside the src folder and execute the following command:
```Javascript
 npx sequelize init
```

By executing the above command you will get migrations and seeders folder along with a config.json inside the config folder.

If you're setting up your development environment, then write the username of your db, password of your db and in dialect mention whatever db you are using for ex: mysql, mariadb etc

If you're setting up test or prod environment, make sure you also replace the host with the hosted db url.

To run the server execute

```Javascript
  npm run dev
```

------
1. `npm init`
2. `git init`
3. Create .gitignore
4. `npm i express`
5. `npm i dotenv` to manage enviroment variables
6. `npm i http-status-codes`: does all the enum mapping for us.
7. Create `.src` folder, inside that 
    7.1. create `index.js` file, where our basic server configuration going to remain.
    ```Javascript
    const express = require("express");
    const { PORT } = require("./config");

    const app = express();

    app.listen(PORT, () => {
        console.log(`Successfully started the server on PORT: ${PORT}`)
    })
    ```
    7.2. create `.config` folder
        7.2.1. Inside config create `index.js` again
        ```Javascript
       const dotenv = require('dotenv');

       // at any particular time we call this file it'll require the dotenv module, that env module actually returns an object on that object you need to call the config function so that you can actually get our enviroment variables

        dotenv.config();

        //every file that we need  a particular enviroment variable we don't need to separately require *dotenv* what we will do is all exports we will do from dotenv and we will import our config file and everything should be a good to go
        module.exports = {
            PORT: process.env.PORT
        }
        ```
8. Create `.env` files, inside this we write our enviroment variables.
```Javascript
 
PORT = 3000

```

9. Run ``` node src/index.js```
Note: To check what all port running on your system run `sudo lsof -i -P -n | grep LISTEN` works in linux
for windows `netstat -a -b`

10. Create `controllers` `routes` `services` `utils`  `middlewares
` inside src folder and inside all these folders add `index.js`

11. Most of the time we will work with API driven application and API versioning is important so inside our routes we will have different route folder for different versions 

12. Add `"dev": "npx nodemon src/index.js"` inside script tag in package.json file, and run `npm run dev` to setup nodemon 

13. If we have to modularise app routings into separate folders for separate entities, then what we can do is we can make express router. 

- Whenever we will have some coding implementation definetel there will be some bugs and we would like to  have a good login information coming out of those bugs so that we would be able to debug it well, In order to handle that we have a package called  `winston npm`  we will integrate it and manage a small log file


-----

