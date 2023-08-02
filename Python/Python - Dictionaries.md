- curly brackets
- mutable

e.g. empty dictionary
`x= {}`
`type(x)`
output
`<class 'dict'>`

Syntax
`my_dictionary = {keyA:value1,value2, keyB:value3,value4}`

key : value
- key can be any immutable data type (e.g. numbers, booleans, strings and tuples) 
- value can be anything incl. other dicts

e.g use to store no. of files corresponding to file type
	`file_counts = {"jpg":10, "txt":14, "csv":2, "py":23}`

- to add to dictionary...
		`file_counts["cfg"] = 8`
		if use a key that already exists then replaces value
- to delete
		`del file_counts["cfg"]`

- use dict in for loop then iterate through key values
	*dict*`.keys()` - returns keys
	*dict*`.values()` - returns values
	*dict*`.items()` - returns tuple for each element in dictionary. first = key, second = value
		e.g.
		`for ext, amount in file.items(): `
		`print('There are {} files with the .{} extensions'.format(amount, ext))`

#### Operations
- `len(`*dictionary*`)` - Returns the number of items in a dictionary.
- `for` *key* `in `*dictionary* - Iterates over each key in a dictionary.
- `for` *key, value* `in` *dictionary*`.items()` - Iterates over each key,value pair in a dictionary.
- `if` *key* `in` *dictionary* - Checks whether a key is in a dictionary.
- `dictionary[`*key*`] `- Accesses a value using the associated key from a dictionary.
- `dictionary[`*key*`]` = value - Sets a value associated with a key.
- `del dictionary[`*key*`]` - Removes a value using the associated key from a dictionary.

#### Methods
- *dictionary*`.get(`*key, default*`)` - Returns the value corresponding to a key, or the default value if the specified key is not present.
- (dictionary)`.keys()` - Returns a sequence containing the keys in a dictionary.
- *dictionary*`.values() `- Returns a sequence containing the values in a dictionary.
- *dictionary*`[`*key*`].append(`*value*`)` - Appends a new value for an existing key.
- *dictionary*`.update(`*other_dictionary*`)`- Updates a dictionary with the items from another dictionary. Existing entries are replaced; new entries are added.
- *dictionary*`.clear() `- Deletes all items from a dictionary.
- *dictionary*`.copy() `- Makes a copy of a dictionary.


#### Sets
- One of these data types is a set which is a bit like a cross between a list and a dictionary. 
- A set is used when you want to store a bunch of elements and be certain that there are only present once. 
- Elements of a set must also be immutable. 
- You can think of this as the keys of a dictionary with no associated values 
- or you could see it as a list where what matters isn't the order of the elements but whether an element is in the list or not.


