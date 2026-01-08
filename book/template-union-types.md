---
title: Template Union Types
sidebar:
  order: 43
  label: 43. Template Union Types
---


Template union types can be used to merge and manipulate text inside the type system for instance:

```typescript
type Status = 'active' | 'inactive';
type Products = 'p1' | 'p2';
type ProductId = `id-${Products}-${Status}`; 
```

