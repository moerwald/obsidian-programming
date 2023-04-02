Beschreibt den Overuse von primitiven Datentypen in APIs. In [[CSharp]] kann man das mit Hilfe von Records umgehen. Die Vorteile

- die API wird lesbarer -> vgl `Func<int, int, int>` vs `Func<CustomerId, OrderId, ProductId>`
- Man kann im Record den gewrappten Wert validieren. Zwei Möglichekeiten
	1. über CTOR der Exception wirft, oder
	2. über Factory-Method die ein `Either<Object, Error>` returnt.