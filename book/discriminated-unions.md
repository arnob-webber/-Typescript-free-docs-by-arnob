---
title: Discriminated Unions
sidebar:
  order: 24
  label: 24. Discriminated Unions
---


Discriminated Unions in TypeScript are a type of union type that uses a common property, known as the discriminant, to narrow down the set of possible types for the union.

```typescript
type Square = {
    kind: 'square'; 
    size: number;
};

type Circle = {
    kind: 'circle'; 
    radius: number;
};

type Shape = Square | Circle;

const area = (shape: Shape) => {
    switch (shape.kind) {
        case 'square':
            return Math.pow(shape.size, 2);
        case 'circle':
            return Math.PI * Math.pow(shape.radius, 2);
    }
};

const square: Square = { kind: 'square', size: 5 };
const circle: Circle = { kind: 'circle', radius: 2 };

console.log(area(square)); 
console.log(area(circle)); 
```

