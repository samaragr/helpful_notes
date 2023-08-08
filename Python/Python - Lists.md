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

### Iterate lists
#iteration
e.g.
```python
animals = ['Lion', 'Zebra', 'Dolphin', 'Monkey'] 
chars = 0 
for animal in animals: chars += len(animal)
  print('Total characters: {}, Average Length: {}'.format(chars, chars/len(animals)))
```

e.g. - people = tuples where 1st email, 2nd full name
```python
def full_emails(people):
result = []
  for email, name in people:
      result.append('{} <{}>'.format(name, email))
return result

print(full_emails([('alex@example.com', 'Alex Diego'),('shay@example.com', 'Shay Brandt')]))
```

#### Enumerate function
#enumerate

e.g.
```python
winners = ['Ashley', 'Dylan', 'Reese']
  for index, person in enumerate(winners):
    print('{} - {}'.format(index +1, person))
```


```python
def skip_elements(elements):
	list = []
	for index, i in enumerate(elements):
		if index % 2 == 0:
			list.append(i)
	return list

print(skip_elements(["a", "b", "c", "d", "e", "f", "g"])) 
print(skip_elements(['Orange', 'Pineapple', 'Strawberry', 'Kiwi', 'Peach']))

```
 
### List comprehensions

e.g.
```python
def odd_numbers(n):
	return [x for x in range (0, n+1) if x % 2 != 0]

print(odd_numbers(5)) # Should print [1, 3, 5]
print(odd_numbers(10)) # Should print [1, 3, 5, 7, 9]
print(odd_numbers(11)) # Should print [1, 3, 5, 7, 9, 11]
print(odd_numbers(1)) # Should print [1]
print(odd_numbers(-1)) # Should print []
```

e.g.
```python
print([ x for x in range(1,101) if x % 10 == 0 ])
```
==same as== 
```python
my_list = []
for x in range(1,101):
	if x % 10 == 0:
	   my_list.append(x)
print(my_list)
```

