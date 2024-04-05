
Siehe auch [Docker Virtual Networks](https://docs.docker.com/network/).

Wenn Docker einen Container startet, wird dieser Container in ein Default Network names `bridge` geadded. Das `bridge` Network verwendet verwendet den [bridge network driver](https://docs.docker.com/network/drivers/bridge/), der es mehreren Containern innerhalb eines `bridge` Networks ermöglich untereinander zu kommunizieren.
Jedes Docker Netzwerk routet den Traffic durch eine NAT Firewall. Um Traffic in das Docker Network zu routen wird ein Port Forwarding verwendet (`-p` Parameter bei `docker container run` setzt das Port Forwarding auf).

Starten von Nginx:

```
docker container run -p 8080:80 --name webhost -d nginx
```

Mit der `port` Option kann das Mapping eines Containers angezeigt werden:

```
moerwald@T16-AMewald:~$ docker container port webhost
80/tcp -> 0.0.0.0:8080
```

Die IP-Adresse eines Containers kann man sich mit folgenden Befehl anzeigen:

```
moerwald@T16-AMewald:~$ docker container inspect webhost --format "{{.NetworkSettings.IPAddress}}"
172.17.0.2
```

Mit dem [`format`](https://docs.docker.com/reference/cli/docker/inspect/#get-an-instances-ip-address) Parameter kann man den Output von `inspect` filtern,


## Network commands

`docker network ls` -> zeigt Docker Networks an
`docker network inspect` -> gibt Infos über das Network aus
`docker network connect` -> verbindet einen Container in ein **bestehendes** Netzwork bzw fügt eine NIC im Container hinzu
`docker network disconnect` -> entfernt einen Container aus einem Netzwerk


### LS

```
moerwald@T16-AMewald:~$ docker network ls
NETWORK ID     NAME         DRIVER    SCOPE
e43aee6f0294   bridge       bridge    local
ffc05de7a3ad   host         host      local
737a17872ba5   my-net       bridge    local
43be86d56c7b   my_app_net   bridge    local
d6ac13df89fb   none         null      local
```

### Inspect

Inspect zeigt Details für das Network an. Z.B:
- IP-Adress Subnet + Gateway
- Container welche diesen Network zugeordnet sind.
- Driver type

```
moerwald@T16-AMewald:~$ docker network inspect bridge
[
    {
        "Name": "bridge",
        "Id": "e43aee6f0294c6242470016bbad438ae0f3f58f8daaf7e611c1f3987d74c6419",
        "Created": "2024-03-24T19:31:25.862900204Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "172.17.0.0/16",
                    "Gateway": "172.17.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "37f24d4529da6c49183cf008c8a94a9d035110a071fd0b4bac6b468d8b75b6ad": {
                "Name": "webhost",
                "EndpointID": "15fff3fc7d8b59f5900912f4ef27db55dcb1fa1409ae734a51c35038388e98db",
                "MacAddress": "02:42:ac:11:00:02",
                "IPv4Address": "172.17.0.2/16",
                "IPv6Address": ""
            }
        },
        "Options": {
            "com.docker.network.bridge.default_bridge": "true",
            "com.docker.network.bridge.enable_icc": "true",
            "com.docker.network.bridge.enable_ip_masquerade": "true",
            "com.docker.network.bridge.host_binding_ipv4": "0.0.0.0",
            "com.docker.network.bridge.name": "docker0",
            "com.docker.network.driver.mtu": "1500"
        },
        "Labels": {}
    }
]
```


#Docker 
#Network
