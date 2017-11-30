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

### Style guide and naming convention


In this chapter, the focus will be on naming stuff in the vue project, based on the essential and strongly recomended rules from the Vue style guide:
* [Each component should be in its own file](https://vuejs.org/v2/style-guide/#Component-files-strongly-recommended)
* [Components and js files should always be PascalCase](https://vuejs.org/v2/style-guide/#Single-file-component-filename-casing-strongly-recommended)
* [Single-instance components should begin with the "The" prefix](https://vuejs.org/v2/style-guide/#Single-file-component-filename-casing-strongly-recommended)
* [Child components that are tightly coupled with their parent should include the parent component name as a prefix](https://vuejs.org/v2/style-guide/#Tightly-coupled-component-names-strongly-recommended)
* [Component names should start with the highest-level words](https://vuejs.org/v2/style-guide/#Order-of-words-in-component-names-strongly-recommended)
  * suggestion: wrap related components in directories
 * [Component names should prefer full words over abbreviations](https://vuejs.org/v2/style-guide/#Full-word-component-names-strongly-recommended)
