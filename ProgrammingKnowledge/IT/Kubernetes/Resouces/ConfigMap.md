
Ein Key-Value Store,der in einen Container gemappt werden kann.

Braucht man ein ganzes Config File kann man den Inhalt des File als `Value` verwenden und `Key` als Filename.

Einen ConfigMap mit einem Key `app.conf`, hier ist der Keyname gleich dem Filename:

``` shell

# Create a ConfigMap with a single key, "app.conf"

kubectl create configmap my-app-config --from=app.conf
```


Möchte man den Keyname selbst definieren:

``` shell
kubectl create configmap my-app-config --from=app.conf=app-prod.conf
```


Man kann auch ein ganzes Verzeichnis verwenden:


``` shell
kubectl create configmap my-app-config --from=config.d/
```

ConfigMap kann auch ganz normal als Key-Value Store verwendet werden:

```shell
kubeclt create cm my-app-config \
  --from-literal=foreground=red \
  --from-literal=background=blue
```


Man kann Key-Values auch aus einem `*.env`-File genieren:


```shell
kubeclt create cm my-app-config \
  --from-env_file=app.conf
```


#Kubernetes