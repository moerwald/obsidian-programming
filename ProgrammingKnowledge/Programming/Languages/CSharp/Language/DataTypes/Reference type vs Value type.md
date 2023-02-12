
# Reference Type vs Value Type

Ich hab am Anfang immer geglaubt Value Types werden am Stack gespeichert und Reference Types am Heap. **Das ist falsch**.  Ich muss das Ganze viel einfacher sehen. 

Wenn ich eine Variable eines *Value Types* anlege dann bekomme ich eine **Kopie** des Inhalts. 

```CSharp

int a = 8;

int b = a;

b = 9; // a ist weiterhin 8. 

```


Die Kopie kann am Stack oder am Heap gespeicher sein. 

Beispiel wo der Wert am Stack liegt:

```CSharp

void funtion Foo(int a)
{
	int b = a; // b hat eine Kopie des Wertes von a. b liegt am Stack
}

```


Beispiel wo der Wert am Heap liegt:

```CSharp


var lst = new List<int> { 1, // Die Werte 1-3 liegen am HEAP, genauso wie die lst
                          2,
                          3,}


```

Aufgrunddessen kann man bei einer [[Struct]] nicht einfach sagen, das diese am Stack allokiert ist. Eine [[Struct]] ist ebenso ein Value Type, es gelten dieselben Regeln.



---
Tags:

[[CSharp]]

#CSharp 