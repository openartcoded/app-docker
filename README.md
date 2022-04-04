## Installation guide

https://openartcoded.github.io/doc/installation/compiled.html

## Misc
### Exporting realm

* uncomment volumes in docker-compose dev
    ```
        # - ./keycloak/realms/export:/tmp/export
    ```
* run the command:

    ```
    docker exec -it app-docker_keycloak_1 /opt/jboss/keycloak/bin/standalone.sh \
    -Djboss.socket.binding.port-offset=100 \
    -Dkeycloak.migration.action=export \
    -Dkeycloak.migration.provider=singleFile \
    -Dkeycloak.migration.realmName=Artcoded \
    -Dkeycloak.migration.usersExportStrategy=REALM_FILE \
    -Dkeycloak.migration.file=/tmp/export/artcoded-realm.json
    ```
