

## Einführung

In diesem Kurs auf Udemy lernen Sie, wie Sie mit Konfigurationsdaten in Kubernetes arbeiten. In der vorherigen Vorlesung haben wir gesehen, wie man Umgebungsvariablen in einer Pod-Definitionsdatei definiert. Wenn Sie jedoch viele Pod-Definitionsdateien haben, wird es schwierig, die in den Abfragedateien gespeicherten Umgebungsdaten zu verwalten. Wir können diese Informationen aus der Pod-Definitionsdatei herausnehmen und sie mithilfe von Config-Maps zentral verwalten.

## Was sind Config-Maps?

Config-Maps werden verwendet, um Konfigurationsdaten in Form von Schlüssel-Wert-Paaren in Kubernetes zu übergeben. Wenn ein Pod erstellt wird, injizieren Sie die Config-Map in den Pod, sodass die Schlüssel-Wert-Paare als Umgebungsvariablen für die Anwendung verfügbar sind, die innerhalb des Containers im Pod gehostet wird.

## Erstellen und Verwenden von Config-Maps

### Imperative Methode

Wie bei jedem anderen Kubernetes-Objekt gibt es zwei Möglichkeiten, eine Config-Map zu erstellen:

1. **Imperative Methode** ohne Verwendung einer Config-Map-Definitionsdatei.
2. **Deklarative Methode** mithilfe einer Config-Map-Definitionsdatei.

#### Erstellen einer Config-Map über die Befehlszeile

Wenn Sie keine Config-Map-Definitionsdatei erstellen möchten, können Sie einfach den Befehl `kubectl create configmap` verwenden und die erforderlichen Argumente angeben. Mit dieser Methode können Sie die Schlüssel-Werte-Paare direkt in der Befehlszeile angeben.

```bash
kubectl create configmap app-config --from-literal=app.color=blue
```


Wenn Sie weitere Schlüssel-Wert-Paare hinzufügen möchten, geben Sie einfach die Optionen `--from-literal` mehrfach an. Dies wird jedoch kompliziert, wenn Sie zu viele Konfigurationselemente haben. Eine andere Möglichkeit, Konfigurationsdaten einzugeben, ist die Eingabe über eine Datei.

bash

Code kopieren

`kubectl create configmap app-config --from-file=path/to/configfile`

### Deklarative Methode

Betrachten wir nun den deklarativen Ansatz. Dazu erstellen wir eine Definitionsdatei, ähnlich wie bei der Pod-Definition.

#### Beispiel einer Config-Map-Definitionsdatei



```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  app.color: blue
```
Um die Config-Map zu erstellen, führen Sie den Befehl `kubectl apply -f configmap.yaml` aus.

bash

Code kopieren

`kubectl apply -f configmap.yaml`

## Injektion von Config-Maps in Pods

Nachdem wir die Config-Map erstellt haben, können wir mit Schritt zwei fortfahren: der Injektion in einen Pod. Hier ist ein Beispiel einer einfachen Pod-Definitionsdatei, die eine Webanwendung ausführt.

### Beispiel einer Pod-Definitionsdatei mit einer Config-Map


```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webapp-pod
spec:
  containers:
    - name: webapp
      image: nginx
      envFrom:
        - configMapRef:
		  name: app-config
```

Beim Erstellen der Pod-Definitionsdatei wird nun eine Webanwendung mit blauem Hintergrund erstellt.

## Weitere Methoden zur Integration von Konfigurationsdaten

Neben der Verwendung von Config-Maps zur Injektion von Umgebungsvariablen gibt es noch andere Möglichkeiten, Konfigurationsdaten in Pods zu integrieren. Sie können sie als einzelne Umgebungsvariable oder die gesamten Daten als Dateien in einem Volume einspeisen. 


#Kubernetes