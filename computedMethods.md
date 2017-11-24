## Computed methods
> Computed properties are cached, and only re-computed on reactive dependency changes. Note that if a certain dependency is out of the instance’s scope (i.e. not reactive), the computed property will not be updated.

```html
<html>
<head>
    <meta charset="utf8">
    <title>VueJS example</title>
    <script src="https://cdn.jsdelivr.net/npm/vue"></script>
</head>

<body>
<div id="vue-app">
    <button v-on:click="a++">Counter 1++</button>
    <button v-on:click="a--">Counter 1--</button>
    <button v-on:click="b++">Counter 2++</button>
    <p>Counter 1: {{ a }}</p>
    <p>Counter 2: {{ b }}</p>
    <!--The result() method is invoked whenever the Counter 1 button is clicker or the Counter 2 button is clicked-->
    <!--The output() method is invoked only when the Counter 2 button is clicked-->
    <p>Result: {{ result() }} | {{ output }}</p>

</div>

<script src="main.js"></script>
</body>
</html>
```

```javascript
new Vue({
    el: '#vue-app',
    data: {
        a: 0,
        b: 0
    },
    methods: {
        result: function () {
            // this function is not interested in the "b" variable, yet it runs every time when the result needs to be changed
            console.log("methods");
            return this.a < 0 ? "Negative" : "Positive";
        }
    },
    computed: {
        // these methods are invoked like attributes, without ()
        // this method runs only when the "a" variable is changed
        output: function () {
            console.log("computed");
            return this.a < 0 ? "Negative" : "Positive";
        }
    }
});
```
