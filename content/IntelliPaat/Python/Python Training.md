
## Module 1 - Getting Started With Python
  
### Lecture 1 – Agenda (Getting Started With Python)

  
### Lecture 2 – Introduction To Python
Cloud and DevOps - [[OpenStack]] APIs and Fabric
Installing python

### Lecture 3 – Python Variables
Assigning a Single Value:
age = 25
Multiple Assignment:
a = b = c = 10
x,  y,  z = 10, 20, 30

### Lecture 4 – Python Tokens

In Python, every logical line of code is broken down into components known as Tokens (everything you type is a token)

Normal Token Types:
- Keywords
    - Python keywords are special [[Python Keywords aka. reserved words|reserved words]]
    - They convey a special meaning to the Compiler/lnterpreter
    - Each keyword has a special meaning and a specific operation
    - NEVER use it as a variable

- Identifiers
    - An identifier is the name used to identify a variable, function, class, or object. Keep in mind the rules for naming an identifier

- Literals
    - A literal is the raw data given to a variable
    - Various Types of Literals:
      - **String literals** - Formed by enclosing a text within quotes. Both single and double quotes can be used
      - **Numeric literals** - Formed by enclosing a text within quotes. Both single and double quotes can be used
      - **Boolean literals** - It can either be True or False. 
      - **Special literals** - There is a special literal in Python called None which means that the variable is yet to be initialized
      - **Operators** - Operators are special symbols that are used to carry out arithmetic and logical operations
    
Various Types of Operators:
[[Python Arithmetic Operators.png|Arithmetic]] - Used for common mathematical operations
[[Python Assignment Operators.png|Assignment]] - Used to assign values to variables
[[Python Comparison Operators.png|Comparison]] - Compares values and returns either True or False
[[Python Logical Operators.png|Logical Operators]] - Used to combine conditional statements

> [!attention] Don't get it
> [[Python Bitwise Operators.png|Bitwise]] - Used to compare binary numbers #pending



[[Python Identity Operators.png|Identity]] - Used to check if the objects are the same or not. Compares the ID of an object. ex: 1 is "1" if False, because one object comes from class Int and other class str, so they have different IDs
[[Python Membership Operators.png|Membership]] -  Used to test if a sequence is present in an object
Ex: `nums = [1, 2, 3, 4]` we try  `4 in nums` give us `True`


### Lecture 5 – Data Types In Python
![[Pasted image 20230804112127.png]]
*The `string.replace()` method you mentioned does not modify the original string in-place. Instead, it returns a new string with the specified replacements performed.*

**Tuples** - A sequence of immutable Python objects

```python
>>> salaries['John']
15
```

Dictionary, you can use `.get()` 
ex: `salaries.get("John, 18")` This returns 15 but if there was no value it will default to 18, same thing if it did not find keyword John, defaults to 18

**Sets** - An unordered collection of immutable data which has no duplicate elements
	set is like a list with unique values, so if you want to make sure a list has certain value and doesnt repeast just use set, so you dont have to be checking whehter it exists on the list etc



Comprehensions:
*So the thing before `for` is what you want to add to the list*

Example - Squaring numbers from 1 to 5:
```python
squared_numbers = [x**2 for x in range(1, 6)]
# Result: [1, 4, 9, 16, 25]
```

Example - Generating a set of even numbers from a list:
```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
even_set = {x for x in numbers if x % 2 == 0}
# Result: {2, 4, 6, 8, 10}
```

Example - Creating a dictionary of squares for numbers 1 to 5:
```python
squared_dict = {x: x**2 for x in range(1, 6)}
# Result: {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
```



### Lecture 6 – Conditional Statements

These statements are used to change the flow of execution when a provided condition is True or False

if-else
Nested if-else


## Module 2 - Python Basic Constructs

