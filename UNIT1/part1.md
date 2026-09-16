# JavaScript Concepts

## Topics Covered

---

1. `var`, `let`, and `const`
2. Redeclaration and reassignment
3. Block scope
4. `const` with objects
5. Objects and object properties
6. Functions
7. Arrow functions
8. `for` loop
9. `setTimeout()`
10. `var` inside a loop with `setTimeout()`
11. `typeof` operator
12. Creating objects
13. Arrays
14. Array references
15. Reassignment vs modification
16. `push()` and `pop()`

---

# 1. `var`, `let`, and `const`

JavaScript provides three commonly used keywords for declaring variables:

```javascript
var
let
const
```

Example:

```javascript
var name = "xyz";

let rollno = 23;

const marks = 45;
```

Here:

- `name` is declared using `var`.
- `rollno` is declared using `let`.
- `marks` is declared using `const`.

---

## 1.1 `var`

A variable declared using `var` can be:

- declared
- reassigned
- redeclared

Example:

```javascript
var name = "navadeep";

var name = "abdullah";

console.log(name);
```

### Output

```text
abdullah
```

The second declaration changes the value of `name`.

### Important Point

`var` allows **redeclaration in the same scope**.

---

# 2. Reassignment

Reassignment means changing the value of an already declared variable.

Example:

```javascript
let rollno = 23;

rollno = 45;

console.log(rollno);
```

### Output

```text
45
```

The variable was declared once, and its value was changed later.

---

## 2.1 Reassignment with `let`

```javascript
let rollno = 23;

rollno = 45;
```

This is allowed.

```text
23 → 45
```

---

## 2.2 Reassignment with `const`

```javascript
const marks = 45;

marks = 50;
```

This is **not allowed**.

A `const` variable cannot be reassigned.

---

# 3. Redeclaration vs Reassignment

These two terms are different.

### Redeclaration

Declaring the variable again:

```javascript
var name = "navadeep";

var name = "abdullah";
```

### Reassignment

Changing the value:

```javascript
let rollno = 23;

rollno = 45;
```

---

## Comparison

| Keyword | Redeclaration                | Reassignment   |
| ------- | ---------------------------- | -------------- |
| `var`   | ✅ Allowed                   | ✅ Allowed     |
| `let`   | ❌ Not allowed in same scope | ✅ Allowed     |
| `const` | ❌ Not allowed               | ❌ Not allowed |

---

# 4. Scope of `var`, `let`, and `const`

Consider the following code:

```javascript
var name = "aditya";
let rollno = 65;
if (true) {
  var name = "navadeep";
  let rollno = 23;
  const marks = 45;
}
console.log(name);
console.log(rollno);
console.log(marks);
```

There are two different scopes involved:

```text
Outside if block
       |
       v
    if block
       |
       v
  console.log(...)
```

---

## 4.1 `var` and Block Scope

`var` does not follow block scope in the same way that `let` and `const` do.

Inside the `if` block:

```javascript
var name = "navadeep";
```

This refers to the same function/global-scoped `name`.

Therefore:

```javascript
console.log(name);
```

prints:

```text
navadeep
```

---

## 4.2 `let` is Block Scoped

Outside:

```javascript
let rollno = 65;
```

Inside the block:

```javascript
let rollno = 23;
```

The inner `rollno` belongs to the `if` block.

Therefore, after the block:

```javascript
console.log(rollno);
```

prints:

```text
65
```

The value `23` existed only inside the block.

---

## 4.3 `const` is Also Block Scoped

Inside the block:

```javascript
const marks = 45;
```

`marks` exists only inside the `if` block.

Therefore:

```javascript
console.log(marks);
```

outside the block causes an error because `marks` is not accessible there.

---

## Key Takeaway

```text
var    → function scoped
let    → block scoped
const  → block scoped
```

A block can be created using `{ }`, for example:

```javascript
if (true) {
  // block
}
```

---

# 5. Redeclaring `let`

Consider:

```javascript
let rollno = 23;

let rollno = 45;
```

This is **not allowed in the same scope**.

It produces an error because `rollno` has already been declared.

However:

```javascript
let rollno = 23;

rollno = 45;
```

is allowed.

### Remember

```text
let → cannot redeclare
let → can reassign
```

---

# 6. `const` with Objects

Consider:

```javascript
const student = {
  name: "ayush raj",

  rollno: 23,

  marks: 45,
};

student.name = "soumili";

console.log(student);

console.log(student.name);
```

### Output

The object becomes:

```text
{
    name: "soumili",
    rollno: 23,
    marks: 45
}
```

and:

```text
soumili
```

---

## But `student` is declared using `const`. Why did the name change?

Because `const` prevents **reassignment of the variable**, but it does not make the object completely immutable.

This is allowed:

```javascript
student.name = "soumili";
```

because we are modifying a property of the existing object.

---

## What is not allowed?

This would be an error:

```javascript
student = {
  name: "abhay",

  rollno: 23,

  marks: 45,
};
```

Here, we are trying to make `student` refer to a completely new object.

---

## Important Difference

### Modifying a property

```javascript
student.name = "soumili";
```

✅ Allowed

### Reassigning the object

