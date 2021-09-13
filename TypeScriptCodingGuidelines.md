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
- [C: Configuration](#S-configuration)
- [L: Language Features](#S-language-features)

# <a name="S-variables"></a>V: Variable Declaration

- To declare a variable you can use the keywords `var`, `let` or `const`.
  - **const:** increase the predictability of your code, that intrinsically improve performance.
  - **var:** is globally scoped, doesn't respect code blocks, this may sometimes generate confusion. **Avoid var when you can**.
  - **let:** is scoped constrained. If you declare a variable inside of a scope that variable will exist only inside of the scope
    where it was created. You can't access the variable externally. This is usually the strategy used in most of the strongly typed languages.
- Prefer `const` over `let` when possible, and **avoid using var**.
- Always initialize variables to avoid undefined behavior
- Variables needs to be expressive.
- Always define the type for your variable.
- Adopt camel-case naming convention for variable declaration.
  - Good variable names: `age, addressDetails, etc.`
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

- Variable names needs to
