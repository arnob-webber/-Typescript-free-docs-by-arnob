---
title: Unknown type
sidebar:
  order: 45
  label: 45. Unknown type
---


In TypeScript, the `unknown` type represents a value that is of an unknown type. Unlike `any` type, which allows for any type of value, `unknown` requires a type check or assertion before it can be used in a specific way so no operations are permitted on an `unknown` without first asserting or narrowing to a more specific type.

The `unknown` type is only assignable to any type and the `unknown` type itself, it is a type-safe alternative to `any`.


```typescript
let value: unknown;

let value1: unknown = value; 
let value2: any = value; 
let value3: boolean = value; 
let value4: number = value; 
```

```typescript
const add = (a: unknown, b: unknown): number | undefined =>
    typeof a === 'number' && typeof b === 'number' ? a + b : undefined;
console.log(add(1, 2)); 
console.log(add('x', 2)); 
```

