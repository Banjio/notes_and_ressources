# Installation

https://www.typescriptlang.org/download

* Run `sudo npm install typescript -g` for a global installation or `npm install typescript --save-dev` for a project installation

# Ressources

* https://www.youtube.com/watch?v=BwuLxPH8IDs
* https://www.typescriptlang.org/docs/handbook/intro.html

# Typrescript.lang notes

## Ts for js Programmers

* TS knows the types of JS objects and often assigns the correct types (**Types by Inference**)
* Dynamic Programming construct in js makes type inference harder. For example:

```ts
const user = {
    name: "Harpun".
    id: 0
};
```
Better approach in Typescript would be to use `interface` declaration

```js
interface User {
    name: string;
    id: number;
}
// Now declare a user like this
const user: User = {
    name: "Hayes",
    id: 0,
};
```
Another approach would be to use the interface declaration with classejs classes
```ts
interface User {
    name: string;
    id: number;
}

class UserAcc {
    name: string;
    id: number;

    constructor(name: string, id: number) {
        this.name = name;
        this.id = id;
    }
}

const user: User = new UserAccount("Murphy", 1);
```

Or you can use interfaces to annotate functions and their return values

```ts
function getAdminsUser(): User{
    //...
}

function deleteUser(user: User){
//...
}
```


# Understanding Typescript 2022: Udemy Course

### List of Types in typescript

javascript "types"

* boolean, 
* bigint
* null
* number
* string
* symbol
* undefined

typescript extends this types

* any (allow all types)
* unknown (type must be declared by the one using it)
* never 
* void (Function that returns unkown or nothing)

## Ts type

Type is similiar to interface intended for building types (the later should be prefered in most cases). In typescript you can create new types by combining primitives

* Type can be used to create unions 

# Misc
# Resource: Typescript Course Begginers (YT)
## Implicit Typecasts

* `const input2 = document.getElementById("num2")! as HTMLInputElement;` &Rightarrow; "!" tells ts that this item will never be Nil and typecasts it to an HTMLInput ELement  (Implicit Typecasts)
* adding `+` in front of a parameter given to a function silences the linter warning (string not compatible with numeric)
## Ch1. Basics & Basic Types
### Core Types:
These are the types, js and ts have in common 

* Number: Ts (Js) makes no difference between float or integer
* String: Using Strings with backticks can be used for string interpolation in modern js
* boolean: Only supports true and false
* Objects: Are comparable to pythons dictionaries, i.e. they are key value pairs that can be nested infinitly 
* Arrays: Can store values of the same type or different types if you use `any[]` for initialization (However this has the downside of no type checking)

### Typescript specific types

* tuples: is a fixed size array
* enums: Is a custom type which assings labels to numbers and are great if you need humanly readable labels
* Any: Allows any type but is strongly discouraged because it takes away the advantages of typescript
* Union  types: we can give multiple types to one parameter in a function like `function  add(n1: number |string, n2: number | string)...` using the pipe operator `|` we can specify as many types as we need.
* Literal types: you can give them to a function parameter and these are the only types allowed as parameters, for example `function  add(n1: number |string, n2: number | string, resultConversion: 'as-number' | 'as-text')...`

### Type aliases

With type aliases you can create your own types using the `type` operator. Typically in conjunction with union types `type Combinable = number | string`

### Functions

* Functions can have return types. If you do not give a type it is inferred by ts. 
* Functions without a return statement have the return type `void`
* If you want to return a function use the type `Function`
* The arrow notation is used if you want too create a Function type with specific parameters and return types (So called **function types**), e.g. `let combineValues: (a: number, b: number) => number;`
* Typescript can also take functions as input parameter for a function, e.g. `function addAndHandle(n1: number, n2: number, cb: (num: number) => void){...}`

### Extra Types

