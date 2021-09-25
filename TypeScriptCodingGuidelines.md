# <a name="main"></a> TypeScript Coding Guidelines

September 11, 2021

Editors:

- [Richard Zampieri](http)
- [Maybe you can help?]()

# <a name="S-why"></a>Why do we need coding guidelines?

Is a general rule of software development to craft applications that are readable, maintainable and scalable. This is not always the truth but we aim for this goal.

Code standards are tools that helps to achieve building applications with the triad principles mentioned above. Here are some of the benefits that are provided by establishing a consistent development guideline:

- Reduction of security risks
- Increase of software performance
- Reduce the system complexity
- Cost-efficient.

# <a name="S-doc"></a>This Document

This is a living document under continuous improvement.
Copying, use, modification, and creation of derivative works from this project is licensed under an MIT-style license.
Contributing to this project requires agreeing to a Contributor License. See the accompanying [LICENSE](LICENSE) file for details.
We make this project available to "friendly users" to use, copy, modify, and derive from, hoping for constructive input.

Comments and suggestions for improvements are most welcome.
We plan to modify and extend this document as our understanding improves and the language and the set of available libraries improve.

# <a name="S-summary"></a>Summary

- [V: Variable Declaration](#S-variables)
- [T: Types](#S-types)
- [L: Language Features](#S-language-features)

# <a name="S-variables"></a>V: Variable Declaration

- To declare a variable you can use the keywords `var`, `let` or `const`.
  - **const:** increase the predictability of your code, that intrinsically improve performance.
  - **var:** is globally scoped, doesn't respect code blocks, this may sometimes generate confusion. **Avoid var when you can**.
  - **let:** is scoped constrained. If you declare a variable inside of a scope that variable will exist only inside of the scope
    where it was created. You can't access the variable externally. This is usually the strategy used in most of the strongly typed languages.
- Prefer `const` over `let` when possible, and **avoid using var**.
- Always initialize variables to avoid undefined behavior
- Always define the type for your variable.
- Declaration patterns: designator statement, variable name, type, and optional assignment operator + value.

> <> _Don’t ever use the types Number, String, Boolean, Symbol, or Object These types refer to non-primitive boxed objects that are
> almost never used appropriately in JavaScript code_.

```
// Variable declaration
// Designator - variable name - assignment operator - optional value

let   name: string = "developer";
const name: string = "developer";

{Without optional value}

let   name: string;
const name: string;
```

```
// Use of let
let y: number = 100;
 {
 let x: number = 10;
 y = 101; {OK}
 }

 x = 11; {You can't assign value to the variable x because the variable was created in a blocked scope}
```

## Proposed practice for Variable Declaration

- Variable names needs to be expressive.
- Adopt camel-case naming convention for variable declaration.
  - Good variable names: `age, addressDetails, etc.`
  - Good constant names: `MAX_AGE, BUFFER_SIZE, etc.`

# <a name="S-types"></a>T: Types

- Primitive data types are:

  - **boolean:** true or false (it is not equivalent to 0 and 1). There is no data overlap between boolean and number.
  - **null:** null varies from language to language but in type script null represents the absence of value, nonexistent or invalid object or address.

  ```
  class MyType {
    public typeInfo: string = "MyType";
  }

  let myType: MyType = new MyType();
  console.log(myType.typeInfo); // MyType {OK}

  myType = null; // Setting object to point to null
  console.log(myType); // null {OK}
  console.log(myType.typeInfo); // cannot read property 'typeInfo' of null {NOK}
  ```

  - **undefined:** when a variable is declared but not initialized or when an argument is not formally passed.

  ```
  let x: number; // variable declared but not initialized
  console.log(x) // undefined

  function MyFunction(x: number)
  {
    console.log(x);
  }

  MyFunction(); // undefined
  ```

  - **number:** represents an integer or floating point number. Ex. 56 or 76.987. The size of a number is a double-precision 64-bit binary [format IEEE 754](https://en.wikipedia.org/wiki/Double-precision_floating-point_format).
  - **bigint:** can represent integers of arbitrary size, larger than whole numbers 2^53 - 1. `Number.MAX_SAFE_INTEGER` is the largest number JavaScript can represent with a number primitive (or Number value).
  - **string:** sequence of characters used to represent text. Ex. "Hello World".
  - **symbol:** a unique and immutable symbol. Used to represent a property key, and used to avoid conflicts with other symbols.
  - **object:** any javascript value with a set of properties.
  - **any:** is a special type that you can use whenever you don't want to specify a type, or you don't want a particular value to cause a typechecking error. If you don't specify a type, or Typescript can't infer the type from it context,the compiler will default to any. You don't usually want to use any because defeats the purpose of typechecking.
  - **Array:** is an ordered list of values. In Typescript you can use array type to specify a list of values.
    Arrays can be declared using the generics template `let myArray: Array<number>` or the type annotation `let myArray: number[]`.

## Table of Types

| Type      | Use                                                                                         |
| --------- | ------------------------------------------------------------------------------------------- |
| boolean   | when we want to represent true or false                                                     |
| null      | to represent absence of value, invalid object                                               |
| undefined | when a variable is declared but not initialized or when an argument is not formally passed. |
| number    | when we want to represent an integer or a floating point                                    |
| bigint    | to represent a large integer number                                                         |
| string    | represent a sequence of characters                                                          |
| symbol    | to represent a unique symbol                                                                |
| object    | to represent a value with a set of properties. Ex. { id: 1, foo: 'foo' }                    |
| any       | to be used to avoid typechecking. Try to do not use this type much                          |
| array     | ordered list of values. Can be used combined with any other type                            |
