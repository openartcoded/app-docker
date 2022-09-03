## Installation guide

https://openartcoded.github.io/doc/installation/compiled.html

## Misc
### Exporting realm

* uncomment volumes in docker-compose dev
    ```
        # - ./config/keycloak-dev/export:/tmp/export
    ```
* run the command:

    ```
    docker exec -it app-docker_keycloak_1 /opt/keycloak/bin/kc.sh export \
    --file /tmp/export/artcoded-realm.json \
    --realm Artcoded
    --users single_file
    ```
> On windows you should use "-" instead of "_" & you can't use "\" apparently, e.g :

   ```
      docker exec -it app-docker-keycloak-1 /opt/keycloak/bin/kc.sh export --file /tmp/export/artcoded-realm.json  --realm Artcoded --users single_file
   ```


### Importing realm

* move the exported realm to `config/keycloak-dev/import`

* run the command:

    ```
    docker exec -it app-docker_keycloak_1 /opt/keycloak/bin/kc.sh import \
    --file /tmp/import/artcoded-realm.json
    ```
    
> On windows you should use "-" instead of "_" & you can't use "\" apparently, e.g :


       docker exec -it app-docker-keycloak-1 /opt/keycloak/bin/kc.sh import  --file /tmp/import/artcoded-realm.json
 
    
* restart the stack
    ```
    docker-compose restart
    ```

### Misc

#### mount volume docker
udisksctl mount -b /dev/sda1
#### list volumes
lsblk -o NAME,FSTYPE,LABEL,SIZE,MOUNTPOINT
#### disable docker
sudo systemctl disable docker.service docker.socket
