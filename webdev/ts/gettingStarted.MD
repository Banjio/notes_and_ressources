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
// Now declause a user like this
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