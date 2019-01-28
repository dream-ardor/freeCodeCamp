**Data Structures: Search within a Linked List**

Let's add a few more useful methods to our linked list class. Wouldn't it be useful if we could tell if our list was empty or not, as with our Stack and Queue classes?

We should also be able to find specific elements in our linked list. Traversing through data structures is something you'll want to get a lot of practice with! Let's create an indexOf method that takes an element as an argument, and returns that element's index in the linked list. If the element is not found in the linked list, return -1.

Let's also implement a method that does the opposite: an elementAt method that takes an index as an argument and returns the element at the given index. If no element is found, return undefined.

* Write an isEmpty method that checks if the linked list is empty, an indexOf method that returns the index of a given element, and an elementAt that returns an element at a given index.

**Solution:**
```javascript
function LinkedList() {
	var length = 0;
	var head = null;
	var Node = function(element) {
		this.element = element;
		this.next = null;
	};
	this.size = function() {
		return length;
	};
	this.head = function() {
		return head;
	};
	this.add = function(element) {
		var node = new Node(element);
		if (head === null) {
			head = node;
		} else {
			var currentNode = head;
			while (currentNode.next) {
				currentNode = currentNode.next;
			}
			currentNode.next = node;
		}
		length++;
	};
	this.remove = function(element) {
		var currentNode = head;
		var previousNode;
		if (currentNode.element === element) {
			head = currentNode.next;
		} else {
			while (currentNode.element !== element) {
				previousNode = currentNode;
				currentNode = currentNode.next;
			}
			previousNode.next = currentNode.next;
		}
		length--;
	};
	this.isEmpty = function() {
		return length === 0;
	};
	this.indexOf = function(element) {
		var currentNode = head;
		var index = -1;
		while (currentNode) {
			index++;
			if (currentNode.element === element) {
				return index;
			}
			currentNode = currentNode.next;
		}
		return -1;
	};
	this.elementAt = function(index) {
		var currentNode = head;
		var count = 0;
		while (count < index) {
			count++;
			currentNode = currentNode.next
		}
		return currentNode.element;
	};
	this.addAt = function(index, element) {
		var node = new Node(element);
		var currentNode = head;
		var previousNode;
		var currentIndex = 0;
		if (index > length) {
			return false;
		}
		if (index === 0) {
			node.next = currentNode;
			head = node;
		} else {
			while (currentIndex < index) {
				currentIndex++;
				previousNode = currentNode;
				currentNode = currentNode.next;
			}
			node.next = currentNode;
			previousNode.next = node;
		}
		length++;
	}
	this.removeAt = function(index) {
		var currentNode = head;
		var previousNode;
		var currentIndex = 0;
		if (index < 0 || index >= length) {
			return null
		}
		if (index === 0) {
			head = currentNode.next;
		} else {
			while (currentIndex < index) {
				currentIndex++;
				previousNode = currentNode;
				currentNode = currentNode.next;
			}
			previousNode.next = currentNode.next
		}
		length--;
		return currentNode.element;
	}
}
```
