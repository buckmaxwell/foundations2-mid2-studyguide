
# Midterm Sample, student work

## 1.  (Heaps and Data Structure Analysis)

 + original = [55,47,26,33,42,24,17,31,14,38,16,11,20,1,5,12,23,13,8,19,6,3,2,4,7,15]

 + remove max element and set to max_key
	- max_key = 55

 + make last element the first element
	- A = [15,47, 26,33,42,24,17,31,14,38,16,11,20,1,5,12,23,13,8,19,6,3,2,4,7]

 + now max_heapify the result
```
	j = 1
	done = False

	while not done:
		
		l = left(j)
		r = right(j)
		largest = j

		if l <= len(A) and A[l] > A[largest]:
			largest = l 
		if r <= len(A) and A[r] > A[largest]:
			largest = r # true
		if j != largest:
			A[largest], A[j] = A[j], A[largest]
		else:
			done = True
		j = largest

	[15,47,26,33,42,24,17,31,14,38,16,11,20,1,5,12,23,13,8,19,6,3,2,4,7]

	  1  2  3  4  5
	[47,15,26,33,42,24,17,31,14,38,16,11,20,1,5,12,23,13,8,19,6,3,2,4,7]

	  1  2  3  4  5  6  7  8  9 10 11 
	[47,42,26,33,15,24,17,31,14,38,16,11,20,1,5,12,23,13,8,19,6,3,2,4,7]

	  1  2  3  4  5  6  7  8  9 10 11 12 131415 16 17 
	[47,42,26,33,38,24,17,31,14,15,16,11,20,1,5,12,23,13,8,19,6,3,2,4,7]
	1819202122

	  1  2  3  4  5  6  7  8  9 10 11 
	[47,42,26,33,38,24,17,31,14,19,16,11,20,1,5,12,23,13,8,15,6,3,2,4,7]

	                      47
	          42                       26
	     33          38          24          17
	  31    14    19    16    11    20    01    05
	12 23 13 08 15 06 03 02 04 07
```

GOOD WORK


## 2. (Binary Search Trees)

### (a) Describe the algorithm to delete a node x from a binary search tree. (Describe just the five or six major steps in the algorithm)

Case 1 -- x has no children
 + delete x

Case 2 -- x has 1 child
 + replace x with x's child

Case 3 -- x has 2 children
 + replace x with the successor of x, y which will be tree_min(x.right)
 + replace y with y.right

### (b)Give asymptotic bounds on the worst case running time of the algorithm in terms of the number of nodes and/or height of the tree.  Give bounds which are as tight and precise as possible.

This will run in log(n) time.  In the worst case, the node replaced is the the root node, and has both left and right subtrees.  In this case, the deleted node will be replaced with it's successor -- the tree_min of the right subtree.  The running time of tree_min in the average case is log(n), but in the worst case, could be n -- if the tree is not well balanced.  Of course since there are at least 2 other nodes (the root and the left subtree), the worst case of our algorithm is n-2 + c, but that simplifies to n, leaving our worst case runtime as THETA(n).

If the height of our tree is h, the worst case running time is THETA(h)


Tree Delete
```python

def tree_delete(T, z):

	# Cover case I and II
	if not z.left:
		transplant(T, z, z.right)  # constant time
	elif not z.right:
		transplant(T, z, z.left)   # constant time

	# Cover case III
	else:
		# get successor
		# simple case, no need to call successor()
		y = TreeMin(z.right)   # h time, where h is tree height

		# replace y w/ it's right child
		if y != z.right:
			transplant(T, y, y.right) # constant time
			y.right = z.right   # constant time
			y.right.parent = y  # constant time

		# replace z w/successor y
		transplant(T, z, y)     # constant time
```


## 3. (Red Black Trees)

Apply RBTreeInsert to insert 18 in the following red-black tree and draw the resulting binary tree.
Indicate which nodes are red or black in your drawing.  Be sure that the resulting tree has all the properties of a red-black tree.  SHOW YOUR WORK.



























