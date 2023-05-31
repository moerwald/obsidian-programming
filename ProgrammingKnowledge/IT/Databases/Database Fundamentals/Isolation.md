

## Read phenomena

#### Dirty read

Eine Transaktion hat was gelesen, was eine andere Transkation geschrieben, **ABER** nocht nicht committed hat!!


#### Non-repeatabl reads

Man ließt zweimal den gleichen Wert über den gleichen SQL Query (innerhalb einer Transaktion) bekommt aber versch. Ergebnisse. Weil in der Zwischenzeit eine Write-Operation committed wurde.

#### Phantom read

Eine Transkation ließt Werte über einen Query. Eine andere Transkation **added** eine neue Row und committed diese. Die erste Transkaiton ließt wieder die Werte über einen Query und hat eine **zusätzliche** Row im Result-Set

#### Lost Updates

Zwei Transkationen machen ein gleichzeitiges Update ein Row. TR1 macht einen `UPDATE`-Query hat aber nocht nicht committed. TR2 macht ebenfalls einen `Udpate`-Query, basierend auf dem alten Row-Wert (da TR1 und TR2 gleichzeitig gestartet sind). TR2 comitted den Change, danach Comitted TR1. Die Änderung von TR1 ist inkorrekt.



## Isolstaion Levels

Sind gedacht um Read Phenomenas zu fixen.

#### Read uncommitted

Jeder Query in einer Transaktion sieht alle Changes von anderen Transaktionen. Egal, ob committed oder nicht.

#### Read committed

Jeder Query in einer Transaktion sieht nur committed changes von anderen Transaktionen.

#### Repeatable Read

Transaktion bekommt immer den gleichen Wert einer Row. Egal, ob andere Transkationen Changes geschrieben haben.

#### Snapshot

Wie ein Snapshot der ganzen DB. Eleminiert Read Phenomenas. Ist allerdings sehr **teuer**.

#### Serializable

Transkationen werden der Reihe nach abgearbeitet.


Von [Wikipedia](https://en.wikipedia.org/wiki/Isolation_(database_systems))

![[Pasted image 20230514093639.png]]






#Database 