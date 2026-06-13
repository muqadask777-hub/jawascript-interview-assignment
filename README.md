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

Output:

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

## A3. Explain the 8 JavaScript data types. What is type coercion — implicit vs explicit?

JavaScript has eight data types. Seven of them are primitive types, and one is a non-primitive type.

The primitive data types are Number, String, Boolean, Undefined, Null, Symbol, and BigInt.

The eighth data type is Object.

Type coercion means converting one data type into another.

Implicit coercion happens automatically.

```js
console.log("5" + 2);
```

Output:

```js
"52"
```

Explicit coercion happens when the developer performs the conversion manually.

```js
Number("123");
String(123);
Boolean(1);
```

I usually prefer explicit conversions because they make the code easier to understand and reduce unexpected behavior.

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

## A6. What is a function in JavaScript? Explain function declaration with syntax, hoisting behaviour, return values, and parameters.

A function is a reusable block of code that performs a specific task.

```js
function greet() {
  console.log("Hello World");
}
```

Functions can accept parameters.

```js
function greet(name) {
  console.log("Hello " + name);
}
```

Functions can also return values.

```js
function multiply(a, b) {
  return a * b;
}
```

Function declarations are hoisted, which means they can be called before their declaration in the code.

```js
sayHello();

function sayHello() {
  console.log("Hello");
}
```

I use functions regularly because they make code more organized, reusable, and easier to maintain.
