

## Konfiguration

Detailierte Info zur Config gibt es [hier](https://github.com/marcel-dempers/docker-development-youtube-series/tree/master/storage/databases/postgresql/2-configuration). Hauptsächlich sollte die Config über Config-Files erfolgen, da diese Files versionierbar sind. Nur relativ wenig sollte über Env-Variablen laufen.


>[!warn]
>Never rely on default values. Always define as much as possible.


### Files

- PG_IDENT.CONF -> [map OS-Users to DB-Users](https://www.youtube.com/watch?v=WyWCa6WVx60&list=PLHq1uqvAteVsnMSMVp-Tcb0MSBVKQ7GLg&index=2).
- PG_HBA.CONF -> [HBA](https://www.youtube.com/watch?v=WyWCa6WVx60&list=PLHq1uqvAteVsnMSMVp-Tcb0MSBVKQ7GLg&index=2)= Host Based Authentication, ist im Prinzip eine Postgres Firewall Config. 
- POSTGRES.CONF -> Main Postgres Configuration.


## Replica

Sehr gute Erklärung findet sich [hier](https://github.com/marcel-dempers/docker-development-youtube-series/blob/master/storage/databases/postgresql/3-replication/README.md) .



#Postgre 