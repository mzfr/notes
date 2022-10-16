# Matrix

- `mkdir matrix`
- Run the following command inside the matrix directory:
```bash
sudo docker run -it --rm \
    -v "/home/mzfr/matrix/synapse:/data" \
    -e SYNAPSE_SERVER_NAME=chat.mzfr.in \
    -e SYNAPSE_REPORT_STATS=yes \
    matrixdotorg/synapse:latest generate
```

- Edit the generated `homeserver.yml`. We will use postgres instead of sqlite
```yml
database:
  name: psycopg2
  args:
    user: synapse
    password: STRONGPASSWORD
    database: synapse
    host: postgres
    cp_min: 5
    cp_max: 10
```

- In the `matrix` directory put this(https://github.com/vector-im/element-web/blob/develop/config.sample.json) config.
		- Make sure to edit the `base_url` and `server_name`
- Put the following in the compose file:

The following docker-compose:

```docker
version: '3'
services:
  postgres:
    image: postgres:14
    restart: unless-stopped
    networks:
      - matrix
    volumes:
     - /home/mzfr/matrix/postgresdata:/var/lib/postgresql/data

    # These will be used in homeserver.yaml later on
    environment:
     - POSTGRES_DB=synapse
     - POSTGRES_USER=synapse
     - POSTGRES_PASSWORD=STRONGPASSWORD
     - POSTGRES_INITDB_ARGS='--encoding=UTF-8 --lc-collate=C --lc-ctype=C'
  element:
    image: vectorim/element-web:latest
    restart: unless-stopped
    networks:
      - matrix
    volumes:
      - /home/mzfr/matrix/element-config.json:/app/config.json
        
  synapse:
    image: matrixdotorg/synapse:latest
    restart: unless-stopped
    networks:
      - matrix
    volumes:
     - /home/mzfr/matrix/synapse:/data

networks:
  matrix:
    driver: bridge
```

***

Last time I did this I was getting: 
```
2022-10-16 14:18:23,325 - synapse.app._base - 207 - ERROR - main - Exception during startup

Traceback (most recent call last):

  File "/usr/local/lib/python3.9/site-packages/synapse/app/homeserver.py", line 375, in setup

    hs.setup()

  File "/usr/local/lib/python3.9/site-packages/synapse/server.py", line 309, in setup

    self.datastores = Databases(self.DATASTORE_CLASS, self)

  File "/usr/local/lib/python3.9/site-packages/synapse/storage/databases/__init__.py", line 67, in __init__

    engine.check_database(db_conn)

  File "/usr/local/lib/python3.9/site-packages/synapse/storage/engines/postgres.py", line 101, in check_database

    raise IncorrectDatabaseSetup(

synapse.storage.engines._base.IncorrectDatabaseSetup: ("Database has incorrect collation of %r. Should be 'C'\nSee docs/postgres.md for more information. You can override this check bysetting 'allow_unsafe_locale' to true in the database config.", 'en_US.utf8')

**********************************************************************************

 Error during initialisation:

    ("Database has incorrect collation of %r. Should be 'C'\nSee docs/postgres.md for more information. You can override this check bysetting 'allow_unsafe_locale' to true in the database config.", 'en_US.utf8')

 There may be more information in the logs.
```
