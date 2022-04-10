# Azure AI Services

[Referenz](https://docs.microsoft.com/en-us/learn/modules/ai-machine-learning-fundamentals/2-identify-product-options)

AI ist Software die sich an neue äußere Gegenbenheiten adaptieren kann, ohne das hierfür zusätzlich Programmierung notwendig ist.

Es gibt zwei Ansätze:

- **Deep learning**: Hier basiert die SW auf einem neuronalen Netz, dass in der Lage ist zu lernen.
- **Machine learning**: Hier wird ein Algorithmus mit "Tonnen" von Daten traininiert, um später enstprechende Aussagen über neue Daten zu treffen.

## Einsatzgebiete
- Shopping: KI erstellt Vorschläge was man noch zusätzlich zum gekauften Item brauchen könnte.
- Schutz: Die KI zum Beispiel Kreditkartentransaktionen analysieren. Treten hier Auffälligkeiten auf kann der Besitzer gewarnt werden.

## Azure Services

- [[Azure Machine Learning]]
- [[Azure Cognitive Services]]
- [[Azure Bot Services]]


## Wann welches Service nutzen?

### Benötigt man Userinteraktion ?

Falls ja, [[Azure Bot Services]]. Es gibt bereits Templates für vorgefertigte Bots.

### Benötigt man kognitive Erkennung?

Falls ja, [[Azure Cognitive Serivces]].

### Userverhalten vorhersagen?

[[Azure Cognitive Serivces]] -> [[Azure Cognitive Service Personalizer]] überwacht Userverhalten und kann in Kombination mit einem eigenes antrainiert Modell ([[Azure Machine Learning]]) dem User Vorschläge vorgeben.

### Vorhersagen basierend auf private Daten notwendig?

Falls ja, [[Azure Machine Learning]].