```javascript
student = {
  name: "abhay",
};
```

❌ Not allowed

---

# 7. Objects in JavaScript

An object stores related information using **key-value pairs**.

Example:

```javascript
const student = {
  name: "ayush raj",

  rollno: 23,

  marks: 45,
};
```

The object contains three properties:

| Property | Value         |
| -------- | ------------- |
| `name`   | `"ayush raj"` |
| `rollno` | `23`          |
| `marks`  | `45`          |

---

## 7.1 Accessing Object Properties

We can access a property using dot notation:

```javascript
console.log(student.name);
```

Output:

```text
ayush raj
```

Similarly:

```javascript
console.log(student.rollno);
```

Output:

```text
23
```

---

## 7.2 Modifying Object Properties

We can change an object's property:

```javascript
student.name = "soumili";
```

Now:

```javascript
console.log(student.name);
```

produces:

```text
soumili
```

---

# 8. Object Example – Vehicle Details

Another example discussed in class:

```javascript
const details = {
  vehicle: "car",
  model: "bmw",
  color: "black",
};
```

The object contains:

```text
vehicle → car
model   → bmw
color   → black
```

Properties can be modified:

```javascript
details.vehicle = "bike";

details.model = "audi";

details.color = "white";
```

The object is now:

```text
{
    vehicle: "bike",
    model: "audi",
    color: "white"
}
```

---

# 9. `typeof` Operator

JavaScript provides the `typeof` operator to determine the type of a value.

Example:

```javascript
console.log(typeof details);
```

Since `details` is an object:

```text
object
```

is printed.

---

## Example

```javascript
const details = {
  vehicle: "car",
  model: "bmw",
  color: "black",
};
console.log(typeof details);
```

### Output

```text
object
```

---

# 10. Functions

A function is a reusable block of code.

The code discussed in class:

```javascript
function add(a, b) {
  return a + b;
}
```

Here:

- `add` → function name
- `a` and `b` → parameters
- `return a + b` → returns the result

---

## Calling the Function

```javascript
console.log(add(10, 20));
```

Output:

```text
30
```

---

## Function Structure

```javascript
function functionName(parameters) {
  // code

  return value;
}
```

Example:

```javascript
function add(a, b) {
  return a + b;
}
```

---

# 11. Arrow Functions

JavaScript also provides arrow-function syntax.

The equivalent of the previous function can be written as:

```javascript
const add1 = (a, b) => {
  return a + b;
};
```

This is an **arrow function**.

Both can perform the same calculation.

---

## Calling the Arrow Function

```javascript
console.log(add1(10, 20));
```

Output:

```text
30
```

---

# 12. `for` Loop

A `for` loop is used to repeat a block of code.

Example:

```javascript
for (var i = 0; i < 5; i++) {
  console.log(i);
}
```

### Output

```text
0
1
2
3
4
```

---

## Understanding the Three Parts

```javascript
for (var i = 0; i < 5; i++)
```

### 1. Initialization

```javascript
var i = 0;
```

The loop starts with `i = 0`.

### 2. Condition

```javascript
i < 5;
```

The loop continues while the condition is true.

### 3. Increment

```javascript
i++;
```

After every iteration, `i` increases by 1.

---

# 13. `setTimeout()`

`setTimeout()` is used to execute a function after a specified amount of time.

Example:

```javascript
setTimeout(() => {
  console.log("Hello");
}, 1000);
```

Here:

```text
1000 milliseconds = 1 second
```

So `"Hello"` is printed after approximately 1 second.

---

## General Syntax

```javascript
setTimeout(function, delay);
```

Example:

```javascript
setTimeout(() => {
  console.log("Hello");
}, 1000);
```

---

# 14. `var` + `for` Loop + `setTimeout()`

Example:

```javascript
for (var i = 0; i < 5; i++) {
  setTimeout(() => {
    console.log(i);
  }, 1000);
}
```

This example is important because it combines:

- `var`
- `for` loop
- arrow function
- `setTimeout()`
- delayed execution
- scope/closure behavior

---

## What students may initially expect

A common expectation is:

```text
0
1
2
3
4
```

But this code prints:

```text
5
5
5
5
5
```

---

## Why?

The important thing is that `setTimeout()` does not immediately execute the callback.

The loop runs first.

During the loop:

```text
i = 0
i = 1
i = 2
i = 3
i = 4
```

Then the loop finishes.

After the last iteration:

```text
i = 5
```

Only after approximately 1 second do the callbacks execute.

Each callback accesses `i`.

Because `var` is used, the callbacks refer to the same variable.

At that time:

```text
i = 5
```

Therefore:

```text
5
5
5
5
5
```

---

## Visual Understanding

```text
Loop starts

i = 0 → setTimeout callback
i = 1 → setTimeout callback
i = 2 → setTimeout callback
i = 3 → setTimeout callback
i = 4 → setTimeout callback

Loop finishes

i = 5

        ↓
   Wait ~1 second
        ↓

Callback 1 → prints 5
Callback 2 → prints 5
Callback 3 → prints 5
Callback 4 → prints 5
Callback 5 → prints 5
```

---

# 15. Comparing `var` and `let` in the Loop

