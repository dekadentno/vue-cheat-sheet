# vue-cheat-sheet
My cheat sheet for vue.js most basic stuff
---
### Basic HTML and JS
```html
<html>
	<head>
		<meta charset="utf8">
		<title>VueJS example</title>
		<link href="style.css" rel="stylesheet" />
		<script src="https://cdn.jsdelivr.net/npm/vue"></script>
	</head>

	<body>
		<div id="vue-app"></div>

		<script src="app.js"></script>
	</body>
</html>
```
```javascript
new Vue({
	el: '#vue-app', // contoled element

	data: {
		name: "Matej",
		age: 27,
		sleepy: true
	},

	methods: {
		test: function () {
			console.log("test");
		},
	computed:{}
});
```
---
### HTML directives

Show/hide div
> where _available_ is a boolean variable in the js 
```html
<div v-show="{{available}}">Stuff</div>
```
Toggle show/hide div
> where _available_ is a boolean variable in the js 
```html
<div v-show="{{available = !available}}">Stuff</div>
```

Render div
> where _available_ is a boolean variable in the js 
```html
<div v-if="{{available}}">Stuff</div>
<div v-else>Smth else</div>
```

Looping
> array of strings
```html
<ul>
    <li v-for="(element, index) in elements">{{index}} {{element}}</li>
</ul>
```
> array of objects
```html
<ul>
    <li v-for="employee in employees">{{employee.name}} - {{employee.age}}</li>
</ul>
```

Set text for element from a variable _name_
```html
<span v-text="name"></span>
```

Set html for element from a variable _name_
```html
<span v-html="name"></span>
```
---
### Two way data binding
```html
input v-model="name" type="text" />
<p>My name is: {{lastName}}</p>
```
```javascript
...
data:{
	name: ""
}
...
```
---
### Events
Call _method_ on click event
> where _method_ is a custom method in the js
```html
<button v-on:click="method">Add</button>
```
> _method_ is called when ALT+ENTER is pressed
```html
<input ref="name" v-on:keyuop.alt.enter="method" type="text" />
```
---

### HTML properties and classes
```html
<p v-bind:style="{ property: value }">...</p>
```
> this div will have the _red_ class if the _userFound_ variable is set to _true_
```html
<div v-bind:class="{ red: userFound }">...</div>
```
---
### Components
> reusable inside the html
```html
<div id="app">
	<signature></signature>
	<signature></signature>
</div>
```
```javascript
// global registration 
Vue.component('signature', { 
     template: '<p>Regards. Matej.</p>'
});
```
---
### References
```html
<input ref="name" type="text" />
```
```javascript
var name = this.$refs.name;

```
---
### .vue components
Source: [iamshaunjp](https://github.com/iamshaunjp/vuejs-playlist)
```vue
<!--App.vue-->
<template>

<div>
  <app-header></app-header>
  <app-ninjas></app-ninjas>
  <app-footer></app-footer>
</div>

</template>

<script>
  // import
  import Header from './components/Header.vue';
  import Footer from './components/Footer.vue';
  import Ninjas from './components/Ninjas.vue';
  export default {
  // register components
    components:{
      // added app- prefix
      // because header and footer tags already exist
      "app-header": Header,
      "app-footer": Footer,
      "app-ninjas": Ninjas
    },

    data () {
      return {

      }
    }

  }

</script>
```
```vue
<!--Ninjas.vue-->
<template>
<div id="ninjas">
  <ul>
    <li v-for="ninja in ninjas">
      <h2>{{ninja.name}} - {{ninja.speciality}}</h2>
    </li>
  </ul>
</div>

</template>

<script>

  export default {


    data () {
      return {
        ninjas:[
          {name: "ninja1", speciality: "vuejs"},
          {name: "ninja2", speciality: "nodejs"},
          {name: "ninja3", speciality: "react"},
          {name: "ninja4", speciality: "js"},
          {name: "ninja5", speciality: "css3"},
          {name: "ninja6", speciality: "ps"}
        ]
      }
    }

  }

</script>
```
```vue
<!--Header.vue-->
<template>
  <header>
    <h1>{{title}}</h1>
  </header>

</template>

<script>

  export default {

    data () {
      return {
        title: "Welcome!"
      }
    }

  }

</script>
```
```vue
<!--Footer.vue-->
<template>
<footer>
  <p>{{copyright}}</p>
</footer>

</template>

<script>

  export default {


    data () {
      return {
        copyright: "Copyright 2017 "
      }
    }

  }

</script>
```

---

### Vue CLI
```
$ vue init webpack-simple my-project
$ cd project-name
$ npm install # install dependencies
$ npm run dev # start a local server for development mod
```
---
