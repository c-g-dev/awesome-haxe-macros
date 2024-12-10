***tl;dr the first argument to a nonstatic macro method is its calling expression***

# Local Method Macros

TryHaxe example: [https://try.haxe.org/#3fCcce90](https://try.haxe.org/#3fCcce90)

Sometimes it is desirable to define a macro as a class method, so that it can be called on a specific object instance.

```haxe
class TextProcessor {
    public function new() {}
    
    public function process(text: String): TextProcessor {}
    public function publish(): Void {}
    
    // this could obviously be done better without macros, but for the sake of example...
    public macro function processFromURL(urlExpr: Expr): Expr {
        // convert to process(<text literal pulled from URL>);
    }
}

new TextProcessor().processFromURL("www.mystuff.com").publish();
// should query the mystuff page for text and macro-convert to:
new TextProcessor().process("my pulled text").publish();
```

If you try this approach, it won't work:

```haxe
public macro function processFromURL(urlExpr: Expr): Expr {
    var remoteString = httpCall(urlExpr);
    return macro process($v{remoteString});
}

// ...

new TextProcessor().processFromURL("www.mystuff.com").publish();
```

Which theoretically renders to:

```haxe
process("my pulled text").publish();
```

But this is not a valid expression, since `process` does not exist statically.

Local macro functions actually take their first parameter to be the calling expression. So the actual implementation will be like this:

```haxe
public macro function processFromURL(callingExpr: Expr, urlExpr: Expr): Expr {
    // in the above example, callingExpr = new TextProcessor()
    var remoteString = httpCall(urlExpr);
    return macro ${callingExpr}.process($v{remoteString});
}
```

This way you can have local methods be macro functions and use them for inline-transforming method calls.
