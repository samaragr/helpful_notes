#loops
## while loops
#while
- initialise variables
- infinite loops - 
	- `x +=1` is a shorthand version of `x = x+1`. inside `while` to increase variable value by 1
	- `break` to stop a loop

`while` *specified condition* `is True:`
*body of loop*

e.g.
```python
multiplier = 1
result = multiplier*5
while result <= 50:
	print(result)
	multiplier += 1
	result = multiplier*5
print("Done") 
```

e.g.
```python
number = 1 # Initialize the variable
while number <= 12:
	if number % 2 == 0:
		print(number, end=" ")
	number +=1 # Increment the variable
# Should print 2 4 6 8 10 12
```

e.g.
```python
def count_factors(given_number):
	factor = 1
	count = 1
	if given_number == 0:
		return 0
	while factor < given_number:
		if given_number % factor == 0:
			count += 1
		factor += 1
	return count

print(count_factors(0)) # Count value will be 0
print(count_factors(3)) # Should count 2 factors (1x3)
print(count_factors(10)) # Should count 4 factors (1x10, 2x5)
print(count_factors(24)) # Should count 8 factors (1x24, 2x12, 3x8, and 4x6).

```

e.g.
```python
def addition_table(given_number):
	iterated_number = 1
	my_sum = 1
	while iterated_number <= 5:
		my_sum = given_number + iterated_number
		if my_sum > 20:
			break
		print(str(given_number), "+", str(iterated_number), "=", str(my_sum))
		iterated_number += 1


addition_table(5)
addition_table(17)
addition_table(30)

# output:
# 5 + 1 = 6 
# 5 + 2 = 7 
# 5 + 3 = 8 
# 5 + 4 = 9 
# 5 + 5 = 10 
# 17 + 1 = 18 
# 17 + 2 = 19 
# 17 + 3 = 20
```

e.g.
```python
def elevator_floor(enter, exit):
	floor = enter
	elevator_direction = ""
	if enter > exit:
		elevator_direction = "Going down: "
		while floor >= exit:
			elevator_direction += str(floor)
			if floor > exit:
				elevator_direction += " | "
			floor -= 1
	else:
		elevator_direction = "Going up: "
		while floor <= exit:
			elevator_direction += str(floor)
			if floor < exit:
				elevator_direction += " | "
			floor += 1
	return elevator_direction

print(elevator_floor(1,4)) # Should print Going up: 1 | 2 | 3 | 4
print(elevator_floor(6,2)) # Should print Going down: 6 | 5 | 4 | 3 | 2

```

## For loops
#for
iterate of a range of numbers / list of strings

`for `*variable* `in `*sequence*:
*body of loop*
e.g. 
```python
for x in range (5):
	print (x)

# output 0 1 2 3 4 
```

e.g.
```python
friends = ["taylor", "alex", "pat", "eli"]
for friend in friends:
	print("Hi" + friend)
```

e.g.
```python
values = [23, 52, 59, 37, 48]
sum = 0
length = 0
for value in values:
	sum += value
	length += 1
print ("total sum: " + str(sum) + " - average: " + str(sum/length))
```

e.g.
```python
def count_by_10(end):
	count = ""
	for number in range(0,end+1,10):
		count += str(number) + " "
	return count.strip()

print(count_by_10(100))
# should print 0 10 20 30 40 50 60 70 80 90 100
```

### Nested for loops

e.g.
```python
for x in range(2):
	print("This is the outer loop iteration number " + str(x))
	for y in range(3+1):
		print("Inner loop iteration number " + str(y))
	print("Exit inner loop")

"""output
This is the outer loop iteration number 0 
Inner loop iteration number 0
Inner loop iteration number 1 
Inner loop iteration number 2 
Inner loop iteration number 3 
Exit inner loop 
This is the outer loop iteration number 1 
Inner loop iteration number 0 
Inner loop iteration number 1 
Inner loop iteration number 2 
Inner loop iteration number 3 
Exit inner loop"""
```


- for loop w nested IF statement
e.g.
```python
for x in range(7):
	if x % 2 == 0:
		print(x)
```

e.g.
```python
def matrix(initial_number, end_of_first_row):
	n1 = initial_number
	n2 = end_of_first_row+1
	for column in range(n1, n2):
		for row in range(n1, n2):
			print(column*row, end=" ")
		print()

matrix(1, 4)

"""ouput
1 2 3 4
2 4 6 8
3 6 9 12
4 8 12 16"""

```

e.g.
```python
def rows_asterisks(rows): 
	for x in range(rows): # Complete the outer loop range to control the number of rows
		for y in reange(x+1): # Complete the inner loop range to control the number of asterisks per row
		print("*", end=" ") # Prints one asterisk and one space
print() # An empty print() function inserts a line break at the end of the row

rows_asterisks(5)

"""output
*
* *
* * *
* * * *
* * * * *"""

```

## Recursion
#recursive
```python
def recursive_function(parameters):
	if base_case_condition(parameters):
		return base_case_value
	recursive_function(modified_parameters)
```

e.g
```python
def is_power_of(number, base): # Base case: when number is smaller than base
if number < base: 
	return number == 1 # If number is equal to 1, it's a power (base* 0)
	return is_power_of(number/base, base) #Recursive case: keep dividing number by base

print(is_power_of(8,2)) # Should be True
print(is_power_of(64,4)) # Should be True
print(is_power_of(70,10)) # Should be False
```

using recursion
```python
def sum_positive_numbers(n):
	if n <= 1:
		return n
	return n + sum_positive_numbers(n-1)

print(sum_positive_numbers(3)) # Should be 6
print(sum_positive_numbers(5)) # Should be 15
```

