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
###### JOI
```
npm i joi
```

```
const Joi = require("joi");
const Schema = Joi.object({
 name: Joi.string().min(3).required(),
 message: Joi.sting(),
 price: Joi.number(),
});

const product={
name:"xyz",
message:"dklsfljakjdf",
price: 20
}
const result = Schema.validate(product);
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

```
#### Working with Mongodb
![mongodb image](https://www.openlogic.com/sites/openlogic/files/image/2019-07/image-blog-big-data-on-demand-with-mongodb.jpg)
> mongodb is use to store no sql data
> Here we are going to use mongoose package that make easy to use and connect to mongodb
> here is the procedure to connect with mongodb
* download and install mongodb community server
* after install you will get mongodb compass community where you can see your db 
* now install mongoose in your project using ``` npm i mongoose```
```
const mongoose = require("mongoose");
mongoose.connect("mongodb://localhost/test_db",{useNewUrlParser: true,
    useUnifiedTopology: true,})
    .then(()=>console.log("connected to db"))
    .catch((err)=>console.log("error:",err));
```
* now if everything goes correct it will be connected to db ( here we are creating tes_db)
* now to create and store document in collection we are going to create schema ( that is the concept of mongoose)
* here are all different types of schema that we can use in schema creation
1. String
2. Number
3. Date
4. Buffer
5. Boolean
6. ObjectID
7. Array
```
const productSchema = mongoose.Schema({
 name:String,
 price: Number,
 tags: [String]
});


const Product = mongoose.model("Product", productSchema);

const product = new Product({
name:"ABC",
price: 199,
tags:["test","try","learn"]
})

```
* first we created the schema of document that is the concept of mongoose (it is not present is mongodb)
* now from this schema we created a model that is a class (in our example that is Product)
* now from this model we created object that is our document
* to save this just call the save method from model notice that save is asynchronous
```
async function saveData(){
 const result = await Product.save();
 console.log(result);
 }
 saveData();
```

* Querying the documents from db
```
async function getData(){
const result = await Product.find({here you can pass one or more key value which you are looking for})
 .limit(number_of_documents)
 .select({in this object you can pass what values you want to select from document like price:1, name:1 })
 .sort({in this object you can pass the one or more keys on the basis of which you want to sort the query result like price: 1 for asc and price:-1 for desc})
```
* using comparison operators these are also present in mongodb that are borrowed
* comparison operators
```
eq (equal)
neq (not equal)
lt (less than)
lte (less than or equal)
gt (greater than)
gte (greater than or equal)
nt (not)
nte (not equal)

```
>use them like this 
```
Product.find({price: {$gt:10}};
Product.find({price: {$gte:10,$lt:20}};
Product.find({price: {$in:[10,20,30]};
```
* logical operators
```
and 
or
```
>use them like this
```
Product.find()
 .or([{name:"abc"},{name:"xyz"}]);
```

> using regualar expression
```
/pattern/

^a  => starts with a 
a$ => ends with a
* => 0 or more
. => one
```
```
Product.find({name:/^a/});
```

> sometime you just want to return only count
```
Product.find().count();
```

* pagination

```
const pageNumber = 2;
const pageSize = 10;
Product.find()
 .skip((pageNumber-1)*pageSize)
 .limit(pageSize)

```
* validation
> mongodb does not provide data validation if you save empty document it will save it.
> mongoose provide validation you can use it in schema declaration
```
const productSchema = mongoose.Schema({
 name: {type:String, required:true},
 date: { type: Date, default: Date.now})
})
```
> mongoose built in validators
```
const productSchema = mongoose.Schema({
 name: {
  type:String, 
  required:true,
  minlength: 5,
  maxlength: 25,
  match: /pattern/},
  
  
 isAdded:true,
 
 date: { 
  type: Date,
  default: Date.now,
  required: function(){return this.isAdded}   // custom required  note that you can't use arrow function here because they refer to global scope
  min:--,
  max: --
 }),
 price:{
  type: Number,
  required: true,
  min: 10,
  max: 20,
}),
category:{
type:String,
required: true,
enum: ["fashion", "electronics", "grocery"]   // here only these three values will be valid and all other will be wrong
}
```
> custom validator

```
tags:{
 type: Array,
 validate:{
  validator: function(v){
   return v&&v.length;    //tag should have atleast one value and can't be null
  },
  message:"A course should have atleast one tag"
 }
 }
 ```
 > Asynchronous course validation
 
 ```
 tags:{
 type: Array,
 validate:{
  isAsync: true,
  validator: function(v, callback){
   setTimeout(()=>{
    const result =  v&&v.length;    //tag should have atleast one value and can't be null
    callback(result);
   },4000);
  },
  message:"A course should have atleast one tag"
 }
 }
 ```
 >some other schema properties
 > for type:string
 ```
 {
 type: String,
 trim: true,
 uppercase:true   /or lowercase: true,
 }
 
 {
 type: Number,
 set: (v)=>Math.round(v),  // when we try to save it will round off value
 get: (v)=>Math.round(v),  // when we try to get value it will give round off value
 }
```
* referencing a doucument 

> courses collection
```
const courseSchema = new mongoose.Schema({
 name: String,
 author: {
  type: mongoose.Schema.Types.ObjectID,
  ref: "Author"
 }
})
```
> authors collection
```
const authorSchema = new mongoose.Schema({
 name: String,
 info: String,
});
```
> now when you create the the object of course and save it passs the id of author (objectid)
> now if you want that when you query the course you get the author from authors collection which you are refering then call the populate method (not that if you pass wrong id    > to refrence if not going to give error becuase it is not relational db
```
Course.find().populate("author", { "name"});
```
* embedding document
{
 name:String,
 author: authroSchema
 }
 
> updating subarray
```
const course = await findById(courseid);
const author = course.authors.id(authorid);
author.name="adkfjs"
author.save();
```
##### list of package
* Joi
* mongoose
* winston
* jsonwebtoken
* jest ( for testing)
* joi-objectid
* lodash
* joi-password-complexity
* bcrypt ( for password encryption)

###### String validation
*type,
*minlength,
*maxlength,
*required,
*trim,
*enum
```
category:{
 type: String,
 enum: ["fashion", "sports"],
 required:function(){ return this.isPublished},
 }
 ```
 ###### Number validation
 *type,
 *required,
 *min,
 *max
 
 ##### custom validator
 ```
 tags: {
 type: Array,
 validate:{
 }
 validator: function(v){
 return v&&v.length>0;
 }
 }
 ```
 ##### custom validator async
 ```
 tags: {
 type: Array,
 validate:{
 isAsync: true,
  validator: function(v, callback){
  setTimeout(()=>{
    const result =  v&&v.length>0;
    callback(result);
   } }
 }
  }
 ```
 
 ##### getter and setter
 ```
 price:{
  type: Number,
  required: true,
  get: v=> Math.round(v),
  set: v=> Math.round(v),
  }
  ```
  
  ##### ObjectID validation
  ```
  mongoose.Types.ObjectId.isValid()
  ```
  
  ###### hashing password
  > bcrypt is a one way encription where you can encrypt password but you can't decrypt
  > but suppose if hacker got access in database and he/she have list of popular password then they he/she can encrypt those popular password and encrypt and compare
  > that why we need to add salt which is some random string that is added before or after the password
  
  ##### How Node js work
  
 > single thread
 > nodejs = v8+libuv+other
 > libuv = Evenloop + Thread Pool
  ![node architecture](https://github.com/cipher-text/NodeJS/blob/master/images/img3.png)
  ![node process and thread](https://github.com/cipher-text/NodeJS/blob/master/images/img4.png)

