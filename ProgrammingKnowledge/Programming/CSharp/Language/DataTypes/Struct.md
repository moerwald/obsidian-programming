# Struct

Eine [[Struct]] ist ein [[Value Type]]. Beispiel:

```CSharp

var p1 = new Point2D() {X = 1, Y = 1}

var p2 = p1;

p2.X = 6;

struct Point2D
{
	public int X { get; set; }
	public int Y { get; set; }

```

Der Wert von `p1.X` ist weiterhin `1`, da `p2` eine Kopie der `struct` erhält. Structs können nicht voneinander erben, was Sinn macht ein `int` erbt auch nicht von `byte`, sind halt getrennte Datentypen.

## Wan verwendet man Structs?

Mann verwendet [[Struct]]s wenn die Kopie teurer ist als die Referenz. Sprich eine Referenz ist grob nix anderes als ein 64-Bit Pointer auf eine Speicheradresse. Wenn jetzt die [[Struct]] viel mehr als die 64-Bit hat (z.B. 200 Byte), dann kostet das Erstellen der Kopie mehr Zeit/Performance als eine Referenz.

Siehe [MSDN](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/choosing-between-class-and-struct).



---
Tags:

[[CSharp]]

#CSharp 