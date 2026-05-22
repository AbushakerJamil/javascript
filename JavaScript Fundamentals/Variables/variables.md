# JavaScript Variables — Complete Guide

---

## 1. What is a Variable?

A variable is a **container** for storing a value — such as a number or a string of text.

```js
let sum = 10;
```

When this runs, the JavaScript engine allocates a space in your computer's **RAM**, stores `10` there, and labels that location `sum`. Whenever you reference `sum` later, the engine fetches the data from that memory location.

---

## 2. The 3 Forms: `var` vs `let` vs `const`

Before ES6 (2015), JavaScript only had `var`. Due to its quirky behavior, `let` and `const` were introduced in modern JavaScript.

---

### a) `var` — Old & Dangerous

| Property      | Description                                               |
| ------------- | --------------------------------------------------------- |
| **Scope**     | Function-scoped — accessible outside `if` or `for` blocks |
| **Redeclare** | Can be declared again with the same name (causes bugs)    |
| **Reassign**  | Value can be changed at any time                          |

---

### b) `let` — Modern & Safe

| Property      | Description                                 |
| ------------- | ------------------------------------------- |
| **Scope**     | Block-scoped — not accessible outside `{ }` |
| **Redeclare** | Cannot be re-declared in the same scope     |
| **Reassign**  | Value can be changed                        |

---

### c) `const` — Constant

| Property      | Description                                               |
| ------------- | --------------------------------------------------------- |
| **Scope**     | Block-scoped                                              |
| **Redeclare** | Cannot be re-declared in the same scope                   |
| **Reassign**  | Value cannot be changed — must be assigned at declaration |

> **Common Misconception:**
> Many people think `const` means the value can never change. That's only partially true.
> If you declare an **Object** or **Array** with `const`, you can still mutate its contents.
> Because `const` only locks the **memory reference**, not the inner values.

```js
const arr = [1, 2, 3, 4, 5];
arr.push(6); //  works fine

const user = { name: "Anik" };
user.name = "Zayan"; //  works fine
```

---

## 3. What is Hoisting?

Before JavaScript executes your code, it scans the entire file first. This is called the **Creation Phase**.

During this phase, variable declarations are moved to the **top of their scope** internally — this behavior is known as **Hoisting**.

### Hoisting with `var`

```js
console.log(a); // Output: undefined
var a = 10;
```

**Why `undefined`?**
Because `var` is hoisted and automatically initialized with `undefined`.

Internally, JavaScript sees it like this:

```js
var a = undefined; // hoisted to the top

console.log(a); // undefined

a = 10; // value is assigned
```

> `let` and `const` are also hoisted but are **not initialized**.
> Accessing them before declaration throws a **ReferenceError**.

---

## 4. Memory Management: Stack vs Heap

JavaScript stores data in two different memory locations depending on the data type.

|                 | Stack Memory                                                       | Heap Memory                                      |
| --------------- | ------------------------------------------------------------------ | ------------------------------------------------ |
| **Used for**    | Primitive Types (String, Number, Boolean, Undefined, Null, Symbol) | Reference Types (Object, Array, Function)        |
| **Size**        | Fixed                                                              | Can grow dynamically                             |
| **When copied** | Pass by Value — a brand new copy is created                        | Pass by Reference — the memory address is copied |

```js
// Stack — Pass by Value
let a = 5;
let b = a;
b = 10;
console.log(a); // 5 (unchanged)

// Heap — Pass by Reference
let obj1 = { name: "Anik" };
let obj2 = obj1;
obj2.name = "Zayan";
console.log(obj1.name); // "Zayan" (same reference!)
```

---

## 5. Global Variables & the `window` Object

If you declare a variable with `var` outside any function or block, it becomes a property of the browser's global object — `window`.

```js
var globalVar = "Hello";
console.log(window.globalVar); //  "Hello"

let globalLet = "Hi";
console.log(window.globalLet); //  undefined (let/const don't attach to window)
```

> **Bonus Tip:**
> If you accidentally declare a variable without any keyword (`var`/`let`/`const`), JavaScript silently makes it a global variable.
>
> ```js
> badVariable = "Oops"; //  very dangerous
> ```
>
> To prevent this, add **`"use strict"`** at the top of your file.

```js
"use strict";

badVariable = "Oops"; //  now throws a ReferenceError
```