Changing `var` to `let` changes the behavior:

```javascript
for (let i = 0; i < 5; i++) {
  setTimeout(() => {
    console.log(i);
  }, 1000);
}
```

The result is:

```text
0
1
2
3
4
```

The important difference is that `let` is block scoped and the loop creates a separate binding for each iteration that the callback can observe.

---

## Comparison

### Using `var`

```javascript
for (var i = 0; i < 5; i++) {
  setTimeout(() => {
    console.log(i);
  }, 1000);
}
```

Output:

```text
5
5
5
5
5
```

### Using `let`

```javascript
for (let i = 0; i < 5; i++) {
  setTimeout(() => {
    console.log(i);
  }, 1000);
}
```

Output:

```text
0
1
2
3
4
```

---

# 16. Creating Objects Using a Function

Example:

```javascript
const createuser = (name, rollno, marks) => {
  return {
    name: name,
    rollno: rollno,
    marks: marks,
  };
};
```

The function creates and returns an object.

---

## Calling the Function

```javascript
console.log(createuser("ayush raj", 23, 45));
```

The returned object is:

```text
{
    name: "ayush raj",
    rollno: 23,
    marks: 45
}
```

---

## Why is this useful?

Instead of manually creating multiple objects:

```javascript
const student1 = {
  name: "Ayush",
  rollno: 23,
  marks: 45,
};

const student2 = {
  name: "Abhay",
  rollno: 24,
  marks: 50,
};
```

we can use a function:

```javascript
createuser("Ayush", 23, 45);
createuser("Abhay", 24, 50);
```

The function can create objects with different values.

---

# 17. Arrays

An array is used to store multiple values in a single variable.

Example:

```javascript
const arr1 = [1, 2, 3, 4, 5];
```

The array contains:

```text
Index:   0  1  2  3  4
Value:   1  2  3  4  5
```

---

## Accessing Array Elements

```javascript
console.log(arr1[0]);
```

Output:

```text
1
```

```javascript
console.log(arr1[2]);
```

Output:

```text
3
```

Remember that array indexing starts from `0`.

---

# 18. `push()` and `pop()`

Arrays provide methods to add and remove elements.

---

## `push()`

`push()` adds an element to the end of an array.

```javascript
const arr = [1, 2, 3];

arr.push(4);

console.log(arr);
```

Output:

```text
[1, 2, 3, 4]
```

---

## `pop()`

`pop()` removes the last element.

```javascript
const arr = [1, 2, 3, 4];

arr.pop();

console.log(arr);
```

Output:

```text
[1, 2, 3]
```

---

# 19. Array Assignment and References

Consider:

```javascript
const arr1 = [1, 2, 3, 4, 5];

const arr2 = arr1;
```

A common misunderstanding is:

> "`arr2` is a copy of `arr1`."

It is **not a new independent array**.

The assignment makes both variables refer to the same array.

Conceptually:

```text
arr1 ─────────┐
              ↓
        [1, 2, 3, 4, 5]
              ↑
arr2 ─────────┘
```

---

# 20. Reassigning an Array Variable

Consider:

```javascript
const arr1 = [1, 2, 3, 4, 5];

const arr2 = arr1;

arr2 = [];

console.log(arr1);

console.log(arr2);
```

The line:

```javascript
arr2 = [];
```

is attempting to reassign `arr2`.

But `arr2` was declared using:

```javascript
const
```

Therefore, this produces an error.

---

# 21. Reassignment vs Array Modification

This distinction is very important.

## Reassignment

```javascript
arr2 = [];
```

This means:

> Make `arr2` refer to another array.

With `const`, this is not allowed.

---

## Modification

```javascript
arr2.push(6);
```

This means:

> Modify the existing array.

For example:

```javascript
const arr1 = [1, 2, 3, 4, 5];

const arr2 = arr1;

arr2.push(6);

console.log(arr1);

console.log(arr2);
```

Both will show:

```text
[1, 2, 3, 4, 5, 6]
```

Why?

Because both variables refer to the same array.

```text
             ┌──────────────┐
arr1 ───────→│ 1 2 3 4 5 6  │
             └──────────────┘
                    ↑
arr2 ───────────────┘
```

---

# 22. `arr1` and `arr2` – Important Example

Consider:

```javascript
const arr1 = [1, 2, 3, 4, 5];

let arr2 = arr1;

arr2 = [];

console.log(arr1);

console.log(arr2);
```

Here `arr2` is declared using `let`, so reassignment is allowed.

Initially:

```text
arr1 ──────┐
           ↓
       [1,2,3,4,5]
           ↑
arr2 ──────┘
```

After:

```javascript
arr2 = [];
```

the reference changes:

```text
arr1 ─────→ [1,2,3,4,5]

arr2 ─────→ []
```

Therefore:

```text
arr1 = [1,2,3,4,5]

arr2 = []
```

The original array was not changed.

Only `arr2` was made to refer to a new array.

---

# 23. Modifying the Shared Array

Now consider:

```javascript
const arr1 = [1, 2, 3, 4, 5];

const arr2 = arr1;

arr2.push(6);

console.log(arr1);

console.log(arr2);
```

Output:

