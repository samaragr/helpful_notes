## Data types
String e.g. "text"
integer e.g. 1, 8, 15
float e.g. 2.5
none - things that are empty or return nothing


## Print

`print("Hello world!")` - Syntax for printing a string of text

`print(360)`,`print(32*45)` - Syntax for printing numeric values

`value = 8*6`
`print(value)` - Syntax for printing the value of a variable

## Calculations
`print(3*8/2+5-1)` - Multiplication, division, addition, and subtraction
`print(4**6)`  - Syntax means 4 to the power of 6
`print(4**0.5)`  - To find the square root of a number

To calculate how many different possible combinations can be formed using a set of "x" characters with each character in "x" having "y" number of possible values, you will need to use an exponent for the calculation:
`x = 4`
`y = 26`
`print(y**x)`

Assignment of values to the variables:
`years = 10`
`weeks_in_a_year = 52`
This variable is assigned an arithmetic calculation:
`weeks_in_a_decade = years * weeks_in_a_year` 
Prints the calculation stored in the "weeks_in_a_decade" variable:
`print(weeks_in_a_decade)` 

## Variables
- "containers" for data
- store values inside a variable

Convert data type (number to string)
`total = 2048 + 4357 + 97658 + 125 + 8`
`files = 5`
`average = total / files`
`print("The average size is:" + str(average))`


## Operators

`**` - to the power
`//` - floor devision - takes integer part of the division as result (e.g. 5//2 = 2 instead of 2.5)
`%` - modulo, returns the remainder of the integer division between two numbers.

### comparison operators
==returns boolean result==
`==` - equal to
`!=` - not equal to
`> `- greater than
`< `- less than
`>= `- greater than or equal to
`<=` - less than or equal to

str - To check if the first letter(s) of a string have a larger Unicode value (meaning the letter is closer to 122 or lowercase z) than the first letter of another string, use the greater than operator: >

### logical operators
`and`
`or`
`not`


Values: **True**, **False**, **None** Conditions: **if**, **elif**, **else** Logical operators: **and**, **or**, **not** Loops: **for**, **in**, **while**, **break**, **continue** Functions: **def**, **return**