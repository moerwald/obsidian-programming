
Docker Container können via

```
docker container run
```

gestartet werden. Folgende Parameter sind interessant:

- `-p` Port Mapping `LocalPort:DockerContainerPort`
- `--name` vergibt einen Namen, der Container ist dann einfacher referenzierbar
- `--net-alias` ermöglicht verschieden Container Instanzen hinter einem DNS Namen zu verstecken. Ermöglicht DNS Roundrobin
- `-network` added Container zu bestehenden Network.

#Docker 