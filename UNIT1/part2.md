# JavaScript Concepts

## Topics Covered

---

1. Object destructuring
2. Extracting multiple object properties
3. Selecting specific properties using destructuring
4. Renaming variables during object destructuring
5. Nested object destructuring
6. Default values in object destructuring
7. Array destructuring
8. Skipping array elements
9. Swapping values using destructuring

---

1. What is Destructuring?

Destructuring is a JavaScript syntax used to extract values from an
object or an array and store those values in variables.

Instead of accessing every property separately:

```javascript
console.log(student.name);
console.log(student.rollNo);
console.log(student.branch);
console.log(student.cgpa);
```

we can extract the required values directly:

```javascript
const { name, rollNo, branch, cgpa } = student;
```

After this statement, the variables:

```text
name
rollNo
branch
cgpa
```

contain the corresponding values from the student object.

Easy Definition

Destructuring = unpacking values from an object or array into
variables.

2. Object Destructuring

Consider the following object:

```javascript
const student = {
  name: "Aman",
  rollNo: 12345,
  branch: "CSE",
  cgpa: 8.4,
};
```

Normally, we can access its properties using dot notation:

```javascript
console.log(student.name);
console.log(student.rollNo);
console.log(student.branch);
console.log(student.cgpa);
```

Output:

```text
Aman
12345
CSE
8.4
```

With destructuring, we can write and directly use the variables:

```javascript
const { name, rollNo, branch, cgpa } = student;

console.log(name);
console.log(rollNo);
console.log(branch);
console.log(cgpa);
```

Output:

```text
Aman
12345
CSE
8.4
```

3. Understanding the Syntax

The basic syntax for object destructuring is:

```javascript
const { property1, property2 } = object;
```

For example:

```javascript
const { name, rollNo, branch, cgpa } = student;
```

Think of it as:

student
|
├── name → name
├── rollNo → rollNo
├── branch → branch
└── cgpa → cgpa

The property names inside { } tell JavaScript which values to extract.

Important Point

For object destructuring, the variable names normally match the object
property names.

For example:

const { name } = student;

means:

Take the name property from student and create a variable called
name.

4. Destructuring Only the Required Properties

We do not have to extract every property.

Suppose:

```javascript
const student = {
  name: "Aman",
  rollNo: 12345,
  branch: "CSE",
  cgpa: 8.4,
};
```

If we only need rollNo and cgpa, we can write:

```javascript
const { rollNo, cgpa } = student;

console.log(rollNo);
console.log(cgpa);
```

Output:

```text
12345
8.4
```

The other properties are not extracted.

Important Point:
Destructuring allows us to select only the values we need.

5. Why Use Object Destructuring?

Without destructuring:

```javascript
console.log(student.name);
console.log(student.rollNo);
console.log(student.branch);
console.log(student.cgpa);
```

With destructuring:

```javascript
const { name, rollNo, branch, cgpa } = student;

console.log(name);
console.log(rollNo);
console.log(branch);
console.log(cgpa);
```

The second approach can make code shorter and easier to read when we
need to work with several properties.

6. Renaming Variables During Destructuring

Sometimes the property name is not the variable name we want to use.

Consider:

```javascript
const student = {
  name: "Aman",
  rollNo: 12345,
  branch: "CSE",
  cgpa: 8.4,
};
```

We can rename the extracted variables:

```javascript
const {
  name: studentName,
  rollNo: studentRollNo,
  branch: studentBranch,
  cgpa: studentCgpa,
} = student;

console.log(studentName);
console.log(studentRollNo);
console.log(studentBranch);
console.log(studentCgpa);
```

Output:

```text
Aman
12345
CSE
8.4
```

7. Understanding the Renaming Syntax

The syntax:

```javascript
const { name: studentName } = student;
```

does not mean that the object property name has been renamed.

It means:

Object property Variable created

name ───────→ studentName

Similarly:

const { rollNo: studentRollNo } = student;

means:

rollNo ───────→ studentRollNo

Important

The original object is still:

```javascript
{
  name: "Aman",
  rollNo: 12345,
  branch: "CSE",
  cgpa: 8.4
}
```

Only the local variable name changes.

8. Object Property Name vs Variable Name

Compare these two examples.

Same variable name

const { name } = student;

Here:

property name → variable name

Different variable name

const { name: studentName } = student;

Here:

property name → variable studentName

A useful way to remember the syntax is:

propertyName : newVariableName

9. Nested Objects

Objects can contain other objects.

Example:

```javascript
const user = {
  id: 7,
  profile: {
    fullName: "Priya Sharma",
    city: "Ludhiana",
  },
};
```

Here, profile itself is an object.

Conceptually:

user
|
├── id → 7
|
└── profile
|
├── fullName → "Priya Sharma"
└── city → "Ludhiana"

10. Accessing Nested Object Properties Normally

Without destructuring:

console.log(user.profile.fullName);
console.log(user.profile.city);

Output:

Priya Sharma
Ludhiana

Here:

user.profile.fullName

means:

user
↓
profile
↓
fullName

11. Nested Destructuring

We can directly extract properties from the nested profile object.

