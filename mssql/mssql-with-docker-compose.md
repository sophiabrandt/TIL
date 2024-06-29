# MSSQL with docker compose

docker-compose file for local development:

```yaml
services:
  server:
    image: mcr.microsoft.com/mssql/server:2022-latest
    user: root
    environment:
      - ACCEPT_EULA=Y
      - MSSQL_SA_PASSWORD=yourStrong(!)Password
    ports:
      - 1433:1433
    volumes:
      - db-data:/var/opt/mssql/data
      - db-log:/var/opt/mssql/log
      - db-secrets:/var/opt/mssql/secrets
    platform: linux/amd64

volumes:
  db-data:
  db-log:
  db-secrets:
```

Usage example:

```
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "ConnectionStrings": {
    "sqlConnection": "Server=localhost,1433;Database=CompanyEmployee;User Id=sa;Password=yourStrong(!)Password;Integrated Security=False;TrustServerCertificate=True;MultipleActiveResultSets=True;"
  },
  "AllowedHosts": "*"
}
```