```text
[1, 2, 3, 4, 5, 6]

[1, 2, 3, 4, 5, 6]
```

Because both variables refer to the same array.

---

# 24. `pop()` with Shared Arrays

Similarly:

```javascript
const arr1 = [1, 2, 3, 4, 5];

const arr2 = arr1;

arr2.pop();

console.log(arr1);

console.log(arr2);
```

Output:

```text
[1, 2, 3, 4]

[1, 2, 3, 4]
```

`pop()` modifies the shared array.

---

# 25. Important Concept: Variable vs Value

When working with objects and arrays, distinguish between:

### Changing the variable's reference

```javascript
arr2 = [];
```

and:

### Changing the contents of the existing object/array

```javascript
arr2.push(6);
```

These are different operations.

---

---

# 28. Final Concept Map

```text
JavaScript
│
├── Variables
│   ├── var
│   ├── let
│   └── const
│
├── Scope
│   ├── Function Scope
│   └── Block Scope
│
├── Objects
│   ├── Create object
│   ├── Access properties
│   └── Modify properties
│
├── Functions
│   ├── Normal Function
│   └── Arrow Function
│
├── Loops
│   └── for loop
│
├── Asynchronous Execution
│   └── setTimeout()
│
├── Operators
│   └── typeof
│
└── Arrays
    ├── Create array
    ├── References
    ├── push()
    └── pop()
```

---

## Topics Covered

- `forEach()`
- `filter()`
- `map()`
- `sort()`
- `reduce()`
- `find()`
- `some()`
- `every()`
- Method chaining
- Working with arrays of objects

---

# 1. `forEach()`

The `forEach()` method is used to **iterate over every element of an array**.
It performs an action for each element.

## Example

```javascript
const arr8 = [1, 2, 3, 4, 5];

arr8.forEach((element) => {
  console.log(element);
});
```

### Output

```text
1
2
3
4
5
```

### How it works

```javascript
arr8.forEach((element) => {
  console.log(element);
});
```

Here:

- `arr8` → array on which `forEach()` is called
- `element` → current element
- `console.log(element)` → action performed for each element

So the callback function runs once for every element.

---

## `forEach()` with Index

We can also get the **index** of the current element.

```javascript
arr8.forEach((element, index) => {
  console.log(`element at index ${index} is ${element}`);
});
```

### Output

```text
element at index 0 is 1
element at index 1 is 2
element at index 2 is 3
element at index 3 is 4
element at index 4 is 5
```

The callback receives:

```text
(element, index)
```

---

## `forEach()` with Array

We can also access the complete array.

```javascript
arr8.forEach((element, index, array) => {
  console.log(
    `element at index ${index} is ${element} and the array is ${array}`,
  );
});
```

The callback can receive:

```text
(element, index, array)
```

---

## Calculating Sum Using `forEach()`

```javascript
let sum = 0;
arr8.forEach((element) => {
  sum += element;
});
console.log(`the sum of the array is ${sum}`);
```

### Output

```text
the sum of the array is 15
```

### Important Point

`forEach()` is mainly used when we want to **perform an action** on every element.

It does **not create a new array** from the callback result.

---

# 2. `filter()`

The `filter()` method is used to create a **new array containing only the elements that satisfy a condition**.

### Example

```javascript
const arr9 = [1, 2, 3, 4, 5];
const arr10 = arr9.filter((element) => {
  return element > 3;
});
console.log(arr10);
```

### Output

```text
[4, 5]
```

### How it works

The condition is:

```javascript
element > 3;
```

Each element is checked:

| Element | `element > 3` | Included? |
| ------: | :-----------: | :-------: |
|       1 |     false     |    ❌     |
|       2 |     false     |    ❌     |
|       3 |     false     |    ❌     |
|       4 |     true      |    ✅     |
|       5 |     true      |    ✅     |

Therefore:

```javascript
[4, 5];
```

is returned.

## Important Points

- `filter()` returns a **new array**.
- The original array is not changed by the filtering operation.
- The callback should return a condition (`true` or `false`).

---

# 3. How `filter()` Works Internally

Conceptually, `filter()` can be understood like this:

```javascript
const newArr = [];
for (let i = 0; i < arr.length; i++) {
  if (callback(arr[i], i, arr)) {
    newArr.push(arr[i]);
  }
}
return newArr;
```

The important idea is:

```text
Check → Condition true → Add element
Check → Condition false → Ignore element
```

---

# 4. `map()`

The `map()` method is used to create a **new array by transforming every element** of an existing array.

## Example

```javascript
const arr11 = [1, 2, 3, 4, 5];
const arr12 = arr11.map((element) => {
  return element * 2;
});

console.log(arr12);
```

### Output

```text
[2, 4, 6, 8, 10]
```

### How it works

| Original | Operation | New value |
| -------: | :-------: | --------: |
|        1 |  `1 * 2`  |         2 |
|        2 |  `2 * 2`  |         4 |
|        3 |  `3 * 2`  |         6 |
|        4 |  `4 * 2`  |         8 |
|        5 |  `5 * 2`  |        10 |

So:

```javascript
[1, 2, 3, 4, 5];
```

becomes:

```javascript
[2, 4, 6, 8, 10];
```

