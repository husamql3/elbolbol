# TypeScript

<!-- markdownlint-disable MD033 -->

<details>
<summary>What are the key differences between TypeScript and JavaScript?</summary>

TypeScript is a statically typed superset of JavaScript. It adds types, interfaces, and compile-time type checking, which JavaScript lacks. TypeScript transpiles to plain JavaScript, making it compatible with any JavaScript environment.

</details>

<details>
<summary>Why do we need TypeScript?</summary>

TypeScript helps catch errors at compile time, offers better tooling (autocomplete, refactoring), and ensures more maintainable and scalable code by enforcing strict typing rules.

</details>

<details>
<summary>What types exist in TypeScript?</summary>

TypeScript supports primitive types like `string`, `number`, `boolean`, `undefined`, `null`, `symbol`, and `bigint`. It also supports complex types like `arrays`, `tuples`, `enums`, `any`, `unknown`, `void`, `never`, `objects`, and `union` and `intersection` types

</details>

<details>
<summary>What is the difference between <code>type</code> and <code>interface</code>?</summary>

`type` and `interface` both allow you to define custom types, but `interface` is better suited for defining shapes of objects, while `type` can handle more complex types such as unions and tuples.

</details>

<details>
<summary>What is your opinion on <code>JSDoc</code> as an alternative to TypeScript?</summary>

JSDoc is a documentation tool that can annotate types in JavaScript, but it doesn't offer the same `compile-time` safety as TypeScript. JSDoc lacks many features TypeScript has, such as static analysis, which ensures code correctness before execution.

</details>

<details>
<summary>What are union types in TypeScript? Give an example.</summary>

A union type allows a value to be one of several types. It uses the `|` operator to combine types `type CustomType = string | number;`

</details>

<details>
<summary>How does TypeScript handle type assertions? Why should you use <code>as</code>?</summary>

Type assertions (using `as` or the angle bracket syntax) tell the TypeScript compiler that you know the type better than it does. It's used when you're sure about the type but TypeScript cannot infer it correctly.

</details>

<details>
<summary>What is the difference between the <code>unknown</code> and <code>any</code> types?</summary>

`unknown` is safer than `any`. While `any` disables all type-checking, `unknown` forces you to perform type checks before manipulating the value.

</details>

<details>
<summary>What is the <code>never</code> type, and when would you use it?</summary>

The `never` type represents values that never occur. It's often used for functions that throw errors or infinite loops.

</details>

<details>
<summary>What is type narrowing, and how does TypeScript implement it?</summary>

Type narrowing occurs when TypeScript reduces the type of a variable to a more specific type using type guards, such as `typeof` or `instanceof`

</details>

<details>
<summary>What are generics in TypeScript, and how do they contribute to reusability?</summary>

Generics allow you to create reusable components or functions that work with any type, providing flexibility and type safety

</details>

<details>
<summary>How do generics constraints work? Why are they useful?</summary>

You can constrain generics to ensure they meet certain conditions, such as having certain properties

</details>

<details>
<summary>Describe conditional types and when they can be utilized</summary>

Conditional types allow you to define a type that depends on a condition — similar to a ternary operator (`condition ? trueType : falseType`), but for types

</details>

<details>
<summary>What is the difference between the utility types <code>Partial&lt;T&gt;</code> and <code>Pick&lt;T, K&gt;</code>?</summary>

`Partial<T>` makes all properties in `T` optional. `Pick<T, K>` extracts specific properties from `T`.

</details>

<details>
<summary>What does <code>keyof</code> do?</summary>

`keyof` creates a union of the keys of an object type

</details>

<details>
<summary>What are the discriminated unions, and how would you handle type-safe error handling with it?</summary>

A **discriminated union** is a TypeScript pattern where you combine multiple types into one union, and each member has a **common literal property** (the _discriminator_) that uniquely identifies which type it is.

</details>

<details>
<summary>What are template literal types, and how useful are they?</summary>

Template literal types allow you to create new string types by combining unions of string literals, increasing flexibility in working with string types.

</details>

<details>
<summary>What's the difference between <code>JSX.Element</code> and <code>React.ReactNode</code>?</summary>

`JSX.Element` refers to a React element returned by a component, while `React.ReactNode` includes anything renderable by React, like strings, numbers, or fragments

</details>
