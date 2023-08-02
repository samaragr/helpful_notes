- define a new class, class strat with capital letter
`class Apple:`
	`pass`

- define attributes
`class Apple:`
	`color = ""`
	`flavor = ""`

- create a new instance of class
`jonagold = Apple ()` - to create a new instance of any class call the name of the class as if it were a function
`golden = Apple ()`

- set values of attributes
`jonagold.color = "red"` - str value - dot notation #dotnotation
`jonagold.flavor = "sweet"`
`golden.color = 'yellow'`
`golder.flavor = 'soft'`

`print(jonagold.color)` 
output
`red` 

`print(jonagold.color.upper)` 
output
`RED` 

#dotnotation 
- lets you access any abilities objects might have (methods) or info that object might have (attributes)


## Instance methods

`class piglet: ` - make a new class
	`def speak(self): ` - create a new method
		`print('oink oink') ` 

`hamlet = piglet()`  - assign item to class
`hamlet.speak()`  - call method


`class piglet: `- make a new class 
	`name = 'Piglet' `- default name 
	`def speak(self): `- create a new method 
		`print('Oink! Im {}! Oink!'.format(self.name))`


## Constructors
- special method
- `__init__` - special method inside a class to create an object (for initialisation of an class)
- define multiple attributes to a class

`class apple:`
	`def __init__(self, color, flavor): ` - init = constructor
		`self.color = color `
		`self.flavor = flavor `

`jonagold = apple('red', 'sweet')`
`print(jonagold.color)`

output
`red`

e.g.
`class apple: def __init__(self, color, flavor): ` - special method 
`self.color = color `
`self.flavor = flavor `
`def __str__(self): `- call bk when Print is used 
`return 'This apple is {} and its flavor is {}'.format(self.color, self.flavor) `
`jonagold = apple('red', 'sweet') `
`print(jonagold)` - due to STR above, don't get an error.

output
`This apple is red and its flavor is sweet`

## Documenting
#docstring

- can use help on own functions, list defined methods but doc sometimes not helpful
- docstring - brief text that explains what something does
- can add to classes and methods too

to add docstring - indent and triple quotes
e.g.
	`"""info written here"""`


