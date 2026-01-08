---
title: Type Predicates
sidebar:
  order: 23
  label: 23. Type Predicates
---


Type Predicates in TypeScript are functions that return a boolean value and are used to narrow the type of a variable to a more specific type.

```typescript
const isString = (value: unknown): value is string => typeof value === 'string';

const announceActor = (name: unknown) => {
    if (isString(name)) {
        console.log(`Starring: ${name.toUpperCase()}`);
    } else {
        console.log('Unknown actor');
    }
};
```

