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


### Expenses & Reminder Tasks features

Expenses management & reminder tasks use email to receive expenses from a known email address (in the case of expenses),
and send email in case of a reminder task. To test both features, follow these instructions:

- Add to /etc/hosts:

```
127.0.1.1       mail.somehost.org
```

- Down the stack (if it's already running):

```
docker-compose down
```

- Restart it:

```
docker-compose up -d
```

- On the top-right  of `https://backoffice.somehost.org`, click on "Personal Info" then "Contact/Bank"
   and change the email address to `noreply@somehost.com`

- Open a new tab & Go to `https://mail.somehost.org` . You can login with `username: noreply@somehost.com , password: noreply`

- Send an email with an attachment (pdf or image) to `fee@somehost.com` => after a few seconds you should see a notification coming in on `https://backoffice.somehost.org`

- Create a new reminder task. Choose "Send Mail" . Once the task is triggered, go back to `https://mail.somehost.org` and login. 
  you should see an email with the reminder.


#### If you get multiple warnings from your browser when opening the link, this is normal. Certificates are self-signed (only local)


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