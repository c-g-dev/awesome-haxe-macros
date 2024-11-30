
# Expr Printer on TryHaxe

**[Goto](https://try.haxe.org/#F37F2F0d)**

## Source 

```haxe

class Test {
	static function main() {
		trace('Click "Compiler output" above.');
		Macro.print({

			//put your expr here

		});
	}
}

class Macro {
	public static macro function print(e:haxe.macro.Expr):haxe.macro.Expr {
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
