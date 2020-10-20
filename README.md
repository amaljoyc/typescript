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
