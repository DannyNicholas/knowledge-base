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
```

### Compile

Compile using:

```
tsc
```

Compiled `.js` will be created under `/dist` folder.

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

**Tuples**

For example, a user represented by id and name,
```
let user: [number, string] = [1, 'Mosh']
```

**Enums**

```
enum Size {
    Small, Medium, Large
}

let mySize: Size = Size.Large
```

xx