* `Unknown`: Is used if we do not know what the user will enter. It is sligtly different to `any` because the following will **not** work with unkown only with any, because any is the **most flexible** type in ts which disables all type checking. `Unkown` is more restrictive, because we have to check the type if we assign it to another variable.
    ```ts
    let userInput: unknown;
    let userName: string;

    userInput = 5;
    userInput = 'Max'
    userName = userInput;
    ```
* Thus `unkown` is the better type over `any` if we do not know the type of a variable at compilation time (although union types are more preferable than `unknown`)
* `never`: Another type indicating functions do not return anything, consider the following code block:

    ```ts
    function generateError(message: string, code: number): never{
        throw {message: message, errorCode: code};
    }

    generateError('An error occured!', 500);
    ```

* This function never returns anything, because it cannot return anything because it will throw an error before ending the function and thus ending the script.

### Further Ressources

* https://www.typescriptlang.org/docs/handbook/2/everyday-types.html

## Ch2. Typescript Compiler and it's options

* **Watchmode**: Using the `-w` flag in the compiler will start in watchmode. Everytime the watched file changes it will recompile
* **Compiline multiple files**: We need to create a tsconfig.json file by running `tsc --init`. Then we cann run `tsc` without a specific file and all files will be compiled. Note that the tsconfig file offers a lot of other option which will be explained later on. 
* **Including/Exlcluding Files**: Add `exclude: []` as object to the json file outside `compilerOptions{...}`. Usually you want to always exclude "node_modules". However this is the default. `include: []` is the exact opposite to include. Only the files/folders listed here are then compiled. There is also a `file: []` option. However it has the functionality as `include` only that no folders are allowed (May only be feasible for small projects).
* **compilerOptions**: Setting the options for the compiler which also can be set by flags and are offered by `tsc --help`
  * **target**: Which javascript language specification should be used. Newer versions may be better performant but the compatibility with older browser may be not supported 
  * **lib**: Specify which libraries to use. If not set some defaults are assumed, e.g. all dom actions. 
  * **allowJs** and **checkJs**: Not usable in a pure ts project. But can be useful in pure js or mixed projects because it enables some ts checks for js
  * **sourceMap**: This will create `file.js.map` files while compiling. Ultimately this allows to debug also the ts files in the webdeveloper console in the debugger. 
  * **outDir** and **rootDir**: With **rootDir** We can specifcy folders where the source files are lying, e.g. `src/` and where the output (compilation results) are lying, e.g. `dist/`
  * **removeComments**: Will remove all comments in the output files. Useful if you want to make files smaller. 
  * **noEmit**: If this is true, no output files will be created
  * **downlevelIteration**: If this is true in some niche cases loops behave different between older and new es versions. If this is the case only then this option should be activated
  * **noEmitOnError**: Boolean. If set to true, if the compilation fails for any fail no overall output will be created.
  * **strict**: Activates all options below **strict** in the tsconfig file (All are booleans).  
    * **noImplicitAny**: Ensure that now implicit any type is used somewhere in the code, meaning if we forgot too give a type to a parameter in a function and the type cannot be infered we talk about an implicit any
    * **strictNullChecks**: Remember the button is null problem when using `document.querySelector(...)`. Strict null checks complains when we do not expliticy mark values that could be null on runtime. 
    * **strictFunctionTypes**: Niche parameter, catching some errors related to classes and inheritance
    * **strictBindCallApply**: If we use one of those add type checking to this functions
  * Everything under **Additional Checks** helps ensuring code quality, similiar to what a linter would do. For example if we define a variable which is nevers used.
    * **UnusedLocalVariables**: If inside a function a unused variable is created ts will complain.
    * **noImplicitReturns**: If a function does not return anything in all cases (e.g. returning from an if statement) the compiler will complain
* **Debugging with vscode**: Use the extension Debugger for Chrome/Firefox. Then you can set breakpoints inside ts files. Note that the sourceMap option in tsconfig should be enabled


## Common pitfalls

* If you use button and document.query you need to defer the script or otherwise the button will not be found (Will be null)