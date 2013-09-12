# Storage

This  interface to localStorage and sessionStorage that adds expiration dates. To use it simply request a key and provide an expiration date and you will receive an object that you can extend with JSONable properties. Call the `save` method on the object it provides to save your data to localStorage or sessionStorage.

The default expiration date is one year from the time the item is requested. Expired keys will be deleted on the next page load.

Storage.js can be used with AMD loaders (requirejs), CommonJS, or with the storagejs global.

## Basic Usage

```javascript	
var storageObject = storagejs.get( 'foo' );
console.log(storageObject) // { "save": function(){...}, "safeSave": function(){...} }

storageObject.data = 'bar';
console.log(storageObject); // { "data":"bar", "save": function(){...}, "safeSave": function(){...} }

var oneWeekFromNow = new Date().getTime() + (1000 * 60 * 60 * 24 * 7);
storageObject.save( oneWeekFromNow );
```

Then, after a reload:

```javascript
var storageObject = storagejs.get( 'foo' );
console.log(storageObject) // { "data":"bar", "save": function(){...}, "safeSave": function(){...} }
```

## Storage Module Methods

* `storagejs.get( key /*, expirationDate */ )` - gets an object from localStorage. expirationDate will only be used if one is not passed into `save`.
* `storagejs.getSession( key, expirationDate )` - gets an object from sessionStorage

## Storage Objects

* `storageObject.save( expirationDate )` - saves the data on this storage object to localStorage or sessionStorage. If `expirationDate` is not provided it will use the value passed into the `get` function or default to one year.
* `storageObject.safeSave( expirationDate )` - wraps save in a try/catch, in case storage is full. Returns true on success, false on failure.

