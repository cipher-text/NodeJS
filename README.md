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


