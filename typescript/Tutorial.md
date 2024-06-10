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

> This will create a new `tscongig.js` file.

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



