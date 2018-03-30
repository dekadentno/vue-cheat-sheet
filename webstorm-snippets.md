# Live templates

Custom snippets that generate pieces of code using a keyword + TAB.

##### post
```javascript
this.axios.post($PATH$).then(( res ) => {
  if ( !res.status == 200 ) {
    _wrn("Error: ", res.statusText);
    return
  }
  console.log(res.data);
}).catch(function ( error ) {
  _wrn(error);
  $END$
});
```

##### get
```javascript
this.axios.get($PATH$).then(( res ) => {
  if ( !res.status == 200 ) {
    _wrn("Error: ", res.statusText);
    return
  }
  console.log(res.data);
}).catch(function ( error ) {
  _wrn(error);
  $END$
});
```

##### itar
```javascript
for (var $INDEX$ = 0; $INDEX$ < $ARRAY$.length; $INDEX$++) {
  $END$
}
```

##### div.test
```javascript
 <div class="test">
 </div>
```

##### div#test
```javascript
<div id="test">
</div>
```

##### asdf
```javascript
console.log('$BLA$');
```
