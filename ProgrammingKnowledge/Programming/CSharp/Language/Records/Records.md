
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
	
	var x = p1 == p2; // returns true
	
	```
	
	Wären `p1` und `p2` Referenzen auf Klassen wäre der Vergleich `false`, da der Defaultvergleich auf die Referenzen nicht auf deren Inhalt geht!
	
- Records implementieren die `Deconstruct`-Method, somit funktioniert folgendes:

	```CSharp
	var (f,s) = p1;
	```


## Wann verwende ich Records?

To be defined


## Wie wurde dieses Feature eingebaut.

Für Records musste die CLR NICHT angepasst werden. Mithilfe von [Compiler Lowering](https://mattwarren.org/2017/05/25/Lowering-in-the-C-Compiler/), im Endeffekt generiert der Compiler C# Code, **bevor** dieser in IL-Code übersetzt wird. Um sich das Ganze anzusehen kann man obigen Code in [sharplab.io](https://sharplab.io/) verwenden und sich das Outcome ansehen.


## Was passiert beim Vergleich wenn ein Record Referenztypen als Properties hat?

```CSharp
var strings = new List<string> { "Hello", "World" };

var r1 = new MyRecord(strings);
var r2 = new MyRecord(strings);

(r1 == r2).Dump();

```

Der Vergleich verhält sich gleich wie wenn die Property ein Werttyp ist.


## Was passiert wenn ich Records unterschiedlicher Vererbungshirarchien vergleiche?

```CSharp

var strings = new List<string> { "Hello", "World" };

var r1 = new MyRecord(strings);


var r3 = new MyDerivedRecord(strings);
(r1 == r3).Dump();

public record class MyRecord(List<string> MyStrings);

public record class MyDerivedRecord(List<string> MyStrings) : MyRecord(MyStrings);



```

Der Vergleich liefert `false`. Das macht auch Sinn. Allerdings warum ist so? Sehen wir uns den decompiled Code ([[LinqPad]]) mal an:

```CSharp

public class MyDerivedRecord : MyRecord, IEquatable<MyDerivedRecord>  
{
	protected override Type EqualityContract  
    {  
        [CompilerGenerated]  
        get  
        {  
            return typeof(MyDerivedRecord);  
        }  
    }

    ...

    [System.Runtime.CompilerServices.NullableContext(2)]  
    public virtual bool Equals(MyDerivedRecord other)  
    {  
        return (object)this == other || base.Equals(other);  
    }
}

public class MyRecord : IEquatable<MyRecord>
{
    ...
    
	public virtual bool Equals(MyRecord other)  
    {  
        return (object)this == other || ((object)other != null && EqualityContract == other.EqualityContract && EqualityComparer<List<string>>.Default.Equals(<MyStrings>k__BackingField, other.<MyStrings>k__BackingField));  
    }

}
```

Wie man sieht enthält `Equals` einen Typvergleich `EqualityContract == other.EqualityContract`. Nachdem der Base-Type und Derrived-Type unterschiedlich sind können die beiden Records nicht gleich sein.

---
Tags:

[[CSharp]]

#CSharp
#Charp9
#Charp10