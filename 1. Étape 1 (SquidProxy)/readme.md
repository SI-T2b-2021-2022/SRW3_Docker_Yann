# Squid Proxy

## Docker Hub

[Docker Hub](https://hub.docker.com/r/datadog/squid)

## docker-compose.yml

```yaml
version: '3.1'
services:
  squid:
    image: datadog/squid
    container_name: squid_proxy
    ports:
    - "80:3128"
    volumes:
      - /data/squid/cache:/var/spool/squid
      - /data/squid/log:/var/log/squid
```

### Explication docker-compose.yml

> **Image :** datadog/squid ← (repository/image docker)
**container_name :** squid_proxy ←(N’importe quel nom)
**ports :** redirection port 80 vers 3128
**volumes :** afin de consulter les logs et ce qui se trouve en cache les volumes on été monté dans un répertoire défini.
> 

## Sources

[How do I use squid as default gateway](https://stackoverflow.com/questions/37110365/how-do-i-use-squid-as-default-gateway)

[How to route all local trafic to Squid?](https://serverfault.com/questions/665950/how-to-route-all-local-trafic-to-squid)

---