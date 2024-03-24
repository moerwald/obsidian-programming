

[Referenz]([windows - How to Allow Remote Access to PostgreSQL database - Stack Overflow](https://stackoverflow.com/questions/18580066/how-to-allow-remote-access-to-postgresql-database))


Im File `**pg_hba.conf**` folgendes setzen:


```sql
host    all             all              0.0.0.0/0                       md5
host    all             all              ::/0                            md5
```

Im `**postgresql.conf**` muss folgendes aktiv sein:

```
 listen_addresses = '*'
```

#Postgre 
#Database 