**Data Structures: Remove an Element from a Max Heap**

Now that we can add elements to our heap let's see how we can remove elements. Removing and inserting elements both require similar logic. In a max heap you will usually want to remove the greatest value, so this involves simply extracting it from the root of our tree. This will break the heap property of our tree, so we must reestablish it in some way. Typically, for a max heap this is done in the following way:

Move the last element in the heap into the root position.

If either child of the root is greater than it, swap the root with the child of greater value.

Continue swapping until the parent is greater than both children, or you reach the last level in the tree.

**Instructions:** Add a method to our max heap called remove. This method should return the greatest value that has been added to our max heap and remove it from the heap. It should also reorder the heap so the heap property is maintained. After removing an element, the next greatest element remaining in the heap should become the root. Add your insert method again here as well.

**Solution:**
```js
let MaxHeap = function() {
	let heap = [null];
	this.print = () => heap;
	this.insert = function(num) {
		heap.push(num);
		if (heap.length > 2) {
			let idx = heap.length - 1;
			while (heap[idx] > heap[Math.floor(idx / 2)]) {
				if (idx >= 1) {
					[heap[Math.floor(idx / 2)], heap[idx]] = [heap[idx], heap[Math.floor(idx / 2)]];
					if (Math.floor(idx / 2) > 1) {
						idx = Math.floor(idx / 2);
					} else {
						break;
					};
				};
			};
		};
	};
	this.remove = function() {
		let smallest = heap[1];
		if (heap.length > 2) {
			heap[1] = heap[heap.length - 1];
			heap.splice(heap.length - 1);
			if (heap.length == 3) {
				if (heap[1] < heap[2]) {
					[heap[1], heap[2]] = [heap[2], heap[1]];
				};
				return smallest;
			};
			let i = 1;
			let left = 2 * i;
			let right = 2 * i + 1;
			while (heap[i] <= heap[left] || heap[i] <= heap[right]) {
				if (heap[left] > heap[right]) {
					[heap[i], heap[left]] = [heap[left], heap[i]];
					i = 2 * i
				} else {
					[heap[i], heap[right]] = [heap[right], heap[i]];
					i = 2 * i + 1;
				};
				left = 2 * i;
				right = 2 * i + 1;
				if (heap[left] == undefined || heap[right] == undefined) {
					break;
				};
			};
		} else if (heap.length == 2) {
			heap.splice(1, 1);
		} else {
			return null;
		};
		return smallest;
	};
};
```
