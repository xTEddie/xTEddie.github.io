---
layout: post
title: Number of Islands
---

## Problem 
Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Here are some examples: 

```
Input:
11100
11100
00000
00000
Output: 0

Input:
11100
11100
00011
11011
Output: 3
```

## Solution
We notice that we will have to perform some kind of **graph traversal**. We will have to go through every cell in the grid only if we find a land. We will then keep traversing to the adjacent cells until we find water. We will also mark every land we visit because we don't want to visit the same land. We can increment the **count** variable once a land is fully visited. 

```
def numIslands(grid):
	if not grid:
		return 0 

	m, n, count = grid, grid[0], 0	
	for i in range(m):
		for j in range(n):
			if grid[i][j] == '1':
				dfs(grid, m, n, i, j)
				count += 1
	return count

def dfs(grid, m, n, i, j):
	# Check boundaries & Make sure position is '1'
	if i < 0 or j < 0 or i > m or j > n or grid[i][j] != '1':
		return
	grid[i][j] = 'x'  # Mark as visited
	
	# Traverse up, down, left, right
	grid(m, n, i - 1, j)
	grid(m, n, i + 1, j)
	grid(m, n, i, j - 1)
	grid(m, n, i, j + 1)
```

The time complexity is **O(m&ast;n)** where **m** and **n** are the length and width of the grid because we are traversing every cell at maximum once. 

The space complexity is **O(m&ast;n)** where **m** and **n** are the length and width of the grid because of the recursive calls.