### Important Point

> `map()` = **Transform every element**

---

# 5. `filter()` vs `map()`

This is an important difference.

### `filter()`

Used when we want to **select some elements**.

```javascript
const result = arr.filter((element) => {
  return element > 3;
});
```

Result:

```text
[4, 5]
```

### `map()`

Used when we want to **transform every element**.

```javascript
const result = arr.map((element) => {
  return element * 2;
});
```

Result:

```text
[2, 4, 6, 8, 10]
```

### Easy way to remember

```text
filter → SELECT
map    → TRANSFORM
```

---

# 6. Array of Objects

JavaScript arrays can contain objects.

```javascript
const products = [
  {
    name: "laptop",
    price: 1000,
    category: "electronics",
  },
  {
    name: "phone",
    price: 500,
    category: "electronics",
  },
  {
    name: "tablet",
    price: 300,
    category: "electronics",
  },
  {
    name: "monitor",
    price: 800,
    category: "electronics",
  },
  {
    name: "keyboard",
    price: 1100,
    category: "electronics",
  },
];
```

We can access the properties of each product using:

```javascript
product.name;
product.price;
product.category;
```

---

# 7. `filter()` with Objects

Suppose we want products whose price is greater than `500`.

```javascript
const filteredProducts = products.filter((product) => {
  return product.price > 500;
});

console.log(filteredProducts);
```

The condition is:

```javascript
product.price > 500;
```

Products satisfying the condition:

```text
laptop    → 1000 ✅
phone     → 500  ❌
tablet    → 300  ❌
monitor   → 800  ✅
keyboard  → 1100 ✅
```

Therefore, the resulting array contains:

```text
laptop
monitor
keyboard
```

---

# 8. `sort()`

The `sort()` method is used to arrange array elements in a particular order.
`sort()` methode performs lexical sorting. Therefore,

For numbers, we commonly provide a comparison function.

## Ascending Order

```javascript
const sortedProducts = products
  .filter((product) => {
    return product.price > 500;
  })
  .sort((a, b) => {
    return a.price - b.price;
  });

console.log(sortedProducts);
```

The comparison:

```javascript
a.price - b.price;
```

sorts the products by price in **ascending order**.

### Result

The filtered products are:

```text
laptop    → 1000
monitor   → 800
keyboard  → 1100
```

After sorting:

```text
monitor   → 800
laptop    → 1000
keyboard  → 1100
```

### Easy Rule

```javascript
a.price - b.price;
```

→ Ascending order

```javascript
b.price - a.price;
```

→ Descending order

---

# 9. Method Chaining

JavaScript methods can be combined.

Example:

```javascript
const sortedProducts = products
  .filter((product) => {
    return product.price > 500;
  })
  .sort((a, b) => {
    return a.price - b.price;
  });
```

This performs two operations:

```text
products
   ↓
filter()
   ↓
Products with price > 500
   ↓
sort()
   ↓
Products sorted by price
```

This is called **method chaining**.

---

# 10. `map()` with Objects

We can also use `map()` to transform objects.

```javascript
const mappedProducts = products.map((product) => {
  return {
    name: product.name,
    price: product.price * 2,
  };
});

console.log(mappedProducts);
```

Here, every product is transformed.

For example:

```javascript
{
    name: "laptop",
    price: 1000
}
```

becomes:

```javascript
{
    name: "laptop",
    price: 2000
}
```

The same transformation happens for every product.

### Important

`map()` creates a **new array**.

---

# 11. `reduce()`

The `reduce()` method is used to **reduce an array to a single value**.

For example, we can calculate the total price of all products.

```javascript
const totalPrice = products.reduce((total, product) => {
  return total + product.price;
}, 0);

console.log(totalPrice);
```

### How it works

The initial value is:

```javascript
0;
```

Then:

```text
0 + 1000 = 1000
1000 + 500 = 1500
1500 + 300 = 1800
1800 + 800 = 2600
2600 + 1100 = 3700
```

Therefore:

```text
3700
```

is returned.

---

# 12. `reduce()` with Numbers

```javascript
const arr13 = [1, 2, 3, 4, 5];

const reduceSum = arr13.reduce((total, element) => {
  return total + element;
}, 0);

console.log(reduceSum);
```

### Output

```text
15
```

The process is:

```text
0 + 1 = 1
1 + 2 = 3
3 + 3 = 6
6 + 4 = 10
10 + 5 = 15
```

### Easy Way to Remember

```text
reduce → MANY VALUES → ONE VALUE
```

---

# 13. `find()`

The `find()` method is used to find the **first element** that satisfies a condition.

```javascript
const arr14 = [1, 2, 3, 4, 5];

const foundElement = arr14.find((element) => {
  return element > 3;
});

console.log(foundElement);
```

### Output

```text
4
```

Why?

The array is checked from left to right:

```text
1 > 3 → false
2 > 3 → false
3 > 3 → false
4 > 3 → true ✅
```

As soon as `4` satisfies the condition, `find()` returns it.

It does not continue looking for `5`.

### Important Point

If no element satisfies the condition:

```javascript
find();
```

returns:

```javascript
undefined;
```

---

# 14. `some()`

