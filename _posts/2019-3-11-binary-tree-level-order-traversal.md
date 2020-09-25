---
layout: post
title: Binary Tree Level Order Traversal
---

## Problem

You are given a binary tree, return the level order traversal of its nodes' values.

For example, if you were given a binary tree:

```
    1
   / \
  2   3
     / \
    4   5
```

Then, the tree level order traversal would be:

```
	[
		[1],
		[2,3],
		[4,5]
	]
```

## Solution
First thing we notice is that a **variation of BFS** will be required to solve this problem. We see from the output that nodes of the same level are grouped together in the same list. We will have to keep track the size of the nodes at every level in some way. 

The solution would be to use a queue to perform **BFS** iteratively. The queue is used to keep track of the nodes to traverse next.
We start off by having a queue with the root of the tree. Our algorithm will run as long as the queue is not empty. We know the current size of the queue represents the number of nodes from the previous level of the tree. We can use that value to dequeue all the nodes from the previous level to add them in a list. This list will then be added in the output once it contains every node from the previous level of the tree.
```
def level_order_traversal(root):
		output = []
		
		if not root:
				return output
	
		# Queue with root
		queue = collections.deque([root])
	
		while queue:
				# Get current size of the queue
				size = len(queue)
				level = []
				# Traverse nodes on every level
				for _ in range(size):
						node = queue.popleft()
						level.append(node.val)
						if node.left:
								queue.append(node.left)
						if node.right:
								queue.append(node.right)
				output.append(level)
		return output
```

The time complexity is **O(n)** where **n** is the number of nodes in the tree because we are traversing every node once even though we have a for loop inside a while loop.

The space complexity is **O(n)** where **n** is the number of nodes in the tree because of the output and we have a queue to track all the nodes.