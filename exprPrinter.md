
# Expr Printer on TryHaxe

**[Goto](https://try.haxe.org/#E32415fE)**

## Source 

```haxe

class Test {
	static function main() {
		trace('Click "Compiler output" above.');
		Macro.printStr({
			var _STATE_CACHE:Map<String, Dynamic> = [];
			_STATE_CACHE["someKey"] = "someVal";
		});
	}
}

class Macro {
	public static macro function printStr(e:haxe.macro.Expr):haxe.macro.Expr {
		var printExpr:(haxe.macro.Expr, Int) -> Void = null;
		printExpr = (e, level) -> {
			var indent = "";
			for (i in 0...level)
				indent += "    ";

			trace(indent + Std.string(e.expr));
			haxe.macro.ExprTools.iter(e, (childE) -> printExpr(childE, level + 1));
		}

		printExpr(e, 0);

		return macro null;
	}
}



```
