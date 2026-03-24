# JavaScript

<details>
<summary>Explain the concept of "hoisting" in JavaScript</summary>

Hoisting is a JavaScript mechanism where variable and function declarations are moved ("hoisted") to the top of their containing scope during the compile phase.

| Declaration | Accessing before declaration |
| --- | --- |
| `var foo` | `undefined` |
| `let foo` | `ReferenceError` |
| `const foo` | `ReferenceError` |
| `class Foo` | `ReferenceError` |
| `var foo = function() { ... }` | `undefined` |
| `function foo() { ... }` | Normal |
| `import` | Normal |

Hoisting is a JavaScript mechanism where variable and function declarations are moved ("hoisted") to the top of their containing scope during the compile phase.

```jsx
console.log(foo); // undefined
var foo = 1;
console.log(foo); // 1
```

```jsx
for (var i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 0);
}

// 3
// 3
// 3
```

</details>

<details>
<summary>What are the differences between variables created using `let`, `var` or `const`?</summary>

| Behavior | `var` | `let` | `const` |
| --- | --- | --- | --- |
| Scope | Function or Global | Block | Block |
| Initialization | Optional | Optional | Required |
| Redeclaration | Yes | No | No |
| Reassignment | Yes | Yes | No |
| Accessing before declaration | `undefined` | `ReferenceError` | `ReferenceError` |

</details>

<details>
<summary>What is the difference between `==` and `===` in JavaScript?</summary>

**`==`** is the abstract equality operator while **`===`** is the strict equality operator.

- **Equality operator (`==`)**

```jsx
console.log(42 == '42'); // true
console.log(0 == false); // true
console.log(null == undefined); // true
console.log([] == false); // true
console.log('' == false); // true
```

- **Strict equality operator (`===`)**

```jsx
console.log(42 === '42'); // false
console.log(0 === false); // false
console.log(null === undefined); // false
console.log([] === false); // false
console.log('' === false); // false

console.log([] === []); // flase
console.log({} === {}); // false
// Creating [] or {} always creates a brand new object → different reference → false.
```

</details>

<details>
<summary>What is the event loop in JavaScript runtimes?</summary>

The algorithm per tick:

1. Execute everything on the call stack until it's empty
2. Drain the **entire** `microtask` queue (including `microtasks` added during draining)
3. Pick **one** `macrotask` from the queue, push it to the call stack
4. Repeat

```jsx
console.log('1');

setTimeout(() => console.log('2'), 0);

Promise.resolve().then(() => console.log('3'));

console.log('4');

// Output: 1, 4, 3, 2
```

```jsx
Promise.resolve().then(() => {
  console.log('A');
  Promise.resolve().then(() => console.log('B'));
});

Promise.resolve().then(() => console.log('C'));

// Output: A, C, B
```

</details>

<details>
<summary>Explain event delegation in JavaScript</summary>

Event delegation is a technique in JavaScript where a single event listener is attached to a parent element instead of attaching event listeners to multiple child elements. When an event occurs on a child element, the event bubbles up the DOM tree, and the parent element's event listener handles the event based on the target element.

```jsx
// HTML:
// <ul id="item-list">
//   <li>Item 1</li>
//   <li>Item 2</li>
//   <li>Item 3</li>
// </ul>

const itemList = document.getElementById('item-list');

itemList.addEventListener('click', (event) => {
  if (event.target.tagName === 'LI') {
    console.log(`Clicked on ${event.target.textContent}`);
  }
});
```

- Use cases
  - Handling dynamic content in single-page applications
  - Simplifying code by avoiding the need to attach and remove event listeners for elements that change

</details>

<details>
<summary>Explain how `this` works in JavaScript</summary>

**`this`** is a keyword that refers to the current execution context of a function or script.

- **Used globally**
  In the global scope, **`this`** refers to the global object, which is the **`window`** object in a web browser or the **`global`** object in a Node.js environment.
- **Within a regular function call**
  When a function is called in the global context or as a standalone function, **`this`** refers to the global object (in non-strict mode) or **`undefined`** (in strict mode).
- **Within a method call**
  When a function is called as a method of an object, **`this`** refers to the object that the method is called on.

```javascript
const obj = {
  name: 'John',
  showThis: function () {
    console.log(this);
  },
};

obj.showThis(); // { name: 'John', showThis: ƒ }
```

- **Within a function constructor**
  When a function is used as a constructor (called with the **`new`** keyword), **`this`** refers to the newly-created instance. In the following example, **`this`** refers to the **`Person`** object being created, and the **`name`** property is set on that object.

```jsx
function Person(name) {
  this.name = name;
}

const person = new Person('John');
console.log(person.name); // "John"
```

