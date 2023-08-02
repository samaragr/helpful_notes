## Strings
#strings
- Strings are sequences of characters and are immutable
- character in string = use index 
e.g.
`name = "Samara"`
`print (name[0])`
`S`

`print (name[-1])`
`a`

`name.index("m")`
`2`

`name.index("a")`
`1` - return first index it matches


### Operations
#operations
-   **len(string) -** Returns the length of the string
-   **for character in string** - Iterates over each character in the string
-   **if substring in string** - Checks whether the substring is part of the string
-   **string[i]** - Accesses the character at index **i** of the string, starting at zero
-   **string[i:j]** - Accesses the substring starting at index **i**, ending at index **j** minus 1. If **i** is omitted, its value defaults to **0**. If **j** is omitted, the value will default to **len(string)**.

### Slice
- portion of str conatining more than 1 character (substring)
`color = "Orange"`
`color [1:4]`
`"ran"`

`fruit = "Pineapple"`
`print(fruit[:4])`
`Pine`

`fruit = "Pineapple"`
`print(fruit[4:])`
`apple`

### Str methods
#strmethods
`.strip()` - remove spaces, tabs etc.
`.lstrip()` - remove spaces, tabs etc. to left of str
`.rstrip()` - remove spaces, tabs etc. to right of str
`string.isalpha()` - Returns True if there are only alphabetic characters in the string. If not, returns False.
`string.split()`- Returns a list of substrings that were separated by whitespace (whitespace can be a space, tab, or new line)
`.count() `- how many times certain substring in string
`.endswith() `- weather str ends with certain substring
`.isnumeric()` - Returns True if there are only numeric characters in the string. If not, returns False.
	`int()` - to convert to number
`.join()` - concatenate
	e.g. `" ".join(["This", "is", "a", "phrase", "joined", "by", "spaces"])`
	output 'This is a phrase joined ==by spaces==' - due to " " at start
`.upper()` - return uppercase
`.lower()` - return lowercase
`.rfind()` - searches for last occurence of str
`string.split(delimiter)` - Returns a list of substrings that were separated by whitespace or a delimiter
`string.replace(old, new)` - Returns a new string where all occurrences of old have been replaced by new.
`delimiter.join(list of strings)` - Returns a new string with all the strings joined by the delimiter

### Formatting
#formatting
`.format()` - used to insert parameters into 
e.g.
`name = "Manny"`
`number = len(name) * 3`
`print("Hello {}, your lucky number is {}" .format(name, number)`

e.g
`def student_grade(name, grade):`
`return "{} received {}% on the exam" .format(name, grade)`
  
`print(student_grade("Reed", 80))`
`print(student_grade("Paige", 92))`
`print(student_grade("Jesse", 85))`

output
Reed received 80% on the exam
Paige received 92% on the exam
Jesse received 85% on the exam

#### Formatting expressions
`{:.2f}` - : separates from field name, .2f = format float number and 2dp after decimal
`{:>3}` - greater than to align text to right (in this case for a total of 3 spaces) can precede previous for both
`{:.1s}` - 1 character
