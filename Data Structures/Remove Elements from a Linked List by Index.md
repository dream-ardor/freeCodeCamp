**Data Structures: Remove Elements from a Linked List by Index**

Before we move on to another data structure, let's get a couple of last bits of practice with linked lists.

Let's write a removeAt method that removes the element at a given index. The method should be called removeAt(index). To remove an element at a certain index, we'll need to keep a running count of each node as we move along the linked list.

A common technique used to iterate through the elements of a linked list involves a 'runner', or sentinel, that 'points' at the nodes that your code is comparing. In our case, starting at the head of our list, we start with a currentIndex variable that starts at 0. The currentIndex should increment by one for each node we pass.

Just like our remove(element) method, we need to be careful not to orphan the rest of our list when we remove the node in our removeAt(index) method. We keep our nodes contiguous by making sure that the node that has reference to the removed node has a reference to the next node.

* Write a removeAt(index) method that removes and returns a node at a given index. The method should return null if the given index is either negative, or greater than or equal to the length of the linked list.

Note: Remember to keep count of the currentIndex.

**Solution:**
```js
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