The `some()` method checks whether **at least one element** satisfies a condition.
Returns `true/false`

```javascript
const hasElement = arr14.some((element) => {
  return element > 3;
});

console.log(hasElement);
```

### Output

```text
true
```

Why?

Because:

```text
4 > 3 → true
```

At least one element satisfies the condition.

### Think of `some()` as:

> **"Is there at least one?"**

Example:

```javascript
[1, 2, 3, 4, 5];
```

Question:

> Is there at least one number greater than 3?

Answer:

```text
true
```

---

# 15. `every()`

The `every()` method checks whether **all elements** satisfy a condition.
Returns `true/false`

```javascript
const allElements = arr14.every((element) => {
  return element > 3;
});

console.log(allElements);
```

For:

```javascript
[1, 2, 3, 4, 5];
```

the condition is:

```javascript
element > 3;
```

But:

```text
1 > 3 → false ❌
```

Therefore, not every element satisfies the condition.

The result is:

```text
false
```

### Think of `every()` as:

> **"Does everyone satisfy the condition?"**

---

# 16. `some()` vs `every()`

This is an important difference.

Suppose:

```javascript
const arr = [1, 2, 3, 4, 5];
```

### `some()`

```javascript
arr.some((element) => element > 3);
```

Question:

> Is **at least one** element greater than 3?

Answer:

```text
true
```

### `every()`

```javascript
arr.every((element) => element > 3);
```

Question:

> Are **all** elements greater than 3?

Answer:

```text
false
```

### Easy way to remember

```text
some()  → At least ONE
every() → ALL
```

---

# 17. One Example to Understand All Methods

Consider:

```javascript
const marks = [45, 78, 32, 90, 65];
```

### `forEach()`

Print every mark:

```javascript
marks.forEach((mark) => {
  console.log(mark);
});
```

### `filter()`

Find marks greater than 50:

```javascript
const passed = marks.filter((mark) => {
  return mark > 50;
});
```

Result:

```text
[78, 90, 65]
```

### `map()`

Add 5 marks to every student:

```javascript
const updatedMarks = marks.map((mark) => {
  return mark + 5;
});
```

### `reduce()`

Calculate total marks:

```javascript
const total = marks.reduce((sum, mark) => {
  return sum + mark;
}, 0);
```

### `find()`

Find the first mark greater than 80:

```javascript
const result = marks.find((mark) => {
  return mark > 80;
});
```

Result:

```text
90
```

### `some()`

Check if at least one student scored above 80:

```javascript
const result = marks.some((mark) => {
  return mark > 80;
});
```

Result:

```text
true
```

### `every()`

Check if every student scored above 30:

```javascript
const result = marks.every((mark) => {
  return mark > 30;
});
```

Result:

```text
true
```

---

# 18. The Most Important Concept

When deciding which array method to use, ask:

### Do I just want to perform an action?

Use:

```javascript
forEach();
```

### Do I want only some elements?

Use:

```javascript
filter();
```

### Do I want to transform every element?

Use:

```javascript
map();
```

### Do I want one final result?

Use:

```javascript
reduce();
```

### Do I want the first matching element?

Use:

```javascript
find();
```

### Do I want to know if at least one matches?

Use:

```javascript
some();
```

### Do I want to know if all match?

Use:

```javascript
every();
```

### Do I want to arrange the elements?

Use:

```javascript
sort();
```

---

# 📘 JavaScript — Mutation and Immutability

This document explains the concepts of **mutation** and **immutability** in JavaScript, with examples using arrays and objects.

These concepts are especially important when working with **arrays, objects, functions, and React state**.

---

# Topics Covered

- What is mutation?
- What is immutability?
- Mutation with arrays
- Mutation with objects
- Reassignment vs mutation
- `push()` and `pop()`
- Creating new arrays using `filter()`
- Creating new arrays using `map()`
- Creating copies using spread syntax
- Mutation using `sort()`
- Comparing arrays and objects
- Why immutability is important in React
- Quick revision

---

# 1. What is Mutation?

**Mutation** means changing the existing value or data structure.

For example, if we have an array:

```javascript
const arr = [1, 2, 3];
```

and then add an element to the same array:

```javascript
arr.push(4);
```

the original array has been changed.

Before:

```text
[1, 2, 3]
```

After:

```text
[1, 2, 3, 4]
```

This is called **mutation**.

### Simple Definition

> Mutation = changing the existing data.

---

# 2. What is Immutability?

**Immutability** means we do not directly change the existing data.

Instead, we create a **new value** containing the required changes.

For example:

```javascript
const arr = [1, 2, 3];

const newArr = [...arr, 4];
```

Now:

```text
arr    → [1, 2, 3]
newArr → [1, 2, 3, 4]
```

The original array remains unchanged.

### Simple Definition

> Immutability = keep the original data unchanged and create a new value.

---

# 3. `const` Does NOT Mean Immutable

This is a very important concept.

Students often think:

```javascript
const arr = [1, 2, 3];
```

means that the array cannot be changed.

That is not completely correct.

With `const`, we cannot **reassign the variable**.

For example:

```javascript
const arr = [1, 2, 3];

arr = [4, 5, 6]; // ❌ Error
```

