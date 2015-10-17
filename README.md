# refluxjs-aggregate-store-pattern

This is a pattern for creating aggregate stores in refluxjs.

* Parent store state has a property that references the child store state
* Parent store listens for child store trigger events
* Child passes entire state when triggering

```javascript
// Initial state
this.state = {
  child: ChildStore.state
};
...
// Child stores changes
onChildStoreEvent: function (newState) {
  this.state.child = newstate;
  this.trigger(this.state);
}
