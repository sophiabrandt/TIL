# Run Postgres Via Docker

For Postgres 18+:

```bash
docker container run --name postgres -p 5432:5432 \
  -e POSTGRES_PASSWORD=postgres \
  -v postgres-db:/var/lib/postgresql \
  --rm postgres
```
