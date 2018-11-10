CHALLENGE: Here we have a stack of homework assignments represented as an array: "BIO12" is at the base, and "PSY44" is at the top of the stack.

Modify the given array and treat it like a stack using the JavaScript methods mentioned above (pop and push). Remove the top element "PSY44" from the stack. Then add "CS50" to be the new top element of the stack.

MY CODE:
```javascript
var homeworkStack = ["BIO12","HIS80","MAT122","PSY44"];

homeworkStack.pop()
homeworkStack.push("CS50")
