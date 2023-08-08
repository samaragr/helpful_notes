- **parameter (argument)** -  a value passed into a function for use within the function

- `type (`*x*`)` - returns data type
- `str (`*x*`)` - converts to string type
- `int (`*x*`)` - converts to integer type
- `float (`*x*`)` - converts to float type
- `len()` - returns length of a string
- `return` - tells the function to pass data back. When we call the function, we can store the returned value in a variable.

- `def` .... `:`- define a function - followed by function name, body of function must be indented to R of def
	e.g. function
```python
def greeting(name, department):
  print ('Welcome, ' + name)
  print ("You are part of " + department)
```

## Conditionals
- `if` - 
- `else` - 
- `elif` - Companion to if block, will be checked if condition of if statement wasn't true
```python
if condition1:
    action1
elif condition2:
    action2
else:
    action3
```

## Range 
- 1, 2, or 3 parameters
	- 1 = upper limit
	- 2 = lower and upper
	- 3 = 2 + increments
e.g.
```python
for n in range(x, y, z):
  print(n)
```

- `range(5)` - range from 0-4
- `for n in range (1,10)` - range 1- 9
- `for x in range (0,101,10)` - range 0-100 in steps of 10



