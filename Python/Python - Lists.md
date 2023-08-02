## Lists
#list
- Lists are sequences of elements of any type and are mutable
`.append()` - appends to end of list
`.insert(`*index*, *element*`)` - adds element to index specified, use index higher than current length = just added to the end
`.remove("")` - removes element from first instance in the list, if element not in list gives value error
`.pop(` *index*`)` - removes element from specified index - returns element removed
*list*`[`*index*`]` `= "`*element*`"` - replaces element in list with new element by specifying index

### tuples
#tuples
- Tuples are sequences of elements of any type that are immutable.
e.g.
`fullname = (Samara, 'H', 'Garrett-Rickman')`


### iterate lists
#iteration
e.g.
`animals = ['Lion', 'Zebra', 'Dolphin', 'Monkey'] `
`chars = 0 `
	`for animal in animals: chars += len(animal) `
	`print('Total characters: {}, Average Length: {}'.format(chars, chars/len(animals)))`

Total characters: 22, Average Length: 5.5

e.g.
`def full_emails(people):` - people = tuples where 1st email, 2nd full name
`result = [] `
`for email, name in people: `
`result.append('{} <{}>'.format(name, email)) `
`return result `
`print(full_emails([('alex@example.com', 'Alex Diego'),('shay@example.com', 'Shay Brandt')]))`

['Alex Diego <alex@example.com>', 'Shay Brandt <shay@example.com>']

#### enumerate function
#enumerate

e.g.
`winners = ['Ashley', 'Dylan', 'Reese'] `
`for index, person in enumerate(winners): `
`print('{} - {}'.format(index +1, person))` - get index + name

1 - Ashley
2 - Dylan
3 - Reese

`def skip_elements(elements): `
	`list = [] `
	`for index, i in enumerate(elements): `
		`if index % 2 == 0: `
			`list.append(i) `
	`return list`
 
`print(skip_elements(["a", "b", "c", "d", "e", "f", "g"])) `
`print(skip_elements(['Orange', 'Pineapple', 'Strawberry', 'Kiwi', 'Peach'])) `

output
['a', 'c', 'e', 'g']
['Orange', 'Strawberry', 'Peach']

### List comprehensions

e.g.
`def odd_numbers(n):`
	`return [x for x in range (0, n+1) if x % 2 != 0]`

`print(odd_numbers(5))` # Should print [1, 3, 5]
`print(odd_numbers(10))` # Should print [1, 3, 5, 7, 9]
`print(odd_numbers(11))` # Should print [1, 3, 5, 7, 9, 11]
`print(odd_numbers(1)) `# Should print [1]
`print(odd_numbers(-1)) `# Should print []



e.g.
`print([ x for x in range(1,101) if x % 10 == 0 ])`
==same as== 
`my_list = []`
`for x in range(1,101):`
`if x % 10 == 0:`
`my_list.append(x)`
`print(my_list)`

