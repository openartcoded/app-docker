# app-artcoded

docker stack for artcoded

## Installation 

### Prerequisites

- Install docker
- Install docker-compose

- add the following to your /etc/hosts:

```
127.0.1.1       auth.somehost.org
127.0.1.1       somehost.org
127.0.1.1       backoffice.somehost.org
```

### development backend + frontend
- if it's the first time, run inside this directory: `cp .env.monorepo.example .env`

- run: `docker-compose build`
- once done, run: `docker-compose up -d`
### development frontend only
- if it's the first time, run inside this directory: `cp .env.dev.example .env`

- once done, run: `docker-compose up -d`

- Open a private browser's window and go to `https://backoffice.somehost.org`
    - default username: `nordine`
    - default password: `1234`

- you can then run `ng serve` in `backoffice`or `website`

#### If you get multiple warnings from your browser when opening the link, this is normal. Certificates are self-signed (only local)



## Misc
### Exporting realm

* uncomment volumes in docker-compose dev
    ```
        # - ./config/keycloak-dev:/tmp/realms
    ```
* run the command:

    ```
    docker exec -it app-artcoded_keycloak_1 /opt/jboss/keycloak/bin/standalone.sh \
    -Djboss.socket.binding.port-offset=100 \
    -Dkeycloak.migration.action=export \
    -Dkeycloak.migration.provider=singleFile \
    -Dkeycloak.migration.realmName=Artcoded \
    -Dkeycloak.migration.usersExportStrategy=REALM_FILE \
    -Dkeycloak.migration.file=/tmp/export/artcoded-realm.json
    ```