But we can still modify the contents of the array:

```javascript
arr.push(4); // ✅ Allowed
```

Now:

```text
[1, 2, 3, 4]
```

Therefore:

```text
const → prevents reassignment
const → does NOT automatically make objects/arrays immutable
```

---

# 4. Reassignment vs Mutation

These are different concepts.

Suppose:

```javascript
const arr = [1, 2, 3];
```

### Reassignment

Trying to make `arr` refer to another array:

```javascript
arr = [4, 5, 6];
```

This is **reassignment**.

With `const`, it gives an error.

---

### Mutation

Changing the existing array:

```javascript
arr.push(4);
```

This is **mutation**.

The variable still refers to the same array.

---

# 5. Array Mutation Using `push()`

The `push()` method adds an element to the existing array.

```javascript
const arr = [1, 2, 3];
arr.push(4);
console.log(arr);
```

Output:

```text
[1, 2, 3, 4]
```

The original array was modified.

Therefore:

```text
push() → mutates the array
```

---

# 6. Array Mutation Using `pop()`

The `pop()` method removes the last element from an array.

```javascript
const arr = [1, 2, 3, 4];
arr.pop();
console.log(arr);
```

Output:

```text
[1, 2, 3]
```

Again, the existing array was changed.

Therefore:

```text
pop() → mutates the array
```

---

# 7. Creating a New Array Instead of Mutating

Suppose:

```javascript
const arr = [1, 2, 3];
```

Instead of:

```javascript
arr.push(4);
```

we can create a new array:

```javascript
const newArr = [...arr, 4];
```

Now:

```javascript
console.log(arr);
console.log(newArr);
```

Output:

```text
[1, 2, 3]
[1, 2, 3, 4]
```

The original array has not changed.

This is an example of an **immutable approach**.

---

# 8. Spread Syntax and Immutability

The spread operator:

```javascript
...
```

can be used to create a new array containing the elements of an existing array.

Example:

```javascript
const arr1 = [1, 2, 3];

const arr2 = [...arr1];
```

Now:

```text
arr1 → [1, 2, 3]
arr2 → [1, 2, 3]
```

But they are separate array objects.

We can then create a modified version:

```javascript
const arr3 = [...arr1, 4];
```

Result:

```text
arr1 → [1, 2, 3]
arr3 → [1, 2, 3, 4]
```

---

# 9. `filter()` and Immutability

The `filter()` method creates a **new array**.

Example:

```javascript
const arr = [1, 2, 3, 4, 5];

const newArr = arr.filter((element) => {
  return element > 3;
});
```

Result:

```text
arr    → [1, 2, 3, 4, 5]
newArr → [4, 5]
```

The original array remains unchanged.

Therefore, `filter()` is commonly used when we want to create a new array based on a condition.

---

# 10. `map()` and Immutability

The `map()` method also creates a **new array**.

Example:

```javascript
const arr = [1, 2, 3, 4, 5];

const newArr = arr.map((element) => {
  return element * 2;
});
```

Result:

```text
arr    → [1, 2, 3, 4, 5]
newArr → [2, 4, 6, 8, 10]
```

The original array remains unchanged.

---

# 11. `reduce()` and Immutability

`reduce()` normally produces a single result rather than modifying the original array.

Example:

```javascript
const arr = [1, 2, 3, 4, 5];

const sum = arr.reduce((total, element) => {
  return total + element;
}, 0);

console.log(sum);
```

Output:

```text
15
```

The original array is still:

```text
[1, 2, 3, 4, 5]
```

---

# 12. `sort()` — Important Exception

Be careful with `sort()`.

Unlike `filter()` and `map()`, `sort()` **mutates the original array**.

Example:

```javascript
const numbers = [5, 2, 4, 1, 3];

numbers.sort((a, b) => {
  return a - b;
});

console.log(numbers);
```

Output:

```text
[1, 2, 3, 4, 5]
```

The original `numbers` array has been changed.

Therefore:

```text
sort() → mutates the original array
```

---

# 13. Sorting Without Mutating the Original Array

If we want to preserve the original array, first create a copy.

```javascript
const numbers = [5, 2, 4, 1, 3];

const sortedNumbers = [...numbers].sort((a, b) => {
  return a - b;
});
```

Now:

```text
numbers       → [5, 2, 4, 1, 3]

sortedNumbers → [1, 2, 3, 4, 5]
```

The original array is preserved.

### Pattern to Remember

```javascript
[...array].sort(...)
```

means:

```text
Create copy → Sort the copy
```

---

# 14. Mutation with Objects

Mutation can also happen with objects.

Consider:

```javascript
const student = {
  name: "Aman",
  marks: 80,
};
```

We can change the property:

```javascript
student.marks = 90;
```

Now:

```javascript
console.log(student);
```

Output:

```text
{
    name: "Aman",
    marks: 90
}
```

The original object was modified.

This is **mutation**.

---

# 15. Creating a New Object Instead

Instead of modifying the original object:

```javascript
const student = {
  name: "Aman",
  marks: 80,
};
```

we can create a new object:

```javascript
const updatedStudent = {
  ...student,
  marks: 90,
};
```

Now:

