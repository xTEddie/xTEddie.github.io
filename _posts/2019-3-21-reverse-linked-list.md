---
layout: post
title: Reverse Linked List
---

## Problem

Reverse a linked list.

For example, you were given:
```
	1 -> 2 -> 3 -> null
```

Then, the output would be:
```
	3 -> 2 -> 1 -> null
```

## Solution
We notice this is a **singly linked list** where every node has a reference to the next node. Our algorithm will have to be able to keep track of the previous node since its reference is not given. 

We will start off by having a variable to hold the reference of the current and previous node which will be updated in the **while loop** at every iteration. The while loop will run as long as the reference of the current node is not **null**. We will have a variable in the loop which temporarily holds the reference of the next node because we don't want to lose it once it gets replaced by the reference of the previous node. We update the reference of the previous node to the reference of the current node then the reference of current node to the reference of the next node to keep traversing the linked list. Finally, we return the new head of the reversed linked list which is basically the reference of the previous node.

```
def reverse_linked_list(head):
	
	if not head or not head.next:
		return head
	
	# Set previous node to be null by default
	prev_node, curr_node = None, head
	
	while curr_node:
		next_node = curr_node.next
		curr_node.next = prev_node
		prev_node = curr_node
		curr_node = next_node

	return prev_node
```

The time complexity is **O(n)** where **n** is the number of nodes because we are traversing every node from the linked list only once.

The space complexity is **O(1)** because no auxiliary space depending on the size of the input is needed.

