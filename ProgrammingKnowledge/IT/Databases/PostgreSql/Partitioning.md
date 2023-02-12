
[Referenz](https://www.postgresql.org/docs/current/ddl-partitioning.html)

Hilft einen **großen** logischen Table in mehrere kleine Tables (physisch auf der Disk) zu zerlegen.

Vorteile:

- Query Performance wird besser
- Bulk Loads und Buls Deletes werden leicht möglich.
- Daten die seltener benötigt werden können auf billigeren/langsameren Speicher laufen.

*Goldene Regel:* Wenn die Table Size größer der RAM Size ist, dann nimm Partitioning.

## Arten wie Partition erstellt werden kann

- *Range Partition*: Man erzeut die Partion basierend auf Ranges von einer oder mehreren Spalten. Beispiel: Es gibt eine Datumspalte, dann kann man sagen, man erzeugt eine Partition, die alle Einträge für einen Tag enthält.
- *List Partition*: Man gibt **explizit** an welche Keys in welcher Partition liegen sollen.
- *Hash Partition*: Man verwendet auf eine Spalte eine Modulu-Opertion, basierend auf den Rest landet die Zeile in einer enstsprechenden Partition.

## Deklaratives Partitionieren
Ganz einfach: Man deklariert, dass ein Table, basierend auf einer/mehrerer Spalte(n), mit **einer** der obigen Partittionarten aufgeteilt wird. Der ursprüngliche Table ist dann nur mehr einer `virtueller` Table der auf die einzelnen Partitionen zeigt. 

Ändert man in einer Row den Partition-Key moved die DB die Row in eine andere Partition. Auf Partition-Tables könnte man nochmals partitionieren, dass wäre dann ein `Sub-Partitioning`. 

Partition-Tables können eigene `Indexe` haben.

#SQL
#Database
