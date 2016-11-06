# Heaps

## Priority Queues

Operations
 + D.Init()
 + D.Insert(x)
 + D.ExtractMax(x)

## (Max) Heap

Array Representation
	[48, 42, 23, 17, 39, 20, 9, 12, 8, 34, 31, 14]
	  1   2   3   4   5   6  7   8  9  10  11  12

Tree
```
                                 48
                            42         23
                         17    39   20    9
                        12 8 34 31 14 
```
## Nearly Complete Binary Tree

Only nodes on the bottom right of tree are missing

Functions:
```python
def parent(i):
	"""i is the array/heap position, idx frm 1"""

	return i/2

def left(i):
	"""i is the array/heap position, idx frm 1"""

	return 2*i

def right(i):
	"""i is the array/heap position, idx frm 1"""

	return 2*i + 1
```


Max Heap Insertion
```python

def max_heap_insert(A, K):
	"""Array A of elements, Key K"""

	A.append(K)
	i = len(A)
	while (i > 1) and A[parent(i)] < A[i]):
		Swap(A[i], A[parent(i)])
		i = parent(i)

```

Extract Heap Max
```python

def heap_extract_max(A):
	"""Array A of elements"""

	if not len(A):
		raise Exception("Heap Underflow")

	max_key = A[0]
	A[0] = A[len(A)]
	MaxHeapify(A)
	return max_key
```

Max Heapify
```python

def max_heapify(A):
	"""Array A of elements"""

	flag_done = False;
	j = 0
	while not flag_done:
		l = left(j)
		r = right(j)
		largest = j

		if l <= len(A) and A[l] > A[largest]:
			largest = l
		if r <= len(A) and A[r] > A[largest]:
			largest = r
		if j != largest:
			a[j], a[largest] = A[largest], A[j]
		else:
			flag_done = True
		j = largest

```


Heap Increase Key
```python

def max_heap_increase_key(A, i, K):
	"""Array A of elements, index i, Key K"""

	if K < A[i]:
		raise Exception("New key is less than current key")

	A[i] = K

	while i > 1 and A[parent(i)] < A[i]:
		A[i], A[parent(i)] = A[parent(i)], A[i]
		i = parent(i)

```

Heap Sort
```python

def heap_sort(B):
	"""Array B of elements"""

	size = 0
	for e in B:
		max_heap_insert(A, e)

	for i, e in enumerate(reversed(B)):
		B[i] = heap_extract_max(A)

```
