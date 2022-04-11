
# Records

Ein `record` ist nichts anderes als eine Klasse, bei der die Properties `init`-only sind. Somit ist:

```csharp
public record Person(string FirstName, string SurName)
```

Das gleiche wie:

```csharp
public record Person
{
	public string FirstName {get; init;} = default!
	public string SurName {get; init;} = default!
}
```

Records sollte als Dataobjects verwendet werden. Records haben gegenüber Klassen folgende Vorteile:

- `ToString` "printed" die Werte der Properties. Das Verhalten kann mit `override PrintMembers` angepasst werden.

	```csharp
	public record Person
	{
		public string FirstName {get; init;} = default!
		public string SurName {get; init;} = default!

        protected override bool PrintMembers(StringBuilder builder)
		{
			// builder.Append ...
			return true;
		}

	}
	```
- Records implementieren `IEquatable` per Default.  Somit ist folgendes true: 
	
	```CSharp
	
	var p1 = new Person("John", "Doe");
	var p2 = new Person("John", "Doe");
	
	var x = p1 == p2; // return true
	
	```
	
	Wären `p1` und `p2` Referenzen auf Klassen wäre der Vergleich `false`, da der Defaultvergleich auf die Referenzen nicht auf deren Inhalt geht!
- Records implementieren die `Deconstruct`-Method, somit funktioniert folgendes:
	```CSharp
	var (f,s) = p1;
	```


# Wie wurde dieses Feature eingebaut.

Für Records musste die CLR NICHT angepasst werden. Mithilfe von [Compiler Lowering](https://mattwarren.org/2017/05/25/Lowering-in-the-C-Compiler/), im Endeffekt generiert der Compiler C# Code, **bevor** dieser in IL-Code übersetzt wird. Um sich das Ganze anzusehen kann man obigen Code in [sharplab.io](https://sharplab.io/) verwenden und sich das Outcome ansehen.




---
Tags:

[[CSharp]]

#CSharp
#Charp9
#Charp10