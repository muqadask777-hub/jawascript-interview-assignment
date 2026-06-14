# JavaScript Interview Answers

## A1. What is the difference between var, let, and const in JavaScript?

In JavaScript, `var`, `let`, and `const` are all used to declare variables, but they work differently.

The biggest difference is scope. `var` is function-scoped, while `let` and `const` are block-scoped.

```js
if (true) {
  var a = 10;
  let b = 20;
  const c = 30;
}

console.log(a); // 10
```

In this example, `a` can still be accessed outside the block because `var` ignores block scope. However, `b` and `c` cannot be accessed outside the block.

Another important difference is hoisting. `var` is hoisted and initialized with `undefined`, while `let` and `const` stay in the Temporal Dead Zone until they are declared.

```js
console.log(x);
var x = 5;
```

##Output:

```js
undefined
```

But with `let` or `const`, JavaScript throws an error if they are accessed before declaration.

`var` can be re-declared and reassigned, `let` can be reassigned but not re-declared, and `const` cannot be reassigned after initialization.

Personally, I prefer using `const` by default because it makes the code safer. If I know a value will change later, I use `let`. I generally avoid `var` in modern JavaScript projects.

## A2. What is the V8 Engine? What does it mean that JavaScript is single-threaded?

The V8 Engine is Google's JavaScript engine that is used in Chrome and Node.js. Its job is to take JavaScript code and convert it into machine code so that the computer can execute it efficiently.

One reason V8 is fast is because it uses Just-In-Time (JIT) compilation. Instead of interpreting code line by line every time, it compiles code into optimized machine code while the program is running.

JavaScript is called single-threaded because it has only one main execution thread. This means it executes one task at a time.

```js
console.log("A");
console.log("B");
console.log("C");
```

Output:

```js
A
B
C
```

JavaScript executes statements in order using a call stack.

A common question is how JavaScript handles timers and API calls if it is single-threaded. The answer is that browsers provide Web APIs, and JavaScript uses the Event Loop to manage asynchronous operations.

```js
console.log("Start");

setTimeout(() => {
  console.log("Timer Done");
}, 2000);

console.log("End");
```

Output:

```js
Start
End
Timer Done
```

The timer runs outside the call stack, and once it finishes, its callback is placed in the queue. The Event Loop moves it back to the stack when JavaScript is ready to execute it.

So even though JavaScript is single-threaded, it can still handle asynchronous tasks very efficiently.
## A3 - JavaScript Data Types & Type Coercion

### JavaScript's 8 Data Types

JavaScript has **8 data types**: **7 primitive types** and **1 non-primitive type (Object)**.

#### Primitive Types
1. `String` – Represents text data.
2. `Number` – Represents integers and decimal numbers.
3. `BigInt` – Represents very large integers.
4. `Boolean` – Represents `true` or `false`.
5. `Undefined` – A variable declared but not assigned a value.
6. `Symbol` – Represents unique identifiers.
7. `Null` – Represents the intentional absence of a value.

#### Non-Primitive Type
8. `Object` – Used to store collections of data and more complex entities such as arrays, functions, and objects.

```js
let name = "Ali";       // String
let age = 20;           // Number
let big = 123n;         // BigInt
let isStudent = true;   // Boolean
let x;                  // Undefined
let id = Symbol("id");  // Symbol
let value = null;       // Null
let user = {};          // Object
```

### The Famous `typeof null` Bug

```js
console.log(typeof null); // "object"
```

Although `null` is a primitive data type, `typeof null` returns `"object"`. This is a historical bug from JavaScript's first version in 1995. It was never fixed because changing it would break older applications and affect backward compatibility.

### Type Coercion

Type coercion is the process of converting a value from one data type to another.

### Implicit Coercion (Automatic Conversion)

JavaScript automatically converts values when needed.

```js
console.log("5" + 2);  // "52"
console.log("10" - 3); // 7
```

In the first example, the number is converted to a string. In the second example, the string is converted to a number.

### Explicit Coercion (Manual Conversion)

The programmer intentionally converts values using built-in functions.

```js
console.log(Number("123")); // 123
console.log(String(456));   // "456"
console.log(Boolean(1));    // true
```

### `==` vs `===`

#### Loose Equality (`==`)

Performs type coercion before comparison.

```js
console.log("5" == 5); // true
```

#### Strict Equality (`===`)

Compares both value and data type without coercion.

```js
console.log("5" === 5); // false
```

### Why is `===` Safer?

- `==` can produce unexpected results because it automatically converts data types.
- `===` checks both type and value, making comparisons more predictable and reliable.

Therefore, `===` is generally recommended in modern JavaScript.

## A4. What is the difference between primitive and non-primitive (reference) data types in JavaScript? How are they stored in memory?

Primitive data types store a single value and are copied by value.

```js
let a = 10;
let b = a;

b = 20;
```

Changing `b` does not affect `a` because a separate copy was created.

Non-primitive types such as objects and arrays are stored differently. Variables store a reference to the actual data in memory.

```js
const user1 = {
  name: "Ali"
};

const user2 = user1;

user2.name = "Ahmed";
```

Both variables point to the same object, so changes are reflected in both places.

## A5. What is pass by value vs pass by reference? Is JavaScript truly pass by reference?

For primitive values, JavaScript uses pass by value.

```js
function update(num) {
  num = 50;
}

let number = 10;
update(number);
```

The original value remains unchanged because the function receives a copy.

With objects, JavaScript passes the reference value.

```js
function updateUser(user) {
  user.name = "Ahmed";
}
```

Many people call this pass by reference, but technically JavaScript is still pass by value because it passes a copy of the reference.

## A6 - Functions in JavaScript

### What is a Function?

A function is a reusable block of code that performs a specific task. It helps reduce code duplication, improves readability, and makes programs easier to maintain.

### Function Declaration Syntax

```js
function greet(name) {
  return `Hello, ${name}`;
}
```

### Parameters and Arguments

- **Parameter:** A variable defined in the function declaration.
- **Argument:** The actual value passed when calling the function.

```js
function greet(name) { // parameter
  return `Hello ${name}`;
}

greet("Ali"); // argument
```

### Hoisting

Function declarations are hoisted in JavaScript, meaning they can be called before they are defined in the code.

```js
sayHello();

function sayHello() {
  console.log("Hello");
}
```

### Return Values

A function returns a value using the `return` keyword.

```js
function add(a, b) {
  return a + b;
}
```

If no `return` statement is provided, JavaScript automatically returns `undefined`.

```js
function test() {}

console.log(test()); // undefined
```

### Real-World Example: Age Validation

```js
function isEligible(age) {
  return age >= 18;
}

console.log(isEligible(20)); // true
console.log(isEligible(15)); // false
```

### Functions are Objects

Functions are special objects in JavaScript.

```js
function demo() {}

console.log(typeof demo); // "function"
console.log(demo instanceof Object); // true
```

They also have built-in properties such as `.name` and `.length`.

```js
function greet(name) {}

console.log(greet.name);   // "greet"
console.log(greet.length); // 1
```
