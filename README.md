# refluxjs-aggregate-store-pattern

This is a pattern for creating aggregate stores in refluxjs.

* Parent store state has a property that references the child store state
* Parent store listens for child store trigger events
* Child passes entire state when triggering

```javascript
var ParentStore = Reflux.createStore({

  init: function () {
    // Initial state
    this.state = {
      child: ChildStore.state
    };
    
    this.listenTo(ChildStore, this.onChildStoreEvent);
  },

  // Child stores changes
  onChildStoreEvent: function (newState) {
    this.state.child = newstate;
    this.trigger(this.state);
  }
  
});

var ChildStore = Reflux.createStore({
  listenables: ChildActions, // ChildActions.changeFoo is an action
  
  init: function () {
    this.state = {
      foo: ''
    };
  }
  
  onChangeFoo: function (newFoo) {
    this.state.foo = newFoo;
    this.trigger(this.state);
  }
  
});
```

## Example
[Shopping cart example](http://codepen.io/anon/pen/xwPEMe?editors=001#0)
