CHALLENGE: Compare two arrays and return a new array with any items only found in one of the two given arrays, but not both. In other words, return the symmetric difference of the two arrays.

SOLUTION: 
```javascript
function diffArray(arr1, arr2) {
  return arr1
    .concat(arr2)
    .filter(
        item => !arr1.includes(item) || !arr2.includes(item)
    )
}
}
```
COMMENTS: Okay, so what's going on here? Well, first we are using ".concat" to combine arr1 and arr2 into a single array. Then we are using the "filter" method to create a new array which passes the tests of the implemented function. The test here uses arrow functions to check if an item exists in either arr1 or arr2. Any number which exists in only one, but does not exist in both arrays is returned.

EXAMPLE: ```diffArray([1, 2, 3, 5], [1, 2, 3, 4, 5])``` returns [4] because 4 exists only in the second array.
