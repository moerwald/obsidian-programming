# Functions

Via `return` kann man aus einer `function` einen Wert returnen.

```javascript
function f1(num){
	return num - 7;
}

console.log (f1(10)); // prints 3
```


## Function statement vs function expression

Wenn das `function` keyword das erste Keyword im Statement ist, dann ist es ein Function Statement. Ansonsten ist es eine Function Expression.

```
// Statement
function foo(){
	console.log("foo");
}

// Expression

var bar = function foo() {
	console.log("foo");
}
```

Generell sind Function Expressions zu bevorzugen. **Wichtig**: Function Expressions sollten immer einen Namen haben, hilft beim Debuggen. Wenn man nur anonyme Function Expressions verwendet sieht man im Debugger den Function Name nicht.

Kurzum:

```
var bar = function(){
  ....
}
```

Sollte NICHT verwendet werden.