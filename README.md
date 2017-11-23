# vue-cheat-sheet
My cheat sheet for vue.js most basic stuff
Sources:
* [iamshaunjp](https://github.com/iamshaunjp/vuejs-playlist)
* [Vue.js official guide](https://vuejs.org/v2/guide/)

---
## Basic HTML and JS
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
## HTML directives
##### Show / hide div
where _available_ is a boolean variable in the js 
```html
<div v-show="available">Stuff</div>
```
##### Toggle show / hide div
where _available_ is a boolean variable in the js 
```html
<div v-show="available = !available">Stuff</div>
```

##### Render div
where _available_ is a boolean variable in the js 
```html
<div v-if="{{available}}">Stuff</div>
<div v-else>Smth else</div>
```

##### Looping
##### array of strings
```html
<ul>
    <li v-for="(element, index) in elements">{{index}} {{element}}</li>
</ul>
```
##### array of objects
```html
<ul>
    <li v-for="employee in employees">{{employee.name}} - {{employee.age}}</li>
</ul>
```

##### Set text for element from a variable _name_
```html
<span v-text="name"></span>
```
##### Set html for element from a variable _name_
```html
<span v-html="name"></span>
```
---
## Custom HTML directives
##### todo

---
## Filters
##### Change the output data to the browser. They do not change the data directly.
```html
<h1>{{title | to-uppercase}}</h1>
```
```javascript
// main.js
Vue.filter("to-uppercase", function ( value ) {
    return value.toUpperCase();
});
```
---
## Two way data binding
```html
<input v-model="name" type="text" />
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
## Events
##### Call _method_ on click event
where _method_ is a custom method in the js
```html
<button v-on:click="method">Add</button>
```
_method_ is called when ALT+ENTER is pressed
```html
<input ref="name" v-on:keyuop.alt.enter="method" type="text" />
```
---
## Custom events
```javascript
// fire custom event 
this.$emit("eventName", data);
```
```html
<!-- 
$event == event data
when _eventName_ event happens, call _functionName_ function
-->
<p v-on:eventName="functionName($event)"></p>
```
---
## Event bus
##### communicate between child components without the parent component
```javascript
// main.js
// create new event bus
export const bus = new Vue();
```
```html
// Header.vue
import {bus} from "../main";
```
```html
// Footer.vue
import {bus} from "../main";
```
```javascript
// listen to bus event in first component
// usually in .created() function
bus.$on("eventName", (data) => {
	// callback
	// use data
})

// fire bus event in second component
bus.$emit("eventName", data);
```
---

## HTML properties and classes
```html
<p v-bind:style="{ property: value }">...</p>
```
this div will have the _red_ class if the _userFound_ variable is set to _true_
```html
<div v-bind:class="{ red: userFound }">...</div>
```
---
## Components
##### reusable inside the html
```html
<div id="app">
	<!-- <component is="signature"></component> -->
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
## References
```html
<input ref="name" type="text" />
```
```javascript
var name = this.$refs.name;

```
---
## .vue components and props
##### Props - passing data from parent component to child component
```vue
<!--App.vue-->
<template>

<div>
  <app-header></app-header>
  <app-ninjas v-bind:ninjas="ninjas"></app-ninjas>
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
        ninjas:[
          {name: "ninja1", speciality: "vuejs", show: false},
          {name: "ninja2", speciality: "nodejs", show: false},
          {name: "ninja3", speciality: "react", show: false},
          {name: "ninja4", speciality: "js", show: false},
          {name: "ninja5", speciality: "css3", show: false},
          {name: "ninja6", speciality: "ps", show: false}
        ]
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
    <li v-for="ninja in ninjas" v-on:click="ninja.show = !ninja.show">
      <h2>{{ninja.name}}</h2>
      <h3 v-show="ninja.show">{{ninja.speciality}}</h3>
    </li>
  </ul>
</div>

</template>

<script>

  export default {
    // what is it receiving
    props: ["ninjas"],

    data () {
      return {

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
## Dynamic components
dynamically change component based on variable _component_ value
rememberto use _keep-alive_ tag to remember data from the destroyed component
```vue
<template>

<div>
  <component> v-bind:is="componentName"></component>
</div>

</template>

import formOne from "./components/formOne.vue";
import formTwo from "./components/formTwo.vue";

...
data: function() {
	return {
		component: "form-two"
	}
}
```
---
## Validate props
```vue
export default {
	props:{
		ninjas:{
			type: Array,
			required: true
		}
	}
}
```
---

## Vue CLI
```
$ vue init webpack-simple my-project
$ cd project-name
$ npm install # install dependencies
$ npm run dev # start a local server for development mod
```
---
## Vue lifecycle
* new Vue();
* .beforeCreate();
* .created();
* .beforeMount();
* .updated();
* .beforeUpdate();
* .beforeDestroy();
* .destroyed();
![](https://vuejs.org/images/lifecycle.png)
---
## Checkboxes
##### with v-model, the _categories_ array will be appended with the values
```html
<div>
	<label for="">Newsletters</label>
	<input type="checkbox" value="newsletter" v-model="categories">
	<label for="">New posts</label>
	<input type="checkbox" value="post" v-model="categories">
	<label for="">New DMs</label>
	<input type="checkbox" value="dm" v-model="categories">
	<label for="">New pokes</label>
	<input type="checkbox" value="pokes" v-model="categories">
</div>
```
```javascript
data: function () {
	categories: []
}
```
---
## Select box binding
##### hardcoded and looped select
```html
<div>
	<select v-model="town">
	  <option value="osijek">Osijek</option>
	  <option value="zagreb">Zagreb</option>
	  <option value="varazdin">Varazdin</option>
	</select>

	<select v-model="town">
	  <option v-for="t in towns">{{ t }}</option>
	</select>
</div>
```
```javascript
data: function () {
	town: "",
        towns: ["Zagreb", "Osijek", "Varazdin", "Split", "Rijeka", "Dubrovnik"]
}
```
---
## POST requests with vue-resource
##### Register it in main.js
```javascript
import VueResource from 'vue-resource'

Vue.use(VueResource);
```
##### Usage in custom function 
```javascript
post: function () {
	this.$http.post("http://url", {
		title: this.blog.title,
		body: this.blog.body,
		userId: 1
	}).then( function ( res ){
	// promise
		console.log("Response: ", res)
	});
}
```
---
## GET requests
##### Usage in custom function
```javascript
post: function () {
	this.$http.get("http://url/").then( function ( res ){
		// promise
		console.log("Response: ", res)
	});
}
```
---
## Routes with vue-router
##### router.js
```javascript
import login from "./components/login.vue";
import registration from "./components/Registration.vue";
import user from "./components/user.vue";

export default [
  { path: "/", component: login },
  { path: "/registration", component: registration },
  { path: "/users/:id", component: user }
]
```
##### main.js
```javascript
import VueRouter from 'vue-router';
import Routes from "./routes";
Vue.use(VueRouter);

const router = new VueRouter({
  routes: Routes
});

new Vue({
  el: '#app',
  render: h => h(App),
  router: router
})

```
##### router-view is a component that renders the matched component for the given path
```html
<template>
    <router-view></router-view>
</template>
```
##### handling route parameters
##### user.vue
```vue
<template>
    <div id="user">
      <h1></h1>
      <div></div>
    </div>
</template>
<script>

  export default {
    data: function () {
      return {
        id: this.$route.params.id,
        user: {}
      }
    },

    created(){
      this.$http.get("http://url/user/" + this.id).then(function(res){
        this.user = res.body;
      });
    }

  }
</script>
```
##### navigating around
```html
<ul>
	<li><router-link to="/" exact>Home</router-link></li>
	<li><router-link to="/add" exact>Add user</router-link></li>
</ul>
```
---
## Mixins
##### Reuse some piece if code (or function) so that it doesn't need to be written in more separate files.
---