- **Within class constructor and methods**
  In ES2015 classes, **`this`** behaves as it does in object methods. It refers to the instance of the class.

```jsx
class Person {
  constructor(name) {
    this.name = name;
  }

  showThis() {
    console.log(this);
  }
}

const person = new Person('John');
person.showThis(); // Person {name: 'John'}

const showThisStandalone = person.showThis;
showThisStandalone(); // `undefined` because in JavaScript class bodies, all methods are strict mode by default, even if you don't add 'use strict'
```

</details>

<details>
<summary>Describe the difference between a `cookie`, `sessionStorage` and `localStorage`</summary>

| Property | Cookie | `localStorage` | `sessionStorage` |
| --- | --- | --- | --- |
| Initiator | Client or server. Server can use `Set-Cookie` header | Client | Client |
| Lifespan | As specified | Until deleted | Until tab is closed |
| Persistent across browser sessions | If a future expiry date is set | Yes | No |
| Sent to server with every HTTP request | Yes, sent via `Cookie` header | No | No |
| Total capacity (per domain) | 4kb | 5MB | 5MB |
| Access | Across windows/tabs | Across windows/tabs | Same tab |
| Security | JavaScript cannot access `HttpOnly` cookies | None | None |

</details>

<details>
<summary>Describe the difference between `<script>`, `<script async>` and `<script defer>`</summary>

- **`<script>`**
  For normal **`<script>`** tags without any **`async`** or **`defer`**, when they are encountered, HTML parsing is blocked, the script is fetched and executed immediately. HTML parsing resumes after the script is executed. This can block rendering of the page if the script is large.
- **`<script async>`**
  In **`<script async>`**, the browser downloads the script file asynchronously (in parallel with HTML parsing) and executes it as soon as it is available (potentially before HTML parsing completes). The execution will not necessarily be executed in the order in which it appears in the HTML document. This can improve perceived performance because the browser doesn't wait for the script to download before continuing to render the page.
- **`<script defer>`**
  Similar to **`<script async>`**, **`<script defer>`** also downloads the script in parallel to HTML parsing but the script is only executed when the document has been fully parsed and before firing **`DOMContentLoaded`**. If there are multiple of them, each deferred script is executed in the order they appeared in the HTML document.

</details>

<details>
<summary>What's the difference between: `null`, `undefined` or undeclared?</summary>

| Trait | `null` | `undefined` | Undeclared |
| --- | --- | --- | --- |
| Meaning | Explicitly set by the developer to indicate that a variable has no value | Variable has been declared but not assigned a value | Variable has not been declared at all |
| Type (via `typeof` operator) | `'object'` | `'undefined'` | `'undefined'` |
| Equality Comparison | `null == undefined` is `true` | `undefined == null` is `true` | Throws a `ReferenceError` |

</details>

<details>
<summary>What's the difference between `.call` and `.apply` in JavaScript?</summary>

**`.call`** and **`.apply`** are both used to invoke functions with a specific **`this`** context and arguments. The primary difference lies in how they accept arguments:

- **`.call(thisArg, arg1, arg2, ...)`**: Takes arguments individually.
- **`.apply(thisArg, [argsArray])`**: Takes arguments as an array.

```jsx
function add(a, b) {
  return a + b;
}

console.log(add.call(null, 1, 2)); // 3
console.log(add.apply(null, [1, 2])); // 3
```

</details>

<details>
<summary>What is a closure, and how/why would you use one?</summary>

A closure is a function that retains access to these variables even after the outer function has finished executing. This is like the function has a memory of its original environment.

```jsx
function outerFunction() {
  const outerVar = 'I am outside of innerFunction';

  function innerFunction() {
    console.log(outerVar); // `innerFunction` can still access `outerVar`.
  }

  return innerFunction;
}

const inner = outerFunction(); // `inner` now holds a reference to `innerFunction`.

inner(); // "I am outside of innerFunction"
// Even though `outerFunction` has completed execution
// `inner` still has access to variables defined inside `outerFunction`.
```

</details>

<details>
<summary>What is the difference between a `Map` object and a `plain object` in JavaScript?</summary>

Both `Map` objects and plain objects in JavaScript can store key-value pairs, but they have several key differences:

| Feature | `Map` | Plain object |
| --- | --- | --- |
| Key type | Any data type | String (or Symbol) |
| Key order | Maintained | Not guaranteed |
| Size property | Yes (`size`) | None |
| Iteration | `forEach`, `keys()`, `values()`, `entries()` | `for...in`, `Object.keys()`, etc. |
| Inheritance | No | Yes |
| Performance | Generally better for larger datasets and frequent additions/deletions | Faster for small datasets and simple operations |
| Serializable | No | Yes |

</details>

