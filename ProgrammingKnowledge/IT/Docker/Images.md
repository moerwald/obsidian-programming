
Ein Image besteht aus Binaries und Metadata. `docker image inspect` returnt Information über Metadata.
Docker Images bestehen aus verschiedenen Layers (= Layer of Changes).

## Image Layers

 Man kann sich die Histroy eines Images über 

```
moerwald@T16-AMewald:~$ docker image history nginx:latest
IMAGE          CREATED       CREATED BY                                      SIZE      COMMENT
92b11f67642b   5 weeks ago   CMD ["nginx" "-g" "daemon off;"]                0B        buildkit.dockerfile.v0
<missing>      5 weeks ago   STOPSIGNAL SIGQUIT                              0B        buildkit.dockerfile.v0
<missing>      5 weeks ago   EXPOSE map[80/tcp:{}]                           0B        buildkit.dockerfile.v0
<missing>      5 weeks ago   ENTRYPOINT ["/docker-entrypoint.sh"]            0B        buildkit.dockerfile.v0
<missing>      5 weeks ago   COPY 30-tune-worker-processes.sh /docker-ent…   4.62kB    buildkit.dockerfile.v0
<missing>      5 weeks ago   COPY 20-envsubst-on-templates.sh /docker-ent…   3.02kB    buildkit.dockerfile.v0
<missing>      5 weeks ago   COPY 15-local-resolvers.envsh /docker-entryp…   336B      buildkit.dockerfile.v0
<missing>      5 weeks ago   COPY 10-listen-on-ipv6-by-default.sh /docker…   2.12kB    buildkit.dockerfile.v0
<missing>      5 weeks ago   COPY docker-entrypoint.sh / # buildkit          1.62kB    buildkit.dockerfile.v0
<missing>      5 weeks ago   RUN /bin/sh -c set -x     && groupadd --syst…   112MB     buildkit.dockerfile.v0
<missing>      5 weeks ago   ENV PKG_RELEASE=1~bookworm                      0B        buildkit.dockerfile.v0
<missing>      5 weeks ago   ENV NJS_VERSION=0.8.3                           0B        buildkit.dockerfile.v0
<missing>      5 weeks ago   ENV NGINX_VERSION=1.25.4                        0B        buildkit.dockerfile.v0
<missing>      5 weeks ago   LABEL maintainer=NGINX Docker Maintainers <d…   0B        buildkit.dockerfile.v0
<missing>      5 weeks ago   /bin/sh -c #(nop)  CMD ["bash"]                 0B
<missing>      5 weeks ago   /bin/sh -c #(nop) ADD file:b86ae1c7ca3586d8f…   74.8MB
```

ansehen.

Jeder Layer hat einen Hashcode (=`Unique SHA`). Im Dockerfile erstellt jeder Befehl einen Layer. Hat sich der Hashcode eines Layers geändert, werden alle nachfolgenden Layer neu erstellt. Layer werden lokal gecasht. Somit ist jeder Layer nur einmal auf dem Host Filesystem gespeichert.
## Union File System



