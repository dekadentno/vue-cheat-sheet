# Application structure

It is important to read the official [Vue style guide](https://vuejs.org/v2/style-guide/).

When generating a new project with vue-cli with the next command:
```
$ vue init webpack my-project
```
it generates this structure:
```
.
├── build
│   ├── build.js
│   ├── check-versions.js
│   ├── logo.png
│   ├── utils.js
│   ├── vue-loader.conf.js
│   ├── webpack.base.conf.js
│   ├── webpack.dev.conf.js
│   └── webpack.prod.conf.js
├── config
│   ├── dev.env.js
│   ├── index.js
│   └── prod.env.js
├── index.html
├── package.json
├── README.md
├── src
│   ├── App.vue
│   ├── assets
│   │   └── logo.png
│   ├── components
│   │   └── HelloWorld.vue
│   ├── main.js
│   └── router
│       └── index.js
└── static
```

__While the project grows, it is essential to follow the Vue style guide rules and naming convention.__
