# Creating a custom vue-cli webpack template

##### Create a new template

1. fork https://github.com/vuejs-templates/webpack
2. rename the forked repo
3. edit meta.js, package.json and main.js files
4. commit and push changes

##### Editing contents (adding packages)

There are 3 files that have to be edited:
```
./meta.js
./template/package.json
./template/src/main.json
```
### An example will be given with the moment.js package

##### meta.js - adding a prompt
```
"moment": {
    "type": "confirm",
    "message": "Install moment?"
},
```

##### package.json - adding dependencies
```
{{#moment}},
"moment": "~2.19.3"
{{/moment}}
```

##### main.js - including the package into main.js
```
{{#moment}}
import moment from 'moment'{{#if_eq lintConfig "airbnb"}};{{/if_eq}}
Vue.use(moment){{#if_eq lintConfig "airbnb"}};{{/if_eq}
{{/moment}}
```

__Be careful when choosing the package version in package.json file, otherwise things won't work!__
Check the Node and npm version numbering [guide](https://scotch.io/tutorials/node-and-npm-version-numbering-guide-and-best-practices).

##### Use remote template
e.g.
```
vue init dekadentno/webpack-barrage project_name
``` 

##### Use local template
e.g.
```
vue init /home/matej/Desktop/webpack-barrage project_name
``` 
