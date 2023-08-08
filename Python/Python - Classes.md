- define a new class, classes start with capital letter
```python
class Apple:
pass
```

- define attributes
```python
class Apple:
	  color = ""
	  flavor = ""
```

- create a new instance of class
	- to create a new instance of any class call the name of the class as if it were a function
```python
jonagold = Apple () 
golden = Apple ()
```

- set values of attributes
	- dot notation lets you access any abilities objects might have (methods) or info that object might have (attributes)
```python
jonagold.color = "red" 
jonagold.flavor = "sweet"
golden.color = 'yellow'
golder.flavor = 'soft'

print(jonagold.color) 
```
output - `red` 

## Instance methods
- a method that belongs to instances of a class, not to the class itself.
- Use `self` as the first parameter in the instance method when defining it. The `self` parameter refers to the current object.
- Using the `self` parameter to access or modify the current object attributes.

```python
class piglet: 
  def speak(self):
      print('oink oink') 

hamlet = piglet()  # assign item to class
hamlet.speak()  # call method

class piglet: # make a new class 
	name = 'Piglet' # default name 
	def speak(self): # create a new method 
		print('Oink! Im {}! Oink!'.format(self.name))
```


## Constructors
- special method
- `__init__` - special method inside a class to create an object (for initialisation of an class)
- define multiple attributes to a class

e.g.
```python
class apple:
	def __init__(self, color, flavor): 
		self.color = color
		self.flavor = flavor 

jonagold = apple('red', 'sweet')
print(jonagold.color)
```
output - `red`

e.g.
```python
class apple: 
  def __init__(self, color, flavor): 
    self.color = color
	self.flavor = flavor
  def __str__(self):
    return 'This apple is {} and its flavor is {}'.format(self.color,  self.flavor)

jonagold = apple('red', 'sweet')
print(jonagold) 
```
output - `This apple is red and its flavor is sweet`

## Documenting
#docstring

- can use help on own functions, list defined methods but doc sometimes not helpful
- docstring - brief text that explains what something does
- can add to classes and methods too

to add docstring - indent and triple quotes
e.g.
	`"""info written here"""`


