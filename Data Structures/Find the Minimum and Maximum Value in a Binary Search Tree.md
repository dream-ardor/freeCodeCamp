Data Structures: Find the Minimum and Maximum Value in a Binary Search Tree

This series of challenges will introduce the tree data structure. Trees are an important and versatile data structure in computer science. Of course, their name comes from the fact that when visualized they look much like the trees we are familiar with in the natural world. A tree data structure begins with one node, typically referred to as the root, and from here branches out to additional nodes, each of which may have more child nodes, and so on and so forth. The data structure is usually visualized with the root node at the top; you can think of it as a natural tree flipped upside down.

First, let's describe some common terminology we will encounter with trees. The root node is the top of the tree. Data points in the tree are called nodes. Nodes with branches leading to other nodes are referred to as the parent of the node the branch leads to (the child). Other more complicated familial terms apply as you might expect. A subtree refers to all the descendants of a particular node, branches may be referred to as edges, and leaf nodes are nodes at the end of the tree that have no children. Finally, note that trees are inherently recursive data structures. That is, any children of a node are parents of their own subtree, and so on. The recursive nature of trees is important to understand when designing algorithms for common tree operations.

To begin, we will discuss a particular type of a tree, the binary tree. In fact, we will actually discuss a particular binary tree, a binary search tree. Let's describe what this means. While the tree data structure can have any number of branches at a single node, a binary tree can only have two branches for every node. Furthermore, a binary search tree is ordered with respect to the child subtrees, such that the value of each node in the left subtree is less than or equal to the value of the parent node, and the value of each node in the right subtree is greater than or equal to the value of the parent node. It's very helpful to visualize this relationship in order to understand it better:

Now this ordered relationship is very easy to see. Note that every value to the left of 8, the root node, is less than 8, and every value to the right is greater than 8. Also notice that this relationship applies to each of the subtrees as well. For example, the first left child is a subtree. 3 is the parent node, and it has exactly two child nodes — by the rules governing binary search trees, we know without even looking that the left child of this node (and any of its children) will be less than 3, and the right child (and any of its children) will be greater than 3 (but also less than the structure's root value), and so on.

Binary search trees are very common and useful data structures because they provide logarithmic time in the average case for several common operations such as lookup, insertion, and deletion.

**Instructions:** We'll start simple. We've defined the skeleton of a binary search tree structure here in addition to a function to create nodes for our tree. Observe that each node may have a left and right value. These will be assigned child subtrees if they exist. In our binary search tree, define two methods, findMin and findMax. These methods should return the minimum and maximum value held in the binary search tree (don't worry about adding values to the tree for now, we have added some in the background). If you get stuck, reflect on the invariant that must be true for binary search trees: each left subtree is less than or equal to its parent and each right subtree is greater than or equal to its parent. Let's also say that our tree can only store integer values. If the tree is empty, either method should return null.

**Solution:**
```js
var displayTree = tree => console.log(JSON.stringify(tree, null, 2));

function Node(value) {
	this.value = value;
	this.left = null;
	this.right = null;
}

function BinarySearchTree() {
	this.root = null;
	this.findMin = function() {
		// Empty tree.
		if (!this.root) {
			return null;
		}
		let currentNode = this.root;
		while (currentNode.left) {
			currentNode = currentNode.left;
		}
		return currentNode.value;
	};
	this.findMax = function() {
		// Empty tree.
		if (!this.root) {
			return null;
		}
		let currentNode = this.root;
		while (currentNode.right) {
			currentNode = currentNode.right;
		}
		return currentNode.value;
	};
	this.add = function(value) {
		// Empty tree.
		if (!this.root) {
			this.root = new Node(value);
			return undefined;
		}
		return this.addNode(this.root, value);
	};
	this.addNode = function(node, value) {
		// Check if value already exists.
		if (node.value === value) return null;
		if (value < node.value) {
			if (node.left) {
				return this.addNode(node.left, value);
			} else {
				node.left = new Node(value);
				return undefined;
			}
		} else {
			if (node.right) {
				return this.addNode(node.right, value);
			} else {
				node.right = new Node(value);
				return undefined;
			}
		}
	};
	this.isPresent = function(value) {
		if (!this.root) {
			return null;
		}
		return this.isNodePresent(this.root, value);
	};
	this.isNodePresent = function(node, value) {
		if (node.value === value) return true;
		if (value < node.value) {
			return node.left ? this.isNodePresent(node.left, value) : false;
		} else {
			return node.right ? this.isNodePresent(node.right, value) : false;
		}
		return false;
	};
	this.findMinHeight = function() {
		if (!this.root) {
			return -1;
		}
		let heights = {};
		let height = 0;
		this.traverseTree(this.root, height, heights);
		return Math.min(...Object.keys(heights));
	};
	this.findMaxHeight = function() {
		if (!this.root) {
			return -1;
		}
		let heights = {};
		let height = 0;
		this.traverseTree(this.root, height, heights);
		return Math.max(...Object.keys(heights));
	};
	this.traverseTree = function(node, height, heights) {
		if (node.left === null && node.right === null) {
			return (heights[height] = true);
		}
		if (node.left) {
			this.traverseTree(node.left, height + 1, heights);
		}
		if (node.right) {
			this.traverseTree(node.right, height + 1, heights);
		}
	};
	this.isBalanced = function() {
		return this.findMaxHeight() > this.findMinHeight() + 1;
	};
	// DFS tree traversal.
	this.inorder = function() {
		if (!this.root) return null;
		let result = [];

		function traverseInOrder(node) {
			if (node.left) traverseInOrder(node.left);
			result.push(node.value);
			if (node.right) traverseInOrder(node.right);
		}
		traverseInOrder(this.root);
		return result;
	};
	this.preorder = function() {
		if (!this.root) return null;
		let result = [];

		function traverseInOrder(node) {
			result.push(node.value);
			if (node.left) traverseInOrder(node.left);
			if (node.right) traverseInOrder(node.right);
		}
		traverseInOrder(this.root);
		return result;
	};
	this.postorder = function() {
		if (!this.root) return null;
		let result = [];

		function traverseInOrder(node) {
			if (node.left) traverseInOrder(node.left);
			if (node.right) traverseInOrder(node.right);
			result.push(node.value);
		}
		traverseInOrder(this.root);
		return result;
	};
	// BFS tree traversal.
	this.levelOrder = function() {
		if (!this.root) return null;
		let queue = [this.root];
		let result = [];
		while (queue.length) {
			let node = queue.shift();
			result.push(node.value);
			if (node.left) queue.push(node.left);
			if (node.right) queue.push(node.right);
		}
		return result;
	};
	this.reverseLevelOrder = function() {
		if (!this.root) return null;
		let queue = [this.root];
		let result = [];
		while (queue.length) {
			let node = queue.shift();
			result.push(node.value);
			if (node.right) queue.push(node.right);
			if (node.left) queue.push(node.left);
		}
		return result;
	};
	// Delete a leaf node.
}
let bst = new BinarySearchTree();
```