<details>
<summary>Explain how prototypal inheritance works in JavaScript</summary>

Prototypical inheritance in JavaScript is a way for objects to inherit properties and methods from other objects. Every JavaScript object has a special hidden property called **`[[Prototype]]`** (commonly accessed via **`__proto__`** or using  **`Object.getPrototypeOf()`**) that is a reference to another object, which is called the object's "prototype".

```jsx
// Parent object constructor.
function Animal(name) {
  this.name = name;
}

// Add a method to the parent object's prototype.
Animal.prototype.makeSound = function () {
  console.log('The ' + this.constructor.name + ' makes a sound.');
};

// Child object constructor.
function Dog(name) {
  Animal.call(this, name); // Call the parent constructor.
}

// Set the child object's prototype to be the parent's prototype.
Object.setPrototypeOf(Dog.prototype, Animal.prototype);

// Add a method to the child object's prototype.
Dog.prototype.bark = function () {
  console.log('Woof!');
};

// Create a new instance of Dog.
const bolt = new Dog('Bolt');

// Call methods on the child object.
console.log(bolt.name); // "Bolt"
bolt.makeSound(); // "The Dog makes a sound."
bolt.bark(); // "Woof!"
```

</details>

<details>
<summary>What is the difference between `__proto__` vs `prototype`?</summary>

- **`prototype`** is a property that exists on **functions** (specifically constructor functions and classes). It's the object that will become the `__proto__` of any instance created with `new`.
- **`__proto__`** is a property that exists on **every object**. It points to the object's actual prototype in the prototype chain — i.e., the object it inherits from.

```jsx
function Dog(name) {
  this.name = name;
}

Dog.prototype.bark = function() {
  return 'Woof!';
};

const rex = new Dog('Rex');

// These are the same object:
rex.__proto__ === Dog.prototype  // true
```

So in short
`Dog.prototype` — "the blueprint I give to my instances"
`rex.__proto__` — "the blueprint I received from my constructor"

</details>

<details>
<summary>Explain the difference between mutable and immutable objects in JavaScript</summary>

- **Mutable objects** can be changed after creation. Most JavaScript objects, arrays, and Maps fall into this category
- **Immutable values** cannot be changed. All primitives (strings, numbers, booleans) are immutable — any "change" produces a new value:
- React decides whether to re-render by doing a **shallow comparison** (===) on state and props. It checks *references*, not deep equality.

```jsx
// BAD — same reference, React won't re-render
const handleClick = () => {
  items.push('new item');
  setItems(items); // same reference! React sees no change
};

// GOOD — new reference, React detects the change
const handleClick = () => {
  setItems([...items, 'new item']); // new array
};
```

</details>

<details>
<summary>Deep copy of `objects` inside `array`</summary>

- The Core Concept: Shallow vs Deep Copy

```jsx
const users = [
  { name: 'Ali', address: { city: 'Istanbul' } },
  { name: 'Veli', address: { city: 'Ankara' } },
];

// SHALLOW copy — nested objects still share references
const copy = [...users];
copy[0].address.city = 'Izmir';
console.log(users[0].address.city); // 'Izmir' — original mutated!
```

- structuredClone - the modern answer

```jsx
const deepCopy = structuredClone(users);
deepCopy[0].address.city = 'Izmir';
console.log(users[0].address.city); // 'Istanbul' — safe
```

- JSON round-trip

```jsx
const deepCopy = JSON.parse(JSON.stringify(users));
```

</details>

<details>
<summary>What are the pros and cons of using `Promises` instead of `callbacks` in JavaScript?</summary>

Promises offer a cleaner alternative to callbacks, helping to avoid callback hell and making asynchronous code more readable.

- Avoid callback hell which can be unreadable, Callback hell, also known as the "pyramid of doom," is a phenomenon that occurs when you have multiple nested callbacks in your code.

```jsx
function getFirstData(callback) {
  setTimeout(() => {
    callback({ id: 1, title: 'First Data' });
  }, 1000);
}

function getSecondData(data, callback) {
  setTimeout(() => {
    callback({ id: data.id, title: data.title + ' Second Data' });
  }, 1000);
}

// Callback hell
getFirstData((data) => {
  getSecondData(data, (data) => {
  console.log(result); // Output: {id: 1, title: "First Data Second Data Third Data"}
  });
});

```

- Makes it easy to write sequential asynchronous code that is readable with `.then()`.
- Easier error handling with `.catch()` and guaranteed cleanup with `.finally()`
- Makes it easy to write parallel asynchronous code with `Promise.all()`.

</details>

<details>
<summary>Promises - creation, chaining, error handling `Promise.all/race/allSettled`</summary>

