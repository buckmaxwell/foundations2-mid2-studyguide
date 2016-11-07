

# Red Black Trees

A *red-black tree* is a binary search tree with the following properties.

 + Every node is red or black
 + The root is black
 + Every leaf is NIL and is black
 + If a node is red, both it's children are black
 + For each node, all simple paths from the node to descendant leaves contain the same number of black nodes.

 NOTE: Every node in a binary tree is either a leaf or has *both* a left *and* right child.


### Theorem

A red-black tree with n internal nodes has a height at most 2log_2(n+1).

### Theorem 1

A complete binary search tree of height h has 2^(h+1) - 1 nodes.


## Red-Black Tree: Insert

RB Locate Parent
```python

def rb_locate_parent(T, z):

	parent = None
	x = T.root
	while not x.is_leaf():
		parent = x
		if z.key < x.key:
			x = x.left
		else:
			x = x.right

	return parent

```

RB Tree Insert
```python

def rb_tree_insert(T, z):
	
	fparent = rb_locate_parent(T, z)
	z.parent = parent

	if not y:
		T.root = z # Tree was empty

	elif z.key < parent.key:
		parent.left = z

	else:
		parent.right = z

	z.left = None #leaf
	z.right = None #leaf
	z.color = "Red"
	rb_insert_fixup(T, z)


```

### Insert Fixup Case 1
If the parent and uncle of z are Red
 + Color the parent of z Black
 + Color the uncle of z black
 + Color the grandparent of z Red
 + Repeat on the grandparent of z

Sibling
```python

def sibling(x):
	"""Return the sibling of x"""

	if not x.parent:
		raise Exception("Root has no siblings.")

	p = x.parent
	if p.left == x:
		return p.right
	else:
		return p.left
```

RB Insert Fixup A
```python

def rb_insert_fixup_a(T, z):
	
	while z != T.root and z.parent.color != "Black":
		uncle = sibling(z.parent)
		if uncle.color == "Black":
			return None

		z.parent.color = "Black"
		uncle.color = "Black"
		grandpa = z.parent.parent
		grandpa.color = "Red"
		z = grandpa

```

### Insert Fixup Case 3

If the parent of z is red and its uncle is black: If z is a left child and its parent is a left child.
 + Right Rotate on the grandparent of z
 + Color the parent of z Black
 + Color the sibling of z Red


RB Insert Fixup C
```python

def rb_insert_fixup_c(T, z):

	if z == T.root or z.parent.color == "Black":
		return None

	parent = z.parent
	grandp = parent.parent

	# Do this early to avoid redundant code
	parent.color = "Black"
	grandp.color = "Red"

	if z == parent.left and parent == grandp.left:
		right_rotate(T, granp)

	elif z == parent.right and parent == grandp.right:
		left_rotate(T, grandp)
```

### Insert Fixup Case 2

If the parent of z is red and its uncle is black: If z is a right child and it's parent is a left child
 + z = parent
 + Left Rotate on parent
 + Apply Algorithm for Case 3

RB Insert Fixup B
```python

def rb_insert_fixup_b(T, z):
	
	parent = z.parent
	grandp = parent.parent

	if z == parent.right and parent == granp.left:
		z = parent
		left_rotate(T,parent)

	elif z == parent.left and parent == grandp.right:
		z = parent
		right_rotate(T,parent)
```


### Insert Fixup

RB Insert Fixup
```python

def rb_insert_fixup(T, z):
	
	rb_insert_fixup_a(T, z)
	rb_insert_fixup_b(T, z)
	rb_insert_fixup_c(T, z)
	T.root.color = "Black"

```

























