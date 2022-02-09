# CAS

## Docker

### Docker Hub

[](https://hub.docker.com/r/jboss/keycloak/)

### docker-compose.yml

```yaml
version: '3.3'

volumes:
  postgres_data:
    driver: local
networks:
  srw3:
    driver: bridge

services:
  postgres:
    container_name: postgres-cas
    image: postgres
    hostname: postgres-cas
    volumes:
      - /data/postgre/data:/var/lib/postgresql/data
    environment:
      POSTGRES_DB: keycloak
      POSTGRES_USER: keycloak
      POSTGRES_PASSWORD: password
    networks:
      - srw3
  keycloak:
    image: jboss/keycloak
    container_name: keycloak
    hostname: keycloak
    environment:
      DB_VENDOR: POSTGRES
      DB_ADDR: postgres
      DB_DATABASE: keycloak
      DB_USER: keycloak
      DB_SCHEMA: public
      DB_PASSWORD: password
      KEYCLOAK_USER: admin
      KEYCLOAK_PASSWORD: Pa55w0rd
    ports:
      - 8080:8080
    depends_on:
       - postgres
    networks:
      - srw3
```

## Connexion LDAP

<aside>
👉 Connectez vous sur votre **keycloak**, puis connectez vous à l’”**Administration Console”**.

</aside>

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d3c04222-5ffe-4e91-89e9-b664e3869dfa/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e6e4ad7f-b1e5-4e81-8704-0a01e13982bd/Untitled.png)

<aside>
👉 Rendez vous ensuite sur “**User Federation”** puis sélectionnez dans “**Add provider...**“ ****“**LDAP**”

</aside>

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/da48f8ce-a2fb-4022-8e71-be36e2d20361/Untitled.png)

<aside>
👉 Maintenant configurez l’authentification comme ceci :

1. **READ_ONLY**
2. **Other**
3. **inetOrgPerson, organizationalPerson, person, top**
4. **ldap://openldap.root_srw3:389** 
(⚠️ Remplacez openldap.root_srw3 par la bonne ip/url de votre container docker)
5. **ou=People,dc=cpnv-srw3,dc=ch**
6. **cn=admin,dc=cpnv-srw3,dc=ch** (Et le mot de passe)

</aside>

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ac66c1a7-d1a9-411f-a26f-6f55bb151c75/Untitled.png)

<aside>
👉 Si tout s’est bien passé vous devriez pouvoir tester la connexion avec les boutons : 
**Test Connection
Test Authentification**

</aside>

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a6be992d-9b58-4ff7-ad85-6733d1680622/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e3316385-d554-4016-9daa-0579d8b12b66/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0d378ea1-3e6d-49e1-a1c1-774d2ac736cd/Untitled.png)

<aside>
👉 Une fois l’**User Federation** sauvegardé effectuez une synchronisation de tout les utilisateurs.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/16b0c2c6-24bb-4217-be60-ddfe0310900f/Untitled.png)

</aside>

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/839521a9-9ada-498a-ae53-ab9e1003fdd2/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9f12c4e2-200b-4d28-9a5d-8b5c7e376013/Untitled.png)

## Sources

[](https://github.com/keycloak/keycloak-containers)

[](https://www.keycloak.org/getting-started/getting-started-docker)

[Configuring Keycloak for active directory and LDAP integration](https://dmc.datical.com/administer/configure-keycloak-ldap.htm)

[Setting up a user federation with Keycloak (LDAP integration)](https://documentation.abas.cloud/en/abas-keycloak/setup-user-federation-ldap.html)