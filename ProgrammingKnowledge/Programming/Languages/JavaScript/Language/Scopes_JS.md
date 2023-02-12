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


## Scope Auflösung

**Annahme:** Die Ausführung von JS Code läuft zweistufig, ähnlich wie beim Kompilieren. In der ersten Stufe `scant` die JS-Engine den Code und Variablendeklarationen pro Scope vorzunehmen. In der zweiten Stufe werden die Scopes abgefragt, ob es eine Variable mit Namen xyz im aktuellen Scope gibt. Falls nicht, gibt man in den Parent-Scope und wiederholt das Spielchen. Wenn der aktuelle Scope der global Scope ist, kommt es drauf an, ob das Script im Strict-Mode läuft oder nicht. Im Strict Mode wird ein ReferenceError geworfen falls eine Variable nicht existiert. Im NON-Strict Mode wird die Variable einfach definiert 😂.
Weiters gehen wird von LHS und RHS Values aus. Beide tauchen bei Assignments auf -> `LHS = RHS`. Wenn es sich um kein Assignment handelt, z.B. Function Invocation das ist der Value ein RHS Value.

**Scan**: Der Scan ist immer von oben nach unten. Es geht immer nach folgenden Rezept.

1. Hey global scope I've a variable declaration for a variable named `foo`. Global scope adds this declaration.
2. Hey global scope I've a function declaration for a function named `bar`. Global scope adds this declaration.
3. Since it's a function we recursevly move on inside the function. From now on we're in the functions (`bar`) local scope. 
4. Hey local scope of bar I've a variable declaration for a variable named `foo`. Local scope will add it.
5. We recursivly create a new scope for function `baz`. Here we're an implicit variable declaration for parameter `foo`.

At the end we've a scope table, which includes child scopes and variable declarations. Functions are also stored as variable declarations.

**Execution**:

Here the `LHS` and `RHS` values come into the game. 

1. Hey global scope I've an `LHS` called `foo`, do you know it? -> Yes. Ok, please assign value `"foo"` to it.
2. Hey global scope I've an `RHS` value named `bar`, do you know it? -> Yes, invoke it.
3.  ....

```
var foo = "foo";

function bar() {
    var foo = "baz";

    function baz(foo) {
        foo = "zab";
        bam = "yay";
    }

    console.log(foo);

    baz();

    console.log(foo);
}

bar();
console.log(foo);
console.log(bam);

baz();
```

**Wichtig**: Funktionen werden als Variablen gespeichert. Heißt im z.B. global Scope gibt es eine Variable `bar`, dessen Wert ein Function-Object ohne Parameter ist.