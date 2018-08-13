CHALLENGE: The code editor provides an action creator called addMessage(). Write the function mapDispatchToProps() that takes dispatch as an argument, then returns an object. The object should have a property submitNewMessage set to the dispatch function, which takes a parameter for the new message to add when it dispatches addMessage().

SOLUTION: 
```javascript
const addMessage = (message) => {
  return {
    type: 'ADD',
    message: message
  }
};

// change code below this line
function mapDispatchToProps(dispatch){
    return {submitNewMessage: function(newMessage){ dispatch(addMessage(newMessage));}}}