### Lecture 1 – Looping Statements
for
while
break
continue - `if (x == 4): continue` it skips the value value when `print(x)`. Sample in [[Linux Training#Lecture 4 – Hands-On Looping Statements]]

### Lecture 2 – Functions In Python

A function is a block of organized, reusable set of instructions that is used to perform some related actions

User-defined Functions
Built-in Functions- A function already available in a language that we can directly use in our code `abs()`, `all()`, `any()` other

Lambda Function - An anonymous function, i.e., a function having no name. A Lambda function cannot contain more than one expression

```python
lambda <arguments>: <expression>
```

 ```bash
 # Lambda Function 
 r = lambda x, y: x * y 
 
 # Call the Lambda function 
 result = r(12, 3) print(result)
 ```
 
 ```python
 def myfunc(n):
     return lambda a: a + n #returns lambda function with an n value
 
 mySum = myfunc(3) #lambda function now in mySum
 print(mySum(10)) #calling lambda function from mySum passing 10 to a
 ```
You can send the lambda function as an argument

### Lecture 3 – Python Arrays And OOPS
No built-in support for arrays we use lists instead
list.append("keyword")
list.remove("keyword")
list.pop(index)

A class is like a "blueprint" for creating objects

  
### Lecture 4 – File Handling In Python
Open
Read
Write/Create
Delete

The open() function takes two parameters: filename and mode
- 'r' — Read: The default value; opens a file for reading; returns an error if the file does not exist.
- 'a' — Append: Opens a file for appending; creates the file if it does not exist.
- 'w' — Write: Opens a file for writing; creates the file if it does not exist.
- 'x' — Create: Creates the specified file; returns an error if a file with the same name already exists.


The read() function is used to read n bytes from the mentioned file
Can read n for lines print(f.read(5))

If you want to read line by line you can loop throught it. For x in the variable where open(file, r) was saved

`f.close()` need to close file so change made in memory take effect


## Module 3 - Numpy Basic

### Lecture 1 – Introduction To NumPy
1-Dimensional Array:
```python
import numpy as np  
a = np.array([1, 2, 3])  
print(a)
```
Output:
`[1 2 3]`

2-Dimensional Array:
```python
import numpy as np  
b = np.array([[1, 2, 3], [4, 5, 6]])  
print(b)
```
Output:
```bash
[[1 2 3]  
 [4 5 6]]
```

Initialize all the elements of x cross y array to 0
```python
import numpy as np

zeros_array = np.zeros((3, 4))
print(zeros_array)
```
Output:
```python
[[0. 0. 0. 0.]
 [0. 0. 0. 0.]
 [0. 0. 0. 0.]]
```

Arrange the numbers between x and y with an interval of z
```python
import numpy as np
np.arange(1,10,2)
```
Output:
```bash
array([1, 3, 5, 9])
```

Print all even numbers between 10 and 20
```python
np.arange(10,20,2)
```
Output:
```python
array([10, 12, 14, 16, 18])
```

#pending
> [!Attention] Skiped
> ## Module 3 - Numpy Basic
> Lecture 1 – Introduction To NumPy_00:04_
> Lecture 2 – Initializing A NumPy Array_00:09_
> Lecture 3 – Inspecting A NumPy Array_00:16_
> Lecture 4 – Performing Mathematical Functions Using Numpy
> Lecture 5 – NumPy Array Manipulation_00:06_
> ## Module 4 Numpy Advance
> Lecture 1 – Indexing And Slicing Using NumPy_00:08_
> Lecture 2 – NumPy Vs List_00:07_
> Lecture 3 – SciPy Introduction_00:03_
> Lecture 4 – Sub-Package Cluster_00:07_
> Lecture 5 – SCIPY – STATS_00:05_
> Lecture 6SCIPY – SIGNAL_00:03_
> Lecture 7SCIPY – OPTIMIZE_00:02_
> Lecture 8SCIPY – INTEGRATE_00:04_
> Lecture 9SCIPY – FFTPACK_00:07_
> Case Study 1 – NumPy
> Module 4 – Quiz
> ## Module 5 Data Manipulation Using Pandas  
> Lecture 1 – Introduction To Pandas_00:06_
> Lecture 2 – Series Object In Pandas_00:05_
> Lecture 3 – DataFrame In Pandas_00:08_
> Lecture 4 – Merge, Join And Concatenate_00:14_
> Lecture 5 – Importing And Analyzing Data Set_00:05_
> Lecture 6 – Cleaning The Data Set_00:06_
> Lecture 7 – Manipulating The Data Set_00:07_
> Lecture 8 – Visualizing The Data Set_00:04_
> Case Study 1 – Pandas
> Module 5 – Quiz
> #### Module 6 Data Visualization Using Matplotlib
> Lecture 1 – What Is Data Visualization?_00:03_
> Lecture 2 – Introduction To Matplotlib_00:02_
> Lecture 3 – How To Create A Line Plot?_00:09_
> Lecture 4 – How To Create A Bar Plot?_00:04_
> Lecture 5 – How To Create A Scatter Plot?_00:06_
> Lecture 6 – How To Create A Histogram?_00:05_
> Lecture 7 – How To Create A Box And Violin Plot?_00:04_
> Lecture 8 – How To Create A Pie Chart And Doughnut Chart?_00:07_
> Lecture 9 – How To Create An Area Chart?_00:03_
> Lecture 10 – Visualization On Data Set_00:10_
> Case Study 1 – Data Visualization
> Module 6 – Matplotlib : Quiz


## Module 7A - Concept Of OOPS In Python
### Lecture 1 – Agenda

### Lecture 2 – Introduction To OOPs
Object-Oriented Programming is a programming paradigm where you can use a real world entity which is called an Object.  *(mapping a real world object in code)*

Example: Parrot
Attribute: Name, Age, Color
Behavior: Singing, Dancing

  
### Lecture 3 – Real-World OOPs Example

Considering Human Being is a **class** (blueprint to create objects)

Common body features and functions are Class Attributes
Every human has: ears, nose

Polymorphism - being able to perform many tasks at the same time


### Lecture 4 – OOPs Classes And Objects

Class is a blueprint for an object and the objects are defined and created from classes(blueprint)

**Class** (ex: House Blueprint) (**Definition** of how house should be like)
Object (ex: The finished house) (concrete implementation of the blueprint )

- Object is the basic unit of object-oriented programming
- An object represents a particular instance of a class
- There can be more than one instance of an object
- Each instance of an object can hold its own relevant data
- Objects with similar properties and methods are grouped together to form a Class