```text
student        → { name: "Aman", marks: 80 }

updatedStudent → { name: "Aman", marks: 90 }
```

The original object remains unchanged.

---

# 16. Array References

Consider:

```javascript
const arr1 = [1, 2, 3];

const arr2 = arr1;
```

It may look like we created a copy, but we did not.

Both variables refer to the **same array**.

Conceptually:

```text
arr1 ─────┐
          ↓
       [1, 2, 3]
          ↑
arr2 ─────┘
```

Now:

```javascript
arr2.push(4);
```

What happens?

```javascript
console.log(arr1);
console.log(arr2);
```

Both show:

```text
[1, 2, 3, 4]
```

Why?

Because `arr1` and `arr2` refer to the same array.

---

# 17. Creating an Actual Array Copy

Use spread syntax:

```javascript
const arr1 = [1, 2, 3];
const arr2 = [...arr1];
arr2.push(4);
```

Now:

```javascript
console.log(arr1);
console.log(arr2);
```

Output:

```text
[1, 2, 3]
[1, 2, 3, 4]
```

The arrays are separate.

---

# 18. Comparing Arrays

Consider:

```javascript
const arr1 = [1, 2, 3];
const arr2 = [1, 2, 3];
```

If we write:

```javascript
console.log(arr1 === arr2);
```

the result is:

```text
false
```

Even though they contain the same values.

Why?

Because arrays are objects, and the variables refer to different array objects.

---

# 19. Same Reference

Now consider:

```javascript
const arr1 = [1, 2, 3];
const arr2 = arr1;
console.log(arr1 === arr2);
```

Output:

```text
true
```

Both variables refer to the same array.

---

# 20. Mutation vs Immutability — Example

### Mutation

```javascript
const students = ["Aman", "Priya"];
students.push("Rahul");
```

Conceptually:

```text
Before:
students → ["Aman", "Priya"]

After:
students → ["Aman", "Priya", "Rahul"]
```

The same array was changed.

---

### Immutability

```javascript
const students = ["Aman", "Priya"];
const updatedStudents = [...students, "Rahul"];
```

Conceptually:

```text
students
    ↓
["Aman", "Priya"]

updatedStudents
    ↓
["Aman", "Priya", "Rahul"]
```

The original array remains unchanged.

---

# 22. Why Does Immutability Matter in React?

Immutability becomes especially important when working with **React state**.
For example, suppose we have:

```javascript
const [students, setStudents] = useState(["Aman", "Priya"]);
```

A poor approach would be:

```javascript
students.push("Rahul");
```

This directly mutates the existing state array.

Instead, create a new array:

```javascript
setStudents([...students, "Rahul"]);
```

The idea is:

```text
Old state
["Aman", "Priya"]

        ↓

Create new array

        ↓

New state
["Aman", "Priya", "Rahul"]
```

This gives React a new state value/reference to work with.

---

# 23. Updating an Object in React

Suppose:

```javascript
const [student, setStudent] = useState({
  name: "Aman",
  marks: 80,
});
```

Instead of directly changing:

```javascript
student.marks = 90; // ❌
```

create a new object:

```javascript
setStudent({
  ...student,
  marks: 90,
});
```

This preserves the immutable-update approach.

---

# 24. Removing an Element Immutably

Suppose:

```javascript
const students = ["Aman", "Priya", "Rahul"];
```

Instead of using:

```javascript
students.splice(1, 1);
```

we can use `filter()`:

```javascript
const updatedStudents = students.filter((student) => {
  return student !== "Priya";
});
```

Result:

```text
students:
["Aman", "Priya", "Rahul"]

updatedStudents:
["Aman", "Rahul"]
```

The original array remains unchanged.

---

# 25. Common Mutating Array Methods

Some commonly used array methods can modify the original array.

Examples:

```text
push()
pop()
shift()
unshift()
splice()
sort()
reverse()
```

When immutability is required, be careful when using these methods.

---

# 26. Common Non-Mutating Approaches

Methods such as these generally create a new result instead of changing the original array:

```text
map()
filter()
slice()
concat()
```

The spread operator can also be used to create a new array:

```javascript
const newArr = [...oldArr];
```

---

# 27. Important Difference: Copying vs Sharing

### Sharing the same array

```javascript
const arr1 = [1, 2, 3];

const arr2 = arr1;
```

```text
arr1 ────┐
         ↓
      [1,2,3]
         ↑
arr2 ────┘
```

Both refer to the same array.

---

### Creating a new array

```javascript
const arr1 = [1, 2, 3];

const arr2 = [...arr1];
```

```text
arr1 → [1,2,3]

arr2 → [1,2,3]
```

They contain the same values but are different arrays.

---

# ⭐ Final Takeaway

The most important distinction is:

```text
MUTATION
→ Change the existing data


IMMUTABILITY
→ Don't change the existing data
→ Create a new value instead
```

And remember:

```text
const ≠ immutable
```

`const` prevents **reassignment**, but objects and arrays declared with `const` can still be mutated.

For React, prefer the immutable approach when updating state:

```javascript
setStudents([...students, newStudent]);
```

and:

```javascript
setStudent({
  ...student,
  marks: 95,
});
```
