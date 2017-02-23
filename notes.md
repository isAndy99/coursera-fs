# Introduction to HTML5

## Lecture 5: HTML Content models

> **Block-Level elements:** (Roughly Flow Content)
> - render to begin on a new line
> - may contain inline or other block-level elements
> 
> **Inline elements:** (Roughly Phrase Content)
> - rendered on the same line (by default)
> - may only contain other inline elements

# Introduction to CSS3
## Lecture 14: Combining Selectors

Selector type | Syntax
---------|----------
 class selector | selector.class
 child (direct) selector | selector > selector
 descendent selector | selector selector
  | 
  adjacent selector | selector + selector
  general sibling selector | selector - selector

# Introduction to JavaScript

## Lecture 41, Part 1: Defining Variables, Function, and Scope
### Variables
- JS figures the type of the variable at runtime
- same variable cand hold different types during the life of the execution

### Functions

>```javascript
>function a () {...}
>```
>or
>```javascript
>var a = function () {...}
>```
> - no name defined
> - value of function assigned, **NOT the returned result**

### Scope
- Global
- Function (aka lexical)

### Scope chain
- Everything is executed in an *Execution Context*
- Function invocation creates a new *Execution Context*
- Each *Execution Context* has:
  * Its own *Variable Environment*
  * Special *'this'* object
  * Reference to its *Outer Environment*
- Global scope does not have an *Outer Environment* as it's the most outer there is

>Referenced (not defined) variable will be searched for in its current scope first. If not found, the *Outer Reference* will be searched. If not found, the *Outer Reference*'s *Outer Reference* will be searched, etc. This will keep going until the Global scope. If not found in Global scope, the variable is undefined.




# Other
> ### BrowserSync
> ``` browser-sync start --server --directory --files "**/*" ```