# Scopes 

Variablen die ohne `var` definiert werden sind im `Global` Scope.

```javascript

function func1(){
	someVariable = 5;
}

func1();
console.log(someVariable); // Will print 5

```

Variablen die außerhalb einer Function definiert sind können INNERHALB der Function referenziert werden.

```javascript
var outerVar = "Hello";

function func1(){
	console.log(outVar);
}

func1();
```

Würde im obigen Beispiel in der `function` ebenfalls `outVar` definiert werden, würde die lokal Variable die globale Variable ersetzen.