1. Promise Creation
    - A Promise wraps an async operation. It's in one of three states: **pending**, **fulfilled**, or **rejected**. Once settled, it can't change.

```jsx
const fetchUser = (id) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (id > 0) resolve({ id, name: 'Ali' });
      else reject(new Error('Invalid ID'));
    }, 1000);
  });
};
```

- Key point: the executor function runs **synchronously** — only the callbacks are deferred. This is a common trick question.

```jsx
console.log('A');
new Promise(() => console.log('B')); // runs immediately
console.log('C');
// Output: A, B, C

console.log('1');
Promise.resolve().then(() => console.log('2'));
console.log('3');
// Output: 1, 3, 2
// .then() callbacks go to the microtask queue
```

1. **Chaining**
    - Each `.then()` returns a **new Promise**, which is what makes chaining work:

```jsx
fetchUser(1)
  .then(user => {
    console.log(user.name);   // 'Ali'
    return fetchPosts(user.id); // return a promise
  })
  .then(posts => {
    console.log(posts.length);
    return posts[0];            // return a plain value
  })
  .then(firstPost => {
    console.log(firstPost.title);
  });
```

- A classic trap question:

```jsx
// WRONG — creates parallel promises, doesn't chain
promise.then(doA);
promise.then(doB);

// RIGHT — sequential chain
promise.then(doA).then(doB);
```

1. **Error Handling**

Errors propagate down the chain until something catches them, like a try/catch:

```jsx
fetchUser(-1)
  .then(user => fetchPosts(user.id))
  .then(posts => console.log(posts))
  .catch(err => {
    // catches error from ANY step above
    console.error('Something failed:', err.message);
  })
  .finally(() => {
    // runs regardless — great for cleanup
    console.log('Loading done');
  });
```

1. **Static Methods — `Promise.all / race / allSettled / any`**
    - **`Promise.all`** — all must succeed, fails fast on first rejection
    Use case: parallel fetches where you need all results.

```jsx
const [user, posts, comments] = await Promise.all([
  fetchUser(1),
  fetchPosts(1),
  fetchComments(1),
]);
// If ANY one rejects, the whole thing rejects immediately
```

- **`Promise.race`** — first to settle wins (fulfilled OR rejected)
Use case: timeout patterns, performance racing.

```jsx
const result = await Promise.race([
  fetchData(),
  timeout(5000), // rejects after 5s
]);
// Whoever settles first determines the outcome
```

- **`Promise.allSettled`** — waits for ALL, never short-circuits
Use case: batch operations where partial failure is acceptable (sending emails, uploading files).

```jsx
const results = await Promise.allSettled([
  fetchUser(1),
  fetchUser(-1),  // this will reject
  fetchUser(2),
]);

// results:
// [
//   { status: 'fulfilled', value: { id: 1, ... } },
//   { status: 'rejected',  reason: Error('Invalid ID') },
//   { status: 'fulfilled', value: { id: 2, ... } },
// ]
```

- **`Promise.any`** — first to **fulfill** wins, ignores rejections:

```jsx
const fastest = await Promise.any([
  fetchFromCDN_A(),
  fetchFromCDN_B(),
  fetchFromCDN_C(),
]);
// Returns first success. Only rejects if ALL reject (AggregateError)
```

</details>

<details>
<summary>`setTimeout` vs `setInterval` — Behavior, Drift, Cleanup</summary>

- **`setTimeout`** — runs once after a delay:

```jsx
const id = setTimeout(() => {
  console.log('runs once');
}, 1000);

clearTimeout(id); // cancel it
```

- **`setInterval`** — runs repeatedly at an interval:

```jsx
const id = setInterval(() => {
  console.log('runs every second');
}, 1000);

clearInterval(id); // must clean up!
```

- The Drift Problem: `setInterval` doesn't guarantee exact timing — it schedules the **next callback** at the interval, regardless of how long the callback takes:

```jsx
// If callback takes 300ms and interval is 1000ms:
// Expected: 0ms, 1000ms, 2000ms, 3000ms
// Actual:   0ms, 1000ms, 2000ms, 3000ms  (looks fine)

// But if callback takes 1200ms:
// Calls start stacking or getting dropped
// Browsers will clamp overlapping calls
```

- Cleanup in React, Forgetting cleanup causes **memory leaks** and **state updates on unmounted components**. This is the most common React bug interviewers look for.

```jsx
useEffect(() => {
  const id = setInterval(() => {
    setCount(c => c + 1);
  }, 1000);

  return () => clearInterval(id); // cleanup on unmount
}, []);
```

</details>

<details>
<summary>What are Promises and how do they work?</summary>

Promises are a way to handle asynchronous operations in JavaScript. They provide a cleaner, more readable way to handle asynchronous code compared to traditional callback functions.

</details>
