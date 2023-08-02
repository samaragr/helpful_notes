## Inheritance
#inheritance

`class fruit: def __init__(self, color, flavor): `
`self.color = color `
`self.flavor = flavor `

`class apple(fruit):` - add apple to FRUIT class, Inherit from Fruit class. have same constructors of init. i.e. class within a class
`pass `

`class grape(fruit): `
`pass `- empty class - automatically have same constructor as defined by fruit

`granny_smith = apple('green', 'tart') `
`carnelian = grape('purple', 'sweet') `

`print(granny_smith.flavor)`
out
`tart`

## Composition
#composition

- two different classes are related, but there is no inheritance going on. This is referred to as **composition** -- where one class makes use of code contained in another class.


e.g.
`class Clothing:`
	`stock={ 'name': [],'material' :[], 'amount':[]}`
	`def __init__(self,name):`
		`material = ""`
		`self.name = name`
	`def add_item(self, name, material, amount):`
		`Clothing.stock['name'].append(self.name)`
		`Clothing.stock['material'].append(self.material)`
		`Clothing.stock['amount'].append(amount)`
	`def Stock_by_Material(self, material):`
		`count=0`
		`n=0`
			`for item in Clothing.stock['material']:`
			`if item == material:`
				`count += Clothing.stock['amount'][n]`
				`n+=1`
		`return count`

`class shirt(Clothing):`
	`material="Cotton"`
`class pants(Clothing):`
	`material="Cotton"`
`polo = shirt("Polo")`

`sweatpants = pants("Sweatpants")`
`polo.add_item(polo.name, polo.material, 4)`
`sweatpants.add_item(sweatpants.name, sweatpants.material, 6)`
`current_stock = polo.Stock_by_Material("Cotton")`
`print(current_stock)`


## Python Modules

- used to organise functions, classes and other data together ina  structured way
- ready to use - python std library
- Can create own
- uses dot to separate the name of module and the function provided by that module (similar to *class.method*) 

import (keyword) to import `random` module
e.g.
`import random`
`random.randint(1,10)` - generates a random int between 1 and 10


module list
- datetime
- random

