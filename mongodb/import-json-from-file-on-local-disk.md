# Import Json From File On Local Disk

Assuming we have a Mongo DB database setup via Docker/Docker-Compose and want to import via `stdin`:

```bash
 docker exec -i <name of container> sh -c 'mongoimport --host=127.0.0.1 --port=<port> --jsonArray --user=<root user> --password=<root password> -d <database name> -c <collection name>' < <path to json file on disk>
```

## Detailed Example

Example `docker-compose.yml`:

```yaml
version: "3.8"

services:
  mongo:
    image: mongo:4.0.24-xenial
    command: --port 23087
    ports:
      - "23087:23087"
    environment:
      - MONGO_INITDB_ROOT_USERNAME=root
      - MONGO_INITDB_ROOT_PASSWORD=password
      - MONGO_INITDB_DATABASE=db
    healthcheck:
      test: '[ `echo ''db.runCommand("ping").ok'' | mongo localhost/db --quiet` ] && echo 0 || echo 1'
      interval: 5s
      start_period: 10s
      timeout: 4s
      retries: 3

  mongo-express:
    image: mongo-express:0.54.0
    ports:
      - "8099:8081"
    environment:
      - ME_CONFIG_MONGODB_ADMINUSERNAME=root
      - ME_CONFIG_MONGODB_ADMINPASSWORD=password
      - ME_CONFIG_MONGODB_PORT=23087
```

You run `docker-compose up -d`. Then `docker-compose ps`.

Output in console:

```bash
angular-mean-shop_mongo-   tini -- /docker-           Up             0.0.0.0:8099->8081/tcp,:
express_1                  entrypoint ...                            ::8099->8081/tcp
angular-mean-              docker-entrypoint.sh       Up (healthy)   0.0.0.0:23087->23087/tcp
shop_mongo_1               --por ...                                 ,:::23087->23087/tcp,
                                                                     27017/tcp
```

You have data on your local disk under `./seed-data/orders.json`.

That means the import command would look like this:

```bash
 docker exec -i angular-mean-shop_mongo_1 sh -c 'mongoimport --host=127.0.0.1 --port=23087 --jsonArray --user=root --password=password -d admin -c orders' <  ./seed-data/orders.json
```

Normally, you should be able to use `docker-compose exec -T`, too, but on my computer it did not work.
