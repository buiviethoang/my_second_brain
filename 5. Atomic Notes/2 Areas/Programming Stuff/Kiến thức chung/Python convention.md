2025-08-30 09:32
Status: #baby
Tags: [[coding]]
## Main





* Naming convention: 
- Function: function, my_function
- Variable: x, var, my_variable
- Class: Model, MyClass
- Method: class_method, method 
- Constant: MY_CONSTANT, MY_LONG_CONSTANT
- Module: module.py, my_module.py
- Package: package, mypackage (not seperate words with underscores)
* How to choose name: 
- Clear and infomative: 
# Not recommend: x, y = z.split()
# Recommend: first_name, last_name = name.split()
# Not recommend: def db(x): return x*2
# Recommend: def multiply_by_two(x): return x*2
* Code Layout:
- Surround top-level functions and classes with two blank lines:
Eg: 
class MyFirstClass:
    pass


class MySecondClass:
    pass


def top_level_function():
    return None

- Surround method definitions inside classes with a single blank line
Eg: 
class MyClass:
    def first_method(self):
        return None

    def second_method(self):
        return None

- Use blank lines sparingly inside functions to show clear steps:
Eg: 
def calculate_variance(number_list):
    sum_list = 0
    for number in number_list:
        sum_list = sum_list + number
    mean = sum_list / len(number_list)

    sum_squares = 0 
    for number in number_list:
        sum_squares = sum_squares + number**2
    mean_squares = sum_squares / len(number_list)

    return mean_squares - mean**2

=> Should be 1 black line before return statement for the sake of clearness

* Maximum Line Length and Line Breaking:
- Lines should be limited to 79 characters 
Python will assume line continuation if code is contained within parentheses, brackets, or braces
Eg: 
def function(arg_one, arg_two,
             arg_three, arg_four):
    return arg_one

- Use backslashes to break lines instead (recommend)
Eg: 
from mypkg import example1, \
    example2, example3

- Breaking before a binary operator:
# Recommended
total = (first_variable
         + second_variable
         - third_variable)

* Indentation:
- Use 4 consecutive spaces to indicate indentation
- Prefer spaces over tabs

* Indentation Following Line Breaks:
- Should:
Eg: 
x = 5
if (x > 3 and
    x < 10):
    # Both conditions satisfied
    print(x)

Or:
x = 5
if (x > 3 and
        x < 10):
    print(x)

Instead of: 
x = 5
if (x > 3 and
    x < 10):
    print(x)

- Hanging indent:
Should not:
# Not Recommended (must not be any arguments on the first line)
var = function(arg_one, arg_two,
    arg_three, arg_four)

Should: 
var = function(
    arg_one, arg_two,
    arg_three, arg_four)

# Not Recommended
def function(
    arg_one, arg_two,
    arg_three, arg_four):
    return arg_one

def function(
        arg_one, arg_two,
        arg_three, arg_four):
    return arg_one

* Where to Put the Closing Brace:
- Line up the closing brace with the first non-whitespace character of the previous line
list_of_numbers = [
    1, 2, 3,
    4, 5, 6,
    7, 8, 9
    ]
- Line up the closing brace with the first character of the line that starts the construct
list_of_numbers = [
    1, 2, 3,
    4, 5, 6,
    7, 8, 9
]

* Comments:
- Limit the line length of comments and docstrings to 72 characters
- Use complete sentences, starting with a capital letter
- Make sure to update comments if you change your code

* Block Comments:
- Indent block comments to the same level as the code they describe
- Start each line with a # followed by a single space
- Separate paragraphs by a line containing a single #
Eg: 
for i in range(0, 10):
    # Loop over i ten times and print out the value of i, followed by a
    # new line character
    print(i, '\n')

* Inline Comments:
- Use inline comments sparingly
- Write inline comments on the same line as the statement they refer to
- Separate inline comments by two or more spaces from the statement
- Start inline comments with a # and a single space, like block comments
- Don’t use them to explain the obvious
Eg:
x = 5  # This is an inline comment
x = 'John Smith'  # Student Name

# Not Recommend: 
empty_list = []  # Initialize empty list

x = 5
x = x * 5  # Multiply x by 5

