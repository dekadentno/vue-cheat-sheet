# vue-cheat-sheet
My cheat sheet for vue.js most basic stuff
Sources:
* [iamshaunjp](https://github.com/iamshaunjp/vuejs-playlist)
* [Vue.js official guide](https://vuejs.org/v2/guide/)

Cool external libs:
* [axios](https://github.com/axios/axios) - promise based HTTP client
* [vue-router](https://router.vuejs.org/en/) - routing
* [vue-cli](https://github.com/vuejs/vue-cli) - CLI for scaffolding Vue.js projects
* [vue-resorce](https://github.com/pagekit/vue-resource) - web requests and handling responses
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
		<div id="vue-app">
			<p> {{ hello() }} </p>
			<p> {{ name }} </p>
			<p> {{ age + 1 }} </p>
			<p> {{ age < 18 ? "Youngster" : "Adult"}} </p>
		</div>

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
		hello: function () {
			return "Hello";
		},
	computed:{}
    }
});
```

## HTML directives  
##### Show / hide div
##### Hides the element (display none), doesn't delete it
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
##### Deletes the element, doesn't hide it
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

## Custom HTML directives
##### todo

## Two way data binding
```html
<input v-model="name" type="text" />
<p>My name is: {{name}}</p>
```
```javascript
...
data:{
	name: ""
}
...
```

## HTML properties and classes
```html
<p v-bind:style="{ property: value }">...</p>
```
this div will have the _red_ class if the _userFound_ variable is set to _true_
```html
<div v-bind:class="{ red: userFound }">...</div>
```

## Events
##### Call _method_ on click event
where _method_ is a custom method in the js
```html
<button v-on:click="method">Add</button>
```
##### or shorthand
where _method_ is a custom method in the js
```html
<button @click="method">Add</button>
```
_method_ is called when ALT+ENTER is pressed
```html
<input ref="name" v-on:keyuop.alt.enter="method" type="text" />
```

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

    data: function () {
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

    data: function () {
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


    data: function () {
      return {
        copyright: "Copyright 2017 "
      }
    }

  }

</script>
```

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

## Mixins
##### Reuse some piece if code (or function) so that it doesn't need to be written in more separate files.


## References
```html
<input ref="name" type="text" />
```
```javascript
var name = this.$refs.name;

```

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

## Vue CLI
##### make new project
```
$ vue init webpack-simple my-project
$ cd project-name
```
##### install dependencies and start local server
```
$ npm install
$ npm run dev
```
##### build app for production
this will make a dist folder with minified js
```
$ npm run build
```

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
## POST requests with vue-resource
##### Register it in main.js
```javascript
import VueResource from 'vue-resource'

Vue.use(VueResource);
```
##### Usage in custom function 
```javascript
post: function () {
	this.$http.post("http://localhost:3000/users", {
		title: this.blog.title,
		body: this.blog.body,
		userId: 1
	}).then( res => {
	// promise
		console.log("Response: ", res);
	}, error => {
		console.log("Error: ", error);
	});
}
```

## GET requests
##### Usage in custom function
```javascript
post: function () {
	this.$http.get("http://localhost:3000/users").then( function ( res ){
		// promise
		console.log("Response: ", res)
	});
}
```

## Routes with vue-router
```javascript
// router.js
import login from "./components/login.vue";
import registration from "./components/Registration.vue";
import user from "./components/user.vue";
```
```javascript
// main.js
import VueRouter from 'vue-router';
import { routes } from "./routes";
Vue.use(VueRouter);

const router = new VueRouter({
  routes
});

new Vue({
  el: '#app',
  router: router,
  render: h => h(App)  
})
```
```javascript
// routes.js
import Login from "./components/Login.vue";
import Registration from "./components/Registration.vue";
import User from "./components/User.vue";

export const routes = [
  { path: "", component: Login },
  { path: "/registration", component: Registration },
  { path: "/users/", component: Users, children: [
  	{ path: "", component: UserStart },
	{ path: ":id", component: UserDetail },
	{ path: ":id/edit", component: UserEdit }
  ] },
    {path: "*", redirect: "/"} // handle all uncovered routes 
  
]
```
##### mark the place with router-view where the component of the currently active route will be loaded
```html
<template>
    <router-view></router-view>
</template>
```
##### handling route parameters
```vue
<!-- user.vue -->
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
<ul class="nav">
	<router-link to="/" tag="li" active-class="active" exact><a>Home</a></router-link>
	<router-link to="/users" tag="li" active-class="active" ><a>Users</a></router-link>
</ul>
```
##### dynamically route over user details
```vue
<router-link v-bind:to='"/user/" + user.id' tag="li" v-for="(user, index) in users"> {{ user.username }}</router-link>
```
##### navigate home 
```javascript
this.#router.push({ path: "/home"});
```

##### watch for route changes 
```javascript
watch: {
      "$route": function (to, form){
        this.id = to.params.id
      }
}
```

## Stuff that might get handy
* _v-once_ - render the element and component only once
* _v-if_ - conditionally render the element
* [Difference between computed and methods](https://github.com/dekadentno/vue-cheat-sheet/blob/master/computedMethods.md)
* watch - specify what property to listen for changes and then execute some code without returning values
* v-model modifiers
	* .lazy - fire event when user lefts the field
	* .number - force the value to be converted to a integer
	* .trim - delete whitespace
