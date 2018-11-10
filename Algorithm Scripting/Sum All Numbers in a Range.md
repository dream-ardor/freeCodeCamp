CHALLENGE: We'll pass you an array of two numbers. Return the sum of those two numbers plus the sum of all the numbers between them.

The lowest number will not always come first.

SOLUTION:
```javascript
function sumAll(arr) {
return (arr[0]+arr[1])*(Math.max(...arr)-Math.min(...arr)+1)/2;;
}

//sumAll([1, 4]) returns 10//
```
