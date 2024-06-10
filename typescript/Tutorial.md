## TypeScript Tutorial

https://www.youtube.com/watch?v=d56mG7DezGs&t=478s

### Install typescript
```
$ npm i -g typescript
$ tsc -v
Version 5.4.5
```

### Set-up config

```
tsc --init
```

> This will create a new `tsconfig.js` file.

**Recommended changes:**

```
"target": "ES2016",
"module": "commonjs",
"rootDir": "./src",
"sourceMap": true,
"outDir": "./dist",
"removeComments": true,
"noEmitOnError": true,
"noImplicitAny": true,
"noUnusedLocals": true,
"noUnusedParameters": true,
"noImplicitReturns": true,
```

### Compile

Compile using:

```
tsc
```

Compiled `.js` will be created under `/dist` folder.

Run using:

```
node dist/<file>.js
```

### Debugging in VS Code

- Click "Run and Debug" (left panel).
- Choose "Create a launch.json file"
- Choose "node.js" from options list
- Edit created `launch.json` as required (see below)

`launch.json` file should look similar to this:

```
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "Launch Program",
            "skipFiles": [
                "<node_internals>/**"
            ],
            "program": "${workspaceFolder}\\src\\index.ts",
            "preLaunchTask": "tsc: build - tsconfig.json",
            "outFiles": [
                "${workspaceFolder}/**/*.js"
            ]
        }
    ]
}
```

**To debug:**
- Click "Run and Debug" (left panel).
- Choose "Launch Program"
- Click "Start Debugging (F5)"

## Built-in Types

![[built-in-types.png]]

### Tuples

For example, a user represented by id and name:

```
let user: [number, string] = [1, 'Mosh']
```

### Enums

Recommended to use `const` with enums for more optimised compiled code:

```
const enum Size {
    Small, Medium, Large
}

let mySize: Size = Size.Large
```

By default, enums get mapped to numbers. logging `mySize` would return `2`.

Can specify your own values:

```
const enum Size {
    Small = 's', Medium = 'm', Large = 'l'
}
```

### Functions

Declare your return types to avoid unexpected implicit return types:

```
function calculateTax(income: number): number {
    return income * 1.2
}
```

Compiler will error if incorrect number of parameters or parameters of incorrect type are supplied.

Default values:

```
function calculateTax(income: number = 100): number {
    return income * 1.2
}
```

> `income` will default to `100` if not supplied.

### Objects

Typescript compiler can infer the shape of your object:

![[object.png]]


Can declare types:

```
let employee: {
    readonly id: number,
    name: string,
    retire: (date:Date)
    fax?: string,
} = { id: 1, name: 'Dan'}
```

> `id` is `readonly` so can not be modified.

> Not everyone has a fax machine. `fax` is an optional property due to `?` at end.

Can also declare objects with functions:

```
let maths: {
    multiply: (value: number) => number
} = {
    multiply: (value: number) => value * 10
}

let result = maths.multiply(10)
```

### Type Alias

Types can:
- single place to define the shape of an object
- can be referenced wherever type is needed
- can keep code cleaner and follows DRY principals

```
type Employee = {
    readonly id: number,
    name: string
    retire: (date: Date) => void
}
```


```
let employeeDan: Employee = {
    id: 1,
    name: 'Dan',
    retire: (date: Date) => console.log(date)
}
```

### Union Types

Function written to convert kg to lbs - can take either a `number` or `string` so we use a union type.

```
function kgToLbs(weight: number | string): number {
    // narrowing
    if (typeof weight === 'number') {
        // compiler knows weight is now a number
        return weight * 2.2
    } else {
        // compiler knows weight is now a string
        return parseInt(weight) * 2.2
    }
}
```

Can be called using either:

```
let weight1 = kgToLbs(10)
let weight2 = kgToLbs('10kg')
```


### Intersection Types

Types that can be multiple types.

```
type Draggable = {
    drag: () => void
}

type Resizable = {
    resize: () => void
}

// UI widget is both draggable and re-sizeable
type UIWidget = Draggable & Resizable

// create a UI widget
let textBox: UIWidget = {
    drag: () => { console.log("drag") },
    resize: () => { console.log("resize") }
}
```

### Literal Types

Only allows specific (or exact) values to be set.

```
// quantity can only be 50 or 100
let quantity: 50 | 100 = 100
```

Alternatively:

```
type Quantity = 50 | 100
let quantity: Quantity = 100
```

### Nullable Types

Normally passing a `null` such as `greet(null)` would result in a compilation error.

We may want function to handle `null` values.

```
function greet(name: string | null) {
    if (name) {
        console.log(name.toUpperCase())
    } else {
        console.log("Hello stranger")
    }
}
```

We could also allow the function to handle `undefined` values by adding that type too.

### Optional Chaining

Can handle property chaining if value is `undefined` or `null`.

```
type Customer = {
    birthday: Date
}

function getCustomer(id: number): Customer | null | undefined {
    return id === 0 ? null : { birthday: new Date() }
}

// can be null
let customer = getCustomer(0)

// optional property access operator
// will return undefined if customer is null
let year = customer?.birthday?.getFullYear()
```

Handling a null array

```
let myNumbers: number[] | null = null

// will be undefined if array is null
let value: number | undefined = myNumbers?.[0]
```


Optional function calling

```
let log: any = <set to some function that could be null>

// will only execute log function if it references an actual function
log?.(100)
```