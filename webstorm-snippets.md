# Live templates

Custom snippets that generate pieces of code using a keyword + TAB.

##### post
```javascript
this.$http.post($PATH$, {
  name: this.name
}).then(res => {
  console.log("Response: ", res);
}, error => {
  console.log("API Error: ", error);
});
```

##### get
```javascript
this.$http.get($PATH$).then(function ( res ) {
  console.log("Response: ", res.body);
    $END$
});
```

##### itar
```javascript
for (var $INDEX$ = 0; $INDEX$ < $ARRAY$.length; $INDEX$++) {
  $END$
}
```
