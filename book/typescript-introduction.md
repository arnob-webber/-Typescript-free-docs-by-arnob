---
title: TypeScript Introduction
sidebar:
  order: 7
  label: 7. TypeScript Introduction
---


### What is TypeScript?

TypeScript is a strongly typed programming language that builds on JavaScript. It was originally designed by Anders Hejlsberg in 2012 and is currently developed and maintained by Microsoft as an open source project.

TypeScript compiles to JavaScript and can be executed in any JavaScript runtime (e.g., a browser or server Node.js).

TypeScript supports multiple programming paradigms such as functional, generic, imperative, and object-oriented. TypeScript is neither an interpreted nor a compiled language.

### Why TypeScript?

TypeScript is a strongly typed language that helps prevent common programming mistakes and avoid certain kinds of run-time errors before the program is executed.

A strongly typed language allows the developer to specify various program constraints and behaviors in the data type definitions, facilitating the ability to verify the correctness of the software and prevent defects. This is especially valuable in large-scale applications.

Some of the benefits of TypeScript:

* Static typing, optionally strongly typed
* Type Inference
* Access to ES6 and ES7 features
* Cross-Platform and Cross-browser Compatibility
* Tooling support with IntelliSense

### TypeScript and JavaScript

TypeScript is written in `.ts` or `.tsx` files, while JavaScript files are written in `.js` or `.jsx`.

Files with the extension `.tsx` or `.jsx` can contain JavaScript Syntax Extension JSX, which is used in React for UI development.

TypeScript is a typed superset of JavaScript (ECMAScript 2015) in terms of syntax. All JavaScript code is valid TypeScript code, but the reverse is not always true.

For instance, consider a function in a JavaScript file with the `.js` extension, such as the following:


```typescript
const sum = (a, b) => a + b;
```

The function can be converted and used in TypeScript by changing the file extension to `.ts`. However, if the same function is annotated with TypeScript types, it cannot be executed in any JavaScript runtime without compilation. The following TypeScript code will produce a syntax error if it is not compiled:


```typescript
const sum = (a: number, b: number): number => a + b;
```

TypeScript was designed to detect possible exceptions that can occur at runtime during compilation time by having the developer define the intent with type annotations. In addition, TypeScript can also catch issues if no type annotation is provided. For instance, the following code snippet does not specify any TypeScript types:


```typescript
const items = [{ x: 1 }, { x: 2 }];
const result = items.filter(item => item.y);
```

In this case, TypeScript detects an error and reports:

```text
Property 'y' does not exist on type '{ x: number; }'.
```

TypeScript's type system is largely influenced by the runtime behavior of JavaScript. For example, the addition operator (+), which in JavaScript can either perform string concatenation or numeric addition, is modeled in the same way in TypeScript:

```typescript
const result = '1' + 1; 
```

The team behind TypeScript has made a deliberate decision to flag unusual usage of JavaScript as errors. For instance, consider the following valid JavaScript code:


```typescript
const result = 1 + true; 
```

However, TypeScript throws an error:

```text
Operator '+' cannot be applied to types 'number' and 'boolean'.
```

This error occurs because TypeScript strictly enforces type compatibility, and in this case, it identifies an invalid operation between a number and a boolean.

### TypeScript Code Generation

The TypeScript compiler has two main responsibilities: checking for type errors and compiling to JavaScript. These two processes are independent of each other. Types do not affect the execution of the code in a JavaScript runtime, as they are completely erased during compilation. TypeScript can still output JavaScript even in the presence of type errors.
Here is an example of TypeScript code with a type error:


```typescript
const add = (a: number, b: number): number => a + b;
const result = add('x', 'y'); 
```

However, it can still produce executable JavaScript output:


```typescript
'use strict';
const add = (a, b) => a + b;
const result = add('x', 'y'); 
```

It is not possible to check TypeScript types at runtime. For example:


```typescript
interface Character {
    alias: string;
}
interface SuperHero extends Character {
    usePower: () => void;
}
interface Villain extends Character {
    scheme: () => void;
}
const battle = (character: Character) => {
    if (character instanceof SuperHero) {
        
        
    }
};
```

As the types are erased after compilation, there is no way to run this code in JavaScript. To recognize types at runtime, we need to use another mechanism. TypeScript provides several options, with a common one being "tagged union". For example:

```typescript
interface SuperHero {
    kind: 'hero'; 
    usePower: () => void;
}
interface Villain {
    kind: 'villain'; 
    scheme: () => void;
}
type Character = SuperHero | Villain;

const battle = (character: Character) => {
    if (character.kind === 'hero') {
        character.usePower();
    } else {
        character.scheme();
    }
};

const hero: SuperHero = {
    kind: 'hero',
    usePower: () => console.log('Saving the day!'),
};
battle(hero);
```

The property "kind" is a value that can be used at runtime to distinguish between objects in JavaScript.

It is also possible for a value at runtime to have a type different from the one declared in the type declaration. For instance, if the developer has misinterpreted an API type and annotated it incorrectly.

TypeScript is a superset of JavaScript, so the "class" keyword can be used as a type and value at runtime.

```typescript
class Character {
    constructor(public alias: string) {}
}
class SuperHero extends Character {
    constructor(
        public alias: string,
        public usePower: () => void
    ) {
        super(alias);
    }
}
class Villain extends Character {
    constructor(
        public alias: string,
        public scheme: () => void
    ) {
        super(alias);
    }
}
type MetaHuman = SuperHero | Villain;

const battle = (meta: MetaHuman) => {
    if (meta instanceof SuperHero) {
        meta.usePower();
    } else {
        meta.scheme();
    }
};

const hero = new SuperHero('Batman', () => console.log('I am Batman'));
battle(hero);
```

In JavaScript, a "class" has a "prototype" property, and the "instanceof" operator can be used to test if the prototype property of a constructor appears anywhere in the prototype chain of an object.

TypeScript has no effect on runtime performance, as all types will be erased. However, TypeScript does introduce some build time overhead.

### Modern JavaScript Now (Downleveling)

TypeScript can compile code to any released version of JavaScript since ECMAScript 3 (1999). This means that TypeScript can transpile code from the latest JavaScript features to older versions, a process known as Downleveling. This allows the usage of modern JavaScript while maintaining maximum compatibility with older runtime environments.

It's important to note that during transpilation to an older version of JavaScript, TypeScript may generate code that could incur a performance overhead compared to native implementations.

Here are some of the modern JavaScript features that can be used in TypeScript:

* ECMAScript modules instead of AMD-style "define" callbacks or CommonJS "require" statements.
* Classes instead of prototypes.
* Variables declaration using "let" or "const" instead of "var".
* "for-of" loop or ".forEach" instead of the traditional "for" loop.
* Arrow functions instead of function expressions.
* Destructuring assignment.
* Shorthand property/method names and computed property names.
* Default function parameters.

By leveraging these modern JavaScript features, developers can write more expressive and concise code in TypeScript.

