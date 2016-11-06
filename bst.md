Binary Search Trees
-------------------

Binary Search Tree Property.
 Let y be a descendant of node x
  + if y is in the left subtree of x, then y.key <= x.key
  + if y is in the right subtree of x, then y.key >= x.key

Inorder Tree Walk (Recursive)
```python

def inorder_tree_walk(x):

	if x:
		inorder_tree_walk(x.left)
		print x.key
		inorder_tree_walk(x.right)

```

Tree Search (Recursive)
```python

def tree_search(x, K):

	if not x or K == x.key:
		return x

	elif K < x.key:
		tree_search(x.left, K)

	else:
		tree_search(x.right, K)
```

Iterative Tree Search
```python

def iterative_tree_search(x, K):
	
	while x and K != x.key:
		if K <= x.key:
			x = x.left
		else:
			x = x.right

	return x
```

Complete Binary Tree
 + All internal nodes have EXACTLY 2 children
 + All the leeaves are the same distance from the root


Tree Minimum
```python

def tree_min(x):

	while x.left:
		x = x.left
	
	return x
```

Tree Maximum
```python

def tree_max(x):

	while x.right:
		x = x.right

	return x
```

Inorder
 +  If a node x, is in the left subtree of another node y, then x ≺ y
 + If a node z, is in the right subtree of another node y, then y ≺ z

Tree Successor
 + The successor of a node is the next node in the inorder sequence

 Case I
 	x.right != NULL:
 		return TreeMin(x.right)

 Case II
 	x.right == NULL:
 		return closest ancestor y of x where x is in the left subtree of y



Tree Successor Code
```python

def tree_successor(x):
	
	if x.right:
		return tree_min(x.right)

	y = x.parent
	while y and x == y.right:
		x = y
		y = y.parent

	return y

```

Report in Range
```python

def tree_range_report(x, kmin, kmax):

	if x:
		if kmin <= x.key:
			tree_range_report(x.left, kmin, kmax)

		if kmin <= x.key and x.key <= kmax:
			print x.key

		if x.key <= kmax:
			tree_range_report(x.right, kmin, kmax)

```


Compute Tree Size
```python

def tree_compute_size(x):

	if x:
		tree_compute_size(x.left)
		tree_comput_size(x.right)
		x.size = 1

		if x.left:
			x.size += x.left.size

		if x.right:
			x.size += x.right.size
```

Count Nodes Greater Than or Equal To
```python

# TODO: Try this

```

Count Nodes Less Than or Equal To
```python

# TODO: Try this

```

Count Nodes in Range
```python

# TODO: Try this

```


## Binary Search Trees: Insertion


Locate Parent
```python

def locate_parent(T, z):	
	"""Return future parent of z in tree"""

	y = None
	x = T.root

	while x:
		y = x
		if z.key < x.key:
			x = x.left
		else:
			x = x.right

	return y
```

Tree Insert
```python

def tree_insert(T, z):

	y = locate_parent(T, z)
	z.parent = y

	if not y:
		T.root = z  # Tree was empty

	elif z.key < y.key:
		y.left = z
	else:
		y.right = z
```

Tree Insert & Update Size

```python

# TODO: try implementing this

```


## Binary Search Trees: Deletion

Case I.
Node z has zero children:
 + Delete z

Case II.
Node z hase one child:
 + Replace z with its child

Case III.
Node z has two children:
 + Replace z with it's successor y
 + Replace y with it's right child


### Excercize

 Delete node x from the following tree

     4
 3          20(x)
       09            42
     07  12        39  48
                 27
                   31
                 30  35


Case III
Node x has two children.
+ Replace x with it's successor y
  - successor is the tree min in the right tree
  - in this case, 27
+ Replace y with it's right child
  - the right child of y is 31


The new tree is then

     4
 3          27
       09            42
     07  12        39  48
                 31
               30  35


Transplant
```python

def transplant(T, u, v):
	"""Replace subtree w/root u, w subtree w/root v"""

	p = u.parent
	if not p:
		T.root = v

	elif u = p.left:
		p.left = v

	else:
		p.right = v

	if v:
		v.parent = p

```


Tree Delete
```python

def tree_delete(T, z):

	# Cover case I and II
	if not z.left:
		transplant(T, z, z.right)
	elif not z.right:
		transplant(T, z, z.left)

	# Cover case III
	else:
		# get successor
		# simple case, no need to call successor()
		y = TreeMin(z.right) 

		# replace y w/ it's right child
		if y != z.right:
			transplant(T, y, y.right)
			y.right = z.right
			y.right.parent = y

		# replace z w/successor y
		transplant(T, z, y)
```

#### Tree delete, update size

Update Size
```python
def update_size(T, z):
	
	while z:
		z.size = 1
		if z.left:
			z.size += z.left.size

		if z.right:
			z.size += z.right.size
```

Tree Delete with Update Size
```python
# TODO: implement this
```


## Balanced Search Trees