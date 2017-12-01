# Creating a custom vue-cli webpack template

##### Create a new template

1. fork https://github.com/vuejs-templates/webpack
2. rename the forked repo
3. edit meta.js and package.json files
4. commit and push changes

##### Editing contents (adding packages)

There are two files that have to be edited:
```
./meta.js
./template/package.json
```
__Be careful when choosing the package version in package.json file, otherwise things won't work!__
Check the Node and npm version numbering [guide](https://scotch.io/tutorials/node-and-npm-version-numbering-guide-and-best-practices).
##### Use remote template
```
vue init dekadentno/webpack-barrage project_name
``` 

##### Use remote template
```
vue init /home/matej/Desktop/webpack-barrage project_name
``` 
