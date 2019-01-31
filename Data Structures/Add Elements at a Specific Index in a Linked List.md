Data Structures: Add Elements at a Specific Index in a Linked List

Let's create a addAt(index,element) method that adds an element at a given index.

Just like how we remove elements at a given index, we need to keep track of the currentIndex as we traverse the linked list. When the currentIndex matches the given index, we would need to reassign the previous node's next property to reference the new added node. And the new node should reference the next node in the currentIndex.

Returning to the conga line example, a new person wants to join the line, but he wants to join in the middle. You are in the middle of the line, so you take your hands off of the person ahead of you. The new person walks over and puts his hands on the person you once had hands on, and you now have your hands on the new person.

**Instructions:**

Create an addAt(index,element) method that adds an element at a given index. Return false if an element was unable to be added.

Note: Remember to check if the given index is a negative or is longer than the length of the linked list.

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
