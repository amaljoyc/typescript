# typescript

## Datatypes

- number `->` n: number
- string `->` s: string
- boolean `->` b: boolean
- object `->` o: {n: number; s: string}
- Array `->` a: string[]
- Tuple `->` t: [string, number]
- Enum `->` enum Role { CUSTOMER, ADMIN }
- any `->` x: any
- unknown `->` x: unknown (a type which is bit more stricter than any)
- union types `->` x: number | string
- literal types `->` s: 'hello' | 'hi'
- type aliases / custom types `->`

```
type MyType = string | number
type MyType = { name: string; age: number }
type MyFun = (a: number, b: number) => number
type MyFunc = () => number
```

### void return type

```
function hello(): void {
    console.log("hello")
}
```

Note: when this is transpiled to JS, the `void` is considered as `undefined`.

However, the `undefined` is not same as `void` in typescript. For returning undefined, the function would look like below,

```
function hello(): undefined {
    console.log("hello")
    return
}
```

### Function types

```
let myFun: Function
```

```
let myFun: () => void
```

```
let myFun: (n: number, s: string) => number
```

### never return type

useful for functions that never returns, eg, throws error instead of return, or a function that does an infinite loop.

```
function error(message: string, code: number): never {
    throw {message: message, number: number}
}
```

## Typescript Compiler

- to run all typescript files in watch mode, do

```
tsc -w
```

- to run a specific file in watch mode, do

```
tsc myfile.ts -w
```

- to init a typescript project, (will create the file tsconfig.json)
- this tsconfig file can be used to adjust the typescript compiler options

```
tsc --init
```

## Spread operator

can be used for arrays or objects

```
myNewArray = [ ...myarray ]
myNewObject = { ...myObject }
```

the three dot notation is also used for `rest params`, ie. you can pass in multiple function parameters, but they all will be then merged as an array, as shown in eg,

```
function add(...numbers: number[]) {

}

add(1, 2, 3, 4.5) // here these individual params are merged into a numbers array when calling the above function
```

## Destructuring

can be done for array as well as objects

```
const numbers = [1, 2]
const [n1, n2] = numbers // destructuring based on the array order
```

```
const person = {name: "Amal", age: 30}
const { name, age } = person // destructuring based on the key name (ie, name & age)
```

## Classes

```
class Person {
    name: string
    age: number

    constructor(name: string, age: number) {
        this.name = name
        this.age = age
    }
}

const person = new Person("Amal", 30)
```

### Shorthand initialization of class

The above class can be simplified even further as given below,

```
class Person {
    constructor(
        public name: string,
        public age: number
        ) {}
}

const person = new Person("Amal", 20)
```

when we do the shorthand initialization, we don't have to specify the fields separately and also inside the constructor. Although we have to explicitly specify the access modifier (private or public)

### access modifiers

- private -> only within the class
- public -> anywhere
- protected -> only within the classes and any of its child classes
- readonly -> on top of above modifiers, we can also mark a property as readonly if we don't want that property value to be changed or updated.

```
private readonly name
```

## Inheritence

```
class Amal extends Person {
    height: number

    constructor(age: number, height: number) {
        super("Amal", age)
        this.height = height
    }
}

const amal = new Amal(30, 100)
```

## Getter and Setter

```
class Person {
    private _name: string

    constructor(name: string) {
        this._name = name
    }

    get name() {
        return _name
    }

    set name(name: string) {
        this._name = name
    }
}

const p = new Person("Amal")
p.name = "Lama" // used as a property, not as a method
console.log(p.name) // used as a property, not as a method
```

## Static methods and properties

```
class Person {
    static HELLO = "Hello"
    static greeting() {
        return "Hi"
    }
}

const hi = Person.greeting()
const hello = Person.HELLO
```

Note: static fields cannot be accessed from non-static methods inside the class using `this`. Instead it can only be accessed using the "ClassName." notation

## Interfaces

```
interface Person {
    name: string
    age: number
    greet(): void
}

let person: Person;
person = {
    name: "Amal",
    age: 20,
    greet() {
        console.log("Hello " + this.name)
    }
}

person.greet()
```

Notes:

- you an inherit only form one class, but can implement multiple interfaces.
- also you could extend/inherit an interface from multiple interfaces.
- you can only use `readonly` modifier inside an interface. Cannot use private, public, or protected.
- you use an interface if you wanna work with objects. If you rather just need a complex type creation, you could use `type` instead - although the `interface` and `type` can be used interchangably when needed.

### Interface as Function types

```
interface MyFun {
    (a: number, b: number): number
}

let add: MyFun
add = (a: number, b: number) => a + b
```

Notes:

- you don't specify the function name when you define an interface for a function type (but you do it when you define and interface for an object type)
- also it is better to use `type` rather for defining function types.

### Optional properties and method in interface

```
interface Person {
    name: string,
    age?: number, // age is optional
    greet?(): void // greet is optional
}
```

Note: similar to interfaces, you could also have optional properties in classes as well by using the `?:` notation

## Intersection Types

```
type MyType3 = MyType1 & MyType2
```

## Type Casting

```
// syntax 1
const c = <Person>person
// syntax 2
const c = person as Person
```

## Index Properties

```
interface Person {
    [prop: string]: string
}
```

## Optional Chaining

```
const c = obj?.data?.id
```

## Nullish Coalescing

```
const s = data ?? "fallback-value"
```

Note: here if the value of `data` is null or undefined, then the fallback value will be assigned to s
