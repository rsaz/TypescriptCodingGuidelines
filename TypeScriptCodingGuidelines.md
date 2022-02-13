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
- [CV: Conventions](#CV-conventions)
- [T: Types & SubTypes](#S-types)
- [TC: Type Casting](#TC-casting)
- [CF: Conditional Flow](#CF-flow)
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

```typescript
// Variable declaration
// Designator - variable name - assignment operator - optional value

let   name: string = "developer";
const name: string = "developer";

{Without optional value}

let   name: string;
const name: string;
```

```typescript
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

# <a name="S-types"></a>T: Types & Subtypes

- Primitive data types are:

  - **boolean:** true or false (it is not equivalent to 0 and 1). There is no data overlap between boolean and number.
  - **null:** null varies from language to language but in type script null represents the absence of value, nonexistent or invalid object or address.

  ```typescript
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

  ```typescript
  let x: number; // variable declared but not initialized
  console.log(x); // undefined

  function MyFunction(x: number) {
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
  - **void** is a special type that is used to represent the absence of a value. 
  - **unknown:** is a type that represents any value. It is the default type for any variable that is not explicitly typed. 

## Table of Types

| Type      | Use                                                                                         |
| --------- | ------------------------------------------------------------------------------------------- |
| boolean   | when we want to represent true or false                                                     |
| number    | when we want to represent an integer or a floating point                                    |
| bigint    | to represent a large integer number                                                         |
| string    | represent a sequence of characters                                                          |
| symbol    | to represent a unique symbol                                                                |
| array     | ordered list of values. Can be used combined with any other type                            |

## Table of Subtypes

| Type      | Use                                                                                         |
| --------- | ------------------------------------------------------------------------------------------- |
| null      | to represent absence of value, invalid object                                               |
| undefined | when a variable is declared but not initialized or when an argument is not formally passed. |
| object    | to represent a value with a set of properties. Ex. { id: 1, foo: 'foo' }                    |
| any       | to be used to avoid typechecking. Try to do not use this type much                          |
| void      | to represent the absence of a value                                                         |
| unknown   | to represent any value. Prefer to use unknown rather than any                               |

## Assignment of Subtypes

| Type      | any  | unknown | object | void | undefined | null | never |
| --------- | ---- | ------- | ------ | ---- | --------- | ---- | ----- |
| any       |      | OK      | OK     | OK   | OK        | OK   |       |
| unknown   | OK   |         |        |      |           |      |       |
| object    | OK   | OK      |        |      |           |      |       |
| void      | OK   | OK      |        |      |           |      |       |
| never     | OK   | OK      | OK     | OK   | OK        | OK   |       |
| null      | OK   | OK      | OK     | OK   | OK        |      |       |
| undefined | OK   | OK      | OK     | OK   |           | OK   |       |

# <a name="TC-casting"></a>TC: Type Casting

- Type casting is the capability to convert one type to another. In Typescript you can use `as` or `<>` to convert a value to a different type.
- When `any` or `unknown` is used, you can't use `as` or `<>` to convert a value to a specific type. **Always prefer to use unknown over any**. Unknown will force to explicitly specify the type. Unknown also prevents you to reasign a value to a variable without casting it.

```typescript
let varUnknown: unknown = 'foo';
let varAny: any = 'foo';

// Reassign of values
varUnknown = 1;
varAny = 1;

// Variable reassignment
let varStringAny: string = varAny; // (OK)
let varStringUnknown: string = varUnknown; // (NOK)

// Typecasting is necessary
let varStringUnknown1: string = <string>varUnknown; // (OK)
// Or
let varStringUnknown2: string = varUnknown as string; // (OK)
// Or
let varStringUnknown3: string = String(varUnknown); // (OK)
```  

## From any type to string, except object type

```typescript
let localNumber: number = 1;
// Recommended methods below : More readable
let localNumberToString1: string = localNumber.toString();
let localNumberToString2: string = String(localNumber);
let localNumberToString3: string = localNumber as unknown as string;

let localNumberToString4: string = <string>(localNumber as unknown);
let localNumberToString5: string = (<unknown>localNumber) as string;
```  

# <a name="CF-flow"></a>CF: Conditional Flow