* Documentation Strings:
- Surround docstrings with three double quotes on either side, as in """This is a docstring"""
- Write them for all public modules, functions, classes, and methods
- Put the """ that ends a multiline docstring on a line by itself
- For one-line docstrings, keep the """ on the same line
Eg: 
def quadratic(a, b, c, x):
    """Solve quadratic equation via the quadratic formula.

    A quadratic equation has the following form:
    ax**2 + bx + c = 0

    There always two solutions to a quadratic equation: x_1 & x_2.
    """
    x_1 = (- b+(b**2-4*a*c)**(1/2)) / (2*a)
    x_2 = (- b-(b**2-4*a*c)**(1/2)) / (2*a)

    return x_1, x_2

Eg2: 
def quadratic(a, b, c, x):
    """Use the quadratic formula"""
    x_1 = (- b+(b**2-4*a*c)**(1/2)) / (2*a)
    x_2 = (- b-(b**2-4*a*c)**(1/2)) / (2*a)

    return x_1, x_2

* Whitespace in Expressions and Statements:
- Assignment operators (=, +=, -=, and so forth)
Eg: 
# Recommended
def function(default_parameter=5):
    # ...


# Not recommended
def function(default_parameter = 5):
    # ...

- Comparisons (==, !=, >, <. >=, <=) and (is, is not, in, not in)
- Booleans (and, not, or)
Eg:
# Recommended
y = x**2 + 5
z = (x+y) * (x-y)

# Not Recommended
y = x ** 2 + 5
z = (x + y) * (x - y)

# Not recommended
if x > 5 and x % 2 == 0:
    print('x is larger than 5 and divisible by 2!')

# Recommended
if x>5 and x%2==0:
    print('x is larger than 5 and divisible by 2!')

# Definitely do not do this!
if x >5 and x% 2== 0:
    print('x is larger than 5 and divisible by 2!')

Should use:
list[3:4]

# Treat the colon as the operator with lowest priority
list[x+1 : x+2]

# In an extended slice, both colons must be
# surrounded by the same amount of whitespace
list[3:4:5]
list[x+1 : x+2 : x+3]

# The space is omitted if a slice parameter is omitted
list[x+1 : x+2 :]

* When to Avoid Adding Whitespace:
- Immediately inside parentheses, brackets, or braces
Eg:
# Recommended
my_list = [1, 2, 3]

# Not recommended
my_list = [ 1, 2, 3, ]
- Before a comma, semicolon, or colon
Eg:
x = 5
y = 6

# Recommended
print(x, y)

# Not recommended
print(x , y)
- Before the open parenthesis that starts the argument list of a function call
def double(x):
    return x * 2

# Recommended
double(3)

# Not recommended
double (3)
- Before the open bracket that starts an index or slic
# Recommended
list[3]

# Not recommended
list [3]
- Between a trailing comma and a closing parenthesis
# Recommended
tuple = (1,)

# Not recommended
tuple = (1, )
- To align assignment operators
# Recommended
var1 = 5
var2 = 6
some_long_var = 7

# Not recommended
var1          = 5
var2          = 6
some_long_var = 7

* Programming Recommendations:
- on’t compare Boolean values to True or False using the equivalence operator. 
Eg:
# Not recommended
my_bool = 6 > 5
if my_bool == True:
    return '6 is bigger than 5'
# Recommended
if my_bool:
    return '6 is bigger than 5'

- Use the fact that empty sequences are falsy in if statements
Eg:
# Not recommended
my_list = []
if not len(my_list):
    print('List is empty!')

# Recommended
my_list = []
if not my_list:
    print('List is empty!')

- Use is not rather than not ... is in if statements
Eg:
# Recommended
if x is not None:
    return 'x exists!'

# Not recommended
if not x is None:
    return 'x exists!'

- Don’t use if x: when you mean if x is not None
Eg: 
# Not Recommended
if arg:
    # Do something with arg...

# Recommended
if arg is not None:
    # Do something with arg...

- Use .startswith() and .endswith() instead of slicing
# Not recommended
if word[:3] == 'cat':
    print('The word starts with "cat"')

# Recommended
if word.startswith('cat'):
    print('The word starts with "cat"')

# Not recommended
if file_name[-3:] == 'jpg':
    print('The file is a JPEG')

# Recommended
if file_name.endswith('jpg'):
    print('The file is a JPEG')


** Check Python code against PEP8:
$ pip install pycodestyle
Then run: 
$ pycodestyle code.py

** Autoformatters: 
$ pip install black
Then run:
$ black code.py
Config a little bit for line breaking: 
$ black --line-length=79 code.py


## References
