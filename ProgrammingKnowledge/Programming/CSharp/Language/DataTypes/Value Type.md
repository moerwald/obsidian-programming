# Value Type

Variablen eines [[Value Type]] speichern immer einen Wert (**keine** Referenz). Somit ändert eine Variable immer eine dezidierten Wert.

Beispiel:

```CSharp

int a = 9;

int b = a; // b bekommt eine Kopie des Wertes von a

b = 6; // a hat weiterhin den Wert 9

```

Einfache Datentypen wie `int`, `bool`, `char`, `byte`, `long`, `double`, sind [[Value Type]]s.



---
Tags:

[[CSharp]]

#CSharp 