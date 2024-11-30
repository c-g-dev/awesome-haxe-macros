# awesome-haxe-macros

A curated list of articles, examples, and other resources for the Haxe macro system.

## What are macros in Haxe?

In Haxe, macros are preprocessor functions included in source code which transform and generate syntax during compilation. They do not preprocess the raw text of the source code, but rather directly edit the internal abstract syntax tree (AST) of the compiler. As the [manual] (https://haxe.org/manual/macro.html) describes them:

> A basic macro is a syntax-transformation. It receives zero or more expressions and also returns an expression. If a macro is called, it effectively inserts code at the place it was called from. In that respect, it could be compared to a preprocessor like `#define` in C++, but a Haxe macro is not a textual replacement tool.

<br/>

## Basic official references

- The Haxe macro [manual](https://haxe.org/manual/macro.html)
- Macro examples in the [Code Cookbook](https://code.haxe.org/category/macros/)
- [Expr API](https://api.haxe.org/haxe/macro/ExprDef.html) - `Expr` is the fundamental building block of all Haxe code. Any Haxe source code can, and is, represented by an instance of the `Expr` object. Macros take in `Expr` objects and output `Expr` objects. Understanding the structure of an `Expr` instance, how to parse them and pattern match them, and how to construct them, is 90% of macro development.
- [Context API](https://api.haxe.org/haxe/macro/Context.html) - Critical class providing contextual information about the current state of the AST, exposes callback hooks for the compiler, defines new types, and other utility functions. Look over it to get a good scope of what is possible.
- [Compiler API](https://api.haxe.org/haxe/macro/Compiler.html) - Another static utility class with more emphasis on changing compiler functions rather than editing the AST. Has some of the most powerful, most esoteric functions.
- Various standard macro tools:
  - [MacroStringTools](https://api.haxe.org/haxe/macro/MacroStringTools.html)
  - [PositionTools](https://api.haxe.org/haxe/macro/PositionTools.html)
  - [TypedExprTools](https://api.haxe.org/haxe/macro/TypedExprTools.html)
  - [ExprTools](https://api.haxe.org/haxe/macro/ExprTools.html)
  - [ComplexTypeTools](https://api.haxe.org/haxe/macro/ComplexTypeTools.html)
  - [ExprArrayTools](https://api.haxe.org/haxe/macro/ExprArrayTools.html)
  - [TypeTools](https://api.haxe.org/haxe/macro/TypeTools.html)
 
<br/>

## Guides
- **[Marc Weber Macro Reification Examples](https://github.com/MarcWeber/haxe-macro-examples/blob/master/Macro.hx)**

<br/>

## Tools
- **[Easy Online Expr Printer](exprPrinter.md)**

<br/>

## Library Examples

- **[deepnightLibs Cinematic.hx](https://github.com/deepnight/deepnightLibs/blob/master/src/dn/Cinematic.hx)** - Builds an elegant orchestrator/coroutine system, effectively extends the language by parsing expressions in a bespoke form like `{doStuff() > wait(500)}`. Showcases how operators like `>` can be co-opted for creative uses.

- **[compiletime](https://github.com/jasononeil/compiletime)** - Access compile-time information not normally available during runtime, such as lists of all defined types, all types implementing a certain interface, etc.

<br/>


## Full Project Examples

- **[heaps Res.hx system](https://github.com/HeapsIO/heaps/blob/master/hxd/Res.hx)** - In the `./res/` folder of your source code, provides a static class which reads the folder and adds typed fields for each with full IDE completion. Effectively statically types resource files and gives them IntelliSense.

- **[haxeui](https://github.com/haxeui/haxeui-core)** - An incredibly impressive system in many ways, the consummate showcase of all Haxe's unique functions. Exposes build macros to load XML markup files into classes, effectively implementing a sort of pseudo-MVVM system. Not even mentioning all the internal uses of macros which are used to make behaviors composite.


<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

Definitely a lot still missing, I am just updating this as I remember or encounter different things. If you want to add to this list, raise a PR or contact me directly. Especially looking for how-to guides, gists, concise examples or unique, creative examples.
