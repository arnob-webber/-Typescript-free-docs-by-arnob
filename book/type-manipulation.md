---
title: Type Manipulation
sidebar:
  order: 60
  label: 60. Type Manipulation
---


### Creating Types from Types

Is it possible to create new types composing, manipulating or transforming existing types.

Intersection Types (`&`):

Allow you to combine multiple types into a single  type:

```typescript
type Comic = { issue: number };
type Hero = { name: string };
type C = Comic & Hero; 
const obj: C = { issue: 42, name: 'Spider-Man' };
```

Union Types (`|`):

Allow you to define a type that can be one of several types:

```typescript
type Result = string | number;
const value1: Result = 'hello';
const value2: Result = 42;
```

Mapped Types:

Allow you to transform the properties of an existing type to create new type:

```typescript
type Mutable<T> = {
    readonly [P in keyof T]: T[P];
};
type Actor = {
    name: string;
    age: number;
};
type ImmutableActor = Mutable<Actor>; 
```

Conditional types:

Allow you to create types based on some conditions:

```typescript
type ExtractParam<T> = T extends (param: infer P) => any ? P : never;
type MyFunction = (name: string) => number;
type ParamType = ExtractParam<MyFunction>; 
```

### Indexed Access Types

In TypeScript is it possible to access and manipulate  the types of properties within another type using an index, `Type[Key]`.

```typescript
type Actor = {
    name: string;
    age: number;
};

type AgeType = Actor['age']; 
```

```typescript
type MyTuple = [string, number, boolean];
type MyType = MyTuple[2]; 
```

### Utility Types

Several built-in utility types can be used to manipulate types, below a list of the most common used:

#### Awaited\<T\>

Constructs a type that recursively unwraps Promise types.

```typescript
type A = Awaited<Promise<string>>; 
```

#### Partial\<T\>

Constructs a type with all properties of T set to optional.

```typescript
type Actor = {
    name: string;
    age: number;
};

type A = Partial<Actor>; 
```

#### Required\<T\>

Constructs a type with all properties of T set to required.

```typescript
type Actor = {
    name?: string;
    age?: number;
};

type A = Required<Actor>; 
```

#### Readonly\<T\>

Constructs a type with all properties of T set to readonly.


```typescript
type Actor = {
    name: string;
    age: number;
};

type A = Readonly<Actor>;

const a: A = { name: 'Ana de Armas', age: 35 };
a.name = 'Sydney Sweeney'; 
```

#### Record\<K, T\>

Constructs a type with a set of properties K of type T.

```typescript
type Movie = {
    title: string;
    revenue: number;
};

const movies: Record<string, Movie> = {
    madameWeb: { title: 'Madame Web', revenue: 0.5 },
    barbarella: { title: 'Barbarella', revenue: 0.25 },
};

console.log(movies.madameWeb); 
```

#### Pick\<T, K\>

Constructs a type by picking the specified properties K from T.

```typescript
type Movie = {
    title: string;
    revenue: number;
};

type Revenue = Pick<Movie, 'revenue'>; 
```

#### Omit\<T, K\>

Constructs a type by omitting the specified properties K from T.

```typescript
type Movie = {
    title: string;
    revenue: number;
};

type Title = Omit<Movie, 'revenue'>; 
```

#### Exclude\<T, U\>

Constructs a type by excluding all values of type U from T.

```typescript
type Union = 'a' | 'b' | 'c';
type MyType = Exclude<Union, 'a' | 'c'>; 
```

#### Extract\<T, U\>

Constructs a type by extracting all values of type U from T.

```typescript
type Union = 'a' | 'b' | 'c';
type MyType = Extract<Union, 'a' | 'c'>; 
```

#### NonNullable\<T\>

Constructs a type by excluding null and undefined from T.

```typescript
type Union = 'a' | null | undefined | 'b';
type MyType = NonNullable<Union>; 
```

#### Parameters\<T\>

Extracts the parameter types of a function type T.

```typescript
type Func = (a: string, b: number) => void;
type MyType = Parameters<Func>; 
```

#### ConstructorParameters\<T\>

Extracts the parameter types of a constructor function type T.

```typescript
class Actor {
    constructor(
        public name: string,
        public age: number
    ) {}
}
type ActorConstructorParams = ConstructorParameters<typeof Actor>; 
const params: ActorConstructorParams = ['Sydney Sweeney', 26];
const actor = new Actor(...params);
console.log(actor); 
```

#### ReturnType\<T\>

Extracts the return type of a function type T.

```typescript
type Func = (name: string) => number;
type MyType = ReturnType<Func>; 
```

#### InstanceType\<T\>

Extracts the instance type of a class type T.

```typescript
class Actor {
    name: string;

    constructor(name: string) {
        this.name = name;
    }

    sayHello() {
        console.log(`Hello, my name is ${this.name}!`);
    }
}

type ActorInstance = InstanceType<typeof Actor>;

const actor: ActorInstance = new Actor('Hania Amir');

actor.sayHello(); 
```

#### ThisParameterType\<T\>

Extracts the type of 'this' parameter from a function type T.

```typescript
interface Actor {
    name: string;
    greet(this: Actor): void;
}
type ActorThisType = ThisParameterType<Actor['greet']>; 
```

#### OmitThisParameter\<T\>

Removes the 'this' parameter from a function type T.

```typescript
function capitalize(this: String) {
    return this[0].toUpperCase + this.substring(1).toLowerCase();
}

type CapitalizeType = OmitThisParameter<typeof capitalize>; 
```

#### ThisType\<T\>

Servers as a market for a contextual `this` type.


```typescript
type Logger = {
    log: (error: string) => void;
};

let helperFunctions: { [name: string]: Function } & ThisType<Logger> = {
    hello: function () {
        this.log('some error'); 
        this.update(); 
    },
};
```

#### Uppercase\<T\>

Make uppercase the name of the input type T.

```typescript
type MyType = Uppercase<'abc'>; 
```

#### Lowercase\<T\>

Make lowercase the name of the input type T.

```typescript
type MyType = Lowercase<'ABC'>; 
```

#### Capitalize\<T\>

Capitalize the name of the input type T.

```typescript
type MyType = Capitalize<'abc'>; 
```

#### Uncapitalize\<T\>

Uncapitalize the name of the input type T.

```typescript
type MyType = Uncapitalize<'Abc'>; 
```

#### NoInfer\<T\>

NoInfer is a utility type designed to block the automatic inference of types within the scope of a generic function.

Example:

```typescript

function fn<T extends string>(x: T[], y: T) {
    return x.concat(y);
}
const r = fn(['a', 'b'], 'c'); 
```

With NoInfer:


```typescript

function fn2<T extends string>(x: T[], y: NoInfer<T>) {
    return x.concat(y);
}

const r2 = fn2(['a', 'b'], 'c'); 
```