```javascript
const {
  profile: { fullName, city },
} = user;

console.log(fullName);
console.log(city);
```

Output:

```text
Priya Sharma
Ludhiana
```

How to Read This

const {
profile: { fullName, city }
} = user;

means:

Take profile from user
↓
Go inside profile
↓
Extract fullName and city

12. Nested Destructuring Visual

For:

```javascript
const user = {
  id: 7,
  profile: {
    fullName: "Priya Sharma",
    city: "Ludhiana"
  }
};

the destructuring:

const {
  profile: { fullName, city }
} = user;
```

can be visualized as:

user
|
└── profile
|
├── fullName ─────→ fullName
|
└── city ─────────→ city

The profile object itself is used as the path to reach the nested
properties.

13. Default Values in Object Destructuring

What happens if the object does not contain a property we try to
extract?

Example:

```javascript
const user = {
  name: "Sangam",
  city: "Varanasi",
};
```

There is no pincode property.

We can provide a default value:

```javascript
const { name, city, pincode = "123456" } = user;

console.log(name);
console.log(city);
console.log(pincode);
```

Output:

```text
Sangam
Varanasi
123456
```

14. How Default Values Work

Consider:

```javascript
const { pincode = "123456" } = user;
```

JavaScript checks whether user.pincode exists with a value other than
undefined.

If the property is missing:

pincode → "123456"

So the default value is used.

Easy Definition

A default value provides a fallback value when the extracted property
is undefined.

15. Default Value vs Existing Value

Suppose:

```javascript
const user = {
  name: "Sangam",
  city: "Varanasi",
  pincode: "221001",
};

const { pincode = "123456" } = user;
```

The result is:

```text
221001
```

The default "123456" is not used because the object already
provides a value.

Remember

Property exists with a value
↓
Use the object's value

Property is undefined/missing
↓
Use the default value

16. Array Destructuring

Destructuring is not limited to objects.

We can also destructure arrays.

Consider:

```javascript
const colors = ["red", "green", "blue"];

const [first, second] = colors;

console.log(first);
console.log(second);
```

Output:

```text
red
green
```

17. Array Destructuring is Position-Based

This is one of the most important differences between object and array
destructuring.

For an array:

const colors = ["red", "green", "blue"];

the positions are:

Index: 0 1 2
↓ ↓ ↓
Value: "red" "green" "blue"

When we write:

const [first, second] = colors;

JavaScript matches values according to their position:

first ← colors[0] ← "red"
second ← colors[1] ← "green"

Therefore:

first = "red"
second = "green"

Easy Rule

Object destructuring → property name based

Array destructuring → position based

18. Skipping an Array Element

Sometimes we do not need every array element.

Suppose:

```javascript
const colors = ["red", "green", "blue"];

If we want the first and third elements but not the second:

const [first, , third] = colors;

Notice the empty space between the commas.

Now:

console.log(first);
console.log(third);
```

Output:

red
blue

19. How Skipping Works

Consider:

const [first, , third] = colors;

The positions are matched like this:

colors:

Index 0 → "red"
Index 1 → "green"
Index 2 → "blue"

Destructuring:

[first, , third]
↓ ↓ ↓
red skip blue

The second position is intentionally skipped.

Important

const [first, , third] = colors;

does not create a variable for "green".

20. Object vs Array Destructuring

Feature Object Destructuring Array Destructuring

Syntax { } [ ]

Matching Property names Positions

Example const { name } = student const [first] = colors

Can skip values? Select only required Yes, using empty positions
properties

Nested values Supported Supported

Easy Memory Trick

Object → { } → key/property

Array → [ ] → position/index

21. Swapping Two Variables Using Destructuring

Consider:

let a = 10;
let b = 20;

console.log(a, b);

Output:

10 20

Suppose we want:

a = 20
b = 10

A traditional approach uses a temporary variable:

let temp = a;
a = b;
b = temp;

After swapping:

a = 20
b = 10

22. Swapping Using Array Destructuring

JavaScript allows us to swap the values directly using destructuring:

```javascript
let a = 10;
let b = 20;

[a, b] = [b, a];
console.log(a, b);
```

Output:

```text
20 10
```

Important Point:
No temporary variable is required.

23. Destructuring Does Not Modify the Original Object

Consider:

```javascript
const student = {
  name: "Aman",
  rollNo: 12345,
};

const { name, rollNo } = student;
```

Destructuring extracts values into variables.
It does not remove the properties from student.
The original object is still:

{
name: "Aman",
rollNo: 12345
}

So:

console.log(student);

still shows the original object.

Important Point:

Destructuring is an extraction/unpacking operation. It does not mean
deleting properties from the original object.

25. Final Concept Map

                    Destructuring
                         |
              ┌──────────┴──────────┐
              ↓                     ↓

    Object Destructuring Array Destructuring
    | |
    ┌──────┼──────┐ ┌─────┼─────┐
    ↓ ↓ ↓ ↓ ↓ ↓
    Extract Rename Nested Position Skip Swap
    | | |
    ↓ ↓ ↓
    Default Nested [ , ]
    Value Object
