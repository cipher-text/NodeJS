# NodeJS

##### what is node??

> Node is a open source cross plateform run time environment which provides plateform to run javascript outside the 
> browser
> node is not a programming language , node is not a framework
> it's runtime environment to excute javascript code
> ![picture](https://github.com/cipher-text/NodeJS/blob/master/images/img1.png)
> ![picture](https://github.com/cipher-text/NodeJS/blob/master/images/img2.png)

> node is single threaded asynchronous(non-blocking)
> node is ideal for data intensive realtime application but it is not ideal for cpu intensive application
> node is a c++ program embedded with google's v8 engine

##### Module
> unlike javascript used in web where everything is global and you can access the content of one file from other in case of node every file is module and content inside that is privte to other's and it can be only accessed outside using export(what we are exporting)
> node provides modularity using wrapper function it wraps the content of file using wrapper function

##### Some useful modules
* OS
* Path
* File System
* Events
* Http

##### NPM
![picture](https://www.npmjs.cn/images/npm-lg.jpg)
> npm is package manager
> to create a package.json file
```
 npm init
```
> OR (Quickly)
```
npm init --yes
```
> to install a package
```
npm i package-name
```
> to install a specific version of package
```
npm i package-name@version
```
> to get the package metadata
```
npm view package-name   
```
> to get the version of installed package
```
npm view package-name version
```
> to get the list of versions of a installed package
```
npm view package-name versions
```
> to get the all dependencies of a package
```
npm view package-name dependencies
```
> to check the list of outdated packages
```
npm outdated
```
> to update the outdate version (note:-) this will work only for minor or patch update
```
npm update
```
> to update the major version install the following package
```
npm i -g npm-check-updates
```
> now after installing the above package run the following commands
```
ncu -u
```
> this will only update the package.json to actully change the package run follwing command after that
```
npm install
```
> to install a package as a development dependency use the following command
```
npm i package-name --save-dev
```
> to uninstall a package use the following command

```
npm uninstall package-name
```
> OR
```
npm un package-name
```
> to update the version of a package
```
npm version major
npm version minor
npm version patch
```

###### publishing a package in npmjs
https://www.npmjs.cn/getting-started/publishing-npm-packages/
> to create an account 
``` 
npm adduser
```
> to login if you have already account in npmjs
```
npm login
```
> to publish a package just run the following command from your package after login
```
npm publish
```
> to update the package and publish again 
> first change the package version
> then publish it again

##### Express
![picture](https://miro.medium.com/max/700/1*XP-mZOrIqX7OsFInN2ngRQ.png)
> express is a framework that is used to create restful services
```
npm i express
```
>  if you want to validate your request body data there are some libraries which can be useful for data validation like joi etc.
```
npm i joi
```
###### middleware
> middleware or middleware function is basically a function that takes request object and it either returns response to the client or passes control to another middleware 
> function
![request processing pipeline image](https://d33wubrfki0l68.cloudfront.net/a22bb45df146d43b57f2f6c90182d19e7394cd96/d6e10/assets-jekyll/blog/express-middleware-examples/middleware-30b3b30ad54e21d8281719042860f3edd9fb1f40f93150233a08165d908f4631.png)
> every request goes through request processing pipeline
> if you want to add a middleware in request processing pipeline
```
app.use(function)

function a(req, res, next){
next();}
```
######### builtin middleware
* express.json()
* express.static()
* express.urlencoded()
######## third party middleware
> go to expressjs->resources->middleware 

##### working with different environment
> you can customize the code on the basis of the environment in which running like development, production etc.
```
process.env.NODE_ENV  (if it is not set then it gives undefined)( in window you can set using set )
```
>OR
```
app.get('env')  (if not set then it gives development)
```

> there are different packages to manage the environment configuration like rc, config etc.

##### how to use config package

```
npm i config
```

```
const config = require("config")
```
> create different json files for different environment like ..    default.json, development.json, production.json and there content will be accessed on the basic on environment
> if you want to hide something from others you can store them into custom environment varialbe like password (set password = 1234)
> to access this password create a file with exact name  custom-environment-variables.json, and here you can map your environment variable.


#### debugging with debug package
![debugging image](https://stackify.com/wp-content/uploads/2018/04/Troubleshooting-vs.-Debugging-1280x720.png)
> normally we use console.log() for debugging purpose but this way is little tedius as when we don't want to show debug information we have to comment out logged messages
```
npm i debug
```
> in debug package you can control your debugging messages with DEBUG environment variable

```
const startupDebug = require("debug")("app:startup")
const dbDebug = require("debug")("app:db")
```

```
startupDebug(" startup debugging message");
dbDebug(" db debug message ");
```
> now if we want to see only startup debugging message just set the DEBUG variable as app:startup
```
set DEBUG=app:startup
```
> simmilarily if you want to see multiple
```
set DEBUG=app:startup,app:db
```
> if you want to see nothing set nothing to DEBUG
```
set DEBUG=
```
#### Tempelating Engine
* pug
* mustache
* EJS

> we are going to use pug
```
npm i pug
```
```
app.set("view engine", "pug");
app.set("views", "./views");  // by default it is already set
```
> now just create a views folder and then pug file like index.pug in views folder
ex.  index.pug
html
 head
  title=title_var
 body
  h1=message
 
 > now we have to render it where we want to send it as response
 ex.
 ```
 app.get("/", (req, res)=>{
  res.render("index", {title_var="dynamic title", message="message dynamic"});
 })
