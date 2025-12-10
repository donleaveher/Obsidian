***Recursive Functions***
```python
def count_down(count):
	if count == 0:
		print("Over")
	else:
		print(count)
		count_down(count-1)
count_down(2)# output: 2, 1, "Over"

def backwards_alphabet(curr_letter):
	if curr_letter == "a"
		print(curr_letter)
	else:
		print(curr_letter)
		pre_letter = char(ord(curr_letter)-1)
		backwards_alphabet(prev_letter)
```
***
***Recursive Algorithm: Search***
```python
def find(lst, item, low, high):
	mid = (high + low)//2
	if item == lst[mid]:
		pos = mid
	elif high == low:
		pos = -1
	else:
		if item < lst[mid]:
			pos = find(lst, item, low, mid)
		else:
			pos = find(lst, item, mid+1, high)
	return pos
```
***
***Tips***: Recursive functions can be particularly challenging to debug. Adding output statements can be helpful. Furthermore, an additional trick is to indent the print statements to show the current depth of recursion.
***Creating a recursive function***
- *Write base case* -- Every recursive function must have a case that returns a value without performing a recursive call. That case is called the base case. 
- *Write recursive case* -- The programmer then adds the recursive case to the function.
```python
#Step 1, The base case has to be written and tested
def nfact(n):
	fact = 0
	if n == 1 or n == 0:
		fact = 1
	return fact

#Step 2, The recursive case has to be added and tested
def nfact(n):
	fact = 0
	if n == 1 or n == 0:
		fact = 1
	else:
		fact = n * nfact(n - 1)
	return fact
```

***Recursive math function***
```python 
Fibonacci sequence:
def fibonacci(v1, v2, run_cnt):
	print(f"{v1} + {v2} = {v1 + v2}")
	if run_cnt <= 1:
		pass
	else:
		fibonacci(v2, v1 + v2, run_cnt-1)
		
def compute_nth_fib(num):
	if num <= 0:
		return 0
	elif num == 1:
		return 1
	else:
		return compute_nth_fib(num-2) + compute_nth_fib(num-1)
print(compute_nth_fib(2))
```

```python
Determine the greatest common divisor:
def gcd(n1, n2):
	if n1 == n2:
		return n1
	elif n1 > n2:
		return gcd(n1 - n2, n2)
	else:
		return gcd(n1, n2 - n1)
```

***Recursive exploration of all possibilities***
```python
def scramble(r_letters, s_letters):
	if len(r_letters) == 0:
		print(s_letters)
	else:
		for i in range(len(r_letters)):
			scramble_letter = r_letters[i]
			remaining_letters = r_letters[:i] + r_letters[i+1:]
			scramble(remaining_letters, s_letters + scramble_letter)	
```
