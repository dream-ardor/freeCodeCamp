CHALLENGE: First create a buffer that is 64-bytes. Then create a Int32Array typed array with a view of it called i32View.

MY CODE:
```javascript
var buffer = new ArrayBuffer(64);
var i32View = new Int32Array(buffer);
```
