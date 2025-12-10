The main way to determine algorithm efficiency:
- *Complexity*
	1.Runtime
	2.Memory usage
***Computation complexity*** is the amount of resources used by the algorithm.

***Runtime complexity*** is a function *T(N)
- The number of constant time operations performed by input size N.
*Tips*: Complexity analysis always treats the input data size as a variable.

***Space complexity*** is a function *S(N)*
- The number of fixed-sized memory units used by input size N.

***Constant time operations***
	1. Statements x = 10, y = 20, a = 1000, and b = 2000 assign values to fixed-size integer variables. Each assignment is a constant time operation.
	2. A CPU multiplies values 10 and 20 at the same speed as 1000 and 2000. Multiplication of fixed-size integers is a constant time operation.
	3. A loop that iterates x times, adding y to a sum each iteration, will take longer if x is larger. The loop is not constant time.

***Common constant time operations***
- Addition, subtraction, multiplication, and division of fixed size integer or floating point values.
- Assignment of a reference, pointer, or other fixed size data value.
- Comparison of two fixed size data values.
- Read or writ an array element at a particular index

***Big O notation***
- *Big O* notation is a mathematical way of describing how a function (running time, or runtime, of an algorithm) behaves in relation to the input size.

***The rules for determining Big O notation of composite functions***
*Big O computation*![[Big_O_Computation.png]]

***Binary search algorithm***
- The list's elements should be sorted and directly accessible.
- Binary search first check the middle element of the list.
- If the search key is not found, the algorithm will repeats search on left or right remaining sides, depending on the search key values.
***Binary search algorithm achievement by python :***
```python
def binary_search(numbers, key):
	#define two pointers
	low = 0
	high = len(numbers) - 1
	
	while low <= high:
		mid = (high+low)//2
		if numbers[mid] < key:
			low = mid + 1 
		elif numbers[mid] > key:
			high = mid - 1	
		else:
			return mid
	
	return -1
```

# ***Sorting***

***Bubble Sorting***
```python
def Bubble_Sort(numbers, numberSize):
	for i in range(numberSize - 1):
		for j in range (0, numberSize - 1 - j):
			if numbers[j] > numbers[j+1]:
				temp = numbers[j]
				numbers[j] = numbers[j+1]
				numbers[j+1] = temp 
	return numbers
```

***Selection sort***
```python
def Selection_sort(numbers):
	for i in range(len(numbers)-1):
		smallest_index = i
		for j in range(i + 1, len(numbers)):
			if numbers[smallest_index] > numbers [j]:
				smallest_index = j
		#swap numbers[i] and numbers[smallest_index]	
		temp = numbers[i]
		numbers[i] = numbers[smallest_index]
		numbers[smallest_index] = temp
	return numbers	
```
*Tip*: The inner loop is finding the smallest element, and the outer loop is swapping values.

***Insertion sort***
```python
def Insertion_sort(numbers):
	for i in range(1, len(numbers)):
		j = i
		while j > 0 and numbers[j] < numbers[j-1]:
			temp = numbers[j]
			numbers[j] = numbers[j-1]
			numbers[j-1] = temp
			j = j - 1
	return numbers 
```
*Tip*: Insertion sort is a sorting algorithm that treats the input as two parts, sorted and unsorted, and repeatedly inserts the next value from the unsorted part into the correct location in the sorted part.

***Merge sort***
```python
def merge(numbers, i, j, k):
	merged_size = k - i + 1
	merged_numbers = [] #used to stored the merged numbers
	for l in range(merged_size):
		merged_numbers.append(0) # Initialized numbers to zero
	merge_pos = 0
	# using double pointers to detect
	left_pos = i
	right_pos = j + 1
	while left_pos <= j and right_pos <= k:
		if numbers[left_pos] <= numbers[right_pos]:
			merged_numbers[merge_pos] = numbers[left_pos]
			left_pos = left_pos + 1
		else:
			merged_numbers[merge_pos] = numbers[right_pos]
			right_pos = right_pos + 1
		merge_pos = merge_pos + 1
	
	while left_pos <= j:
		merged_numbers[merge_pos] = numbers[left_pos]
		merge_pos = merge_pos + 1
		left_pos = left_pos + 1
	
	while right_pos <= k:
		merged_numbers[merge_pos] = numbers[right_pos]
		merge_pos = merge_pos + 1
		right_pos = right_pos + 1	
	
	#copy merged_numbers elements to numbers
	merge_pos = 0
	while merge_pos < merged_size:
		numbers[i + merge_pos] = merged_numbers[merge_pos]
		merge_pos = merge_pos + 1
```
*Tips*: The merge function is used to sorted each pieces lists in order.
```python
def merge_sort(numbers, i, k):
	j = 0
	if i < k
		j = (i + k)//2
		merge_sort(numbers, i, j)
		merge_sort(numbers, j + 1, k)
		# Merge left and right partition in sorted order
		merge(numbers, i, j, k)
```

***Shell Sort***

***Quick Sort***

***Radix Sort***

***Bucket Sort***
