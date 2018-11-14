**CHALLENGE**: Create a function that takes a single (numeric) argument and returns another function that is an accumulator. The returned accumulator function in turn also takes a single numeric argument, and returns the sum of all the numeric values passed in so far to that accumulator (including the initial value passed when the accumulator was created).

Rules:
Do not use global variables.

Hint:
Closures save outer state.

**SOLUTION**:
```javascript
function accumulator (sum) {
 return function(n) {
  return sum += n
 } 
}
```
