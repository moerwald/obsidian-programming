Ermöglicht das Testen von Verhalten von Funktionen. Input-Parameter werden hierzu Random generiert. Im Unit Test beschreibt man nur das Verhalten einer Funktion und verzichtet auf die Definition der Funktionsparameter.

Beispiel:

``` CSharp

[Fact]
public void AdditionIsCommutative (int a, int b)
{
	var r1 = Add(a, b);
	var r2 = Add(b,a);

	Assert.IsTrue(r1 == r2);
}

```

Obiges Beispiel zeigt das kommulative Verhalten einer Addition. Die Werte der Summanden hier ist egal. Es geht einzig aufzuzeigen, dass die Reihenfolge der **Summanden egal ist**.

In [[CSharp]] kann man [[FSCheck]] für [[Property Based Testing]] verwenden.