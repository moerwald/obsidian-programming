
- `FROM` : A minimum distribution acting as base layer of your container.
- `ENV` : Environment variable, a way to set them. ENV-Vars are the main way to define info. Each `ENV` will be a separate layer in the container.
- `RUN`: runs shell scripts or commands (included in the base distribution). Using chaining via `&&` allow us to pack multiple commands in one layer.

```
RUN set -x\
    && groupadd
```

-  Logging should always be redirected to stdout and stderr. Never write to a log-file. There are log-drivers in Docker that will read stdout/stderr and forward them to logfile on the host.
- `EXPOSE` : Expose port on the virtual network. 
- `CMD`: Final command that will be run if a container is started.



#Docker 