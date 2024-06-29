# Connect to MySQL/MariaDB Via Docker

From [“Connect to MySQL running in Docker container from a local machine”](https://towardsdatascience.com/connect-to-mysql-running-in-docker-container-from-a-local-machine-6d996c574e55):

> By default, MySQL restricts connection other than the local machine (here Docker container) for security reasons. So, to connect from the local machine, you have to change the connection restriction:

```bash
mysql> update mysql.user set host = ‘%’ where user=’root’;
Query OK, 1 row affected (0.02 sec)
```

> Although for security reasons, it would be better to create a new non-admin user and grant access to that user only.

## Docker with MariaDB

Example MariaDB docker container instance with [yobasystems/alpine-mariadb][alpinemariadb], a lightweight container image:

```bash
docker run --name mariadb -p 33067:3306 -v /var/lib/mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root_pass -d yobasystems/alpine-mariadb
```

The command will create a container named `mariadb` with a root password (`root_pass`). You can connect to the database via `localhost` on port 33067.

## Setup User and Database

Example SQL script for setting up a user _with all privileges and without connectionRestriction_:

```sql
-- 01-user-setup.sql
CREATE USER 'myuser'@'%' IDENTIFIED BY 'mypass';

GRANT ALL PRIVILEGES ON * . * TO 'myuser'@'%';
```

Now, let's run these scripts via docker:

```bash
docker exec -i mariadb sh -c 'mysql --host=localhost --user=root --password=root_pass' < 01-user-setup.sql
```

Explanation:

`exec -i mariadb`: run a command in a running container with stdin (`-i`) — we named the database container `mariadb`

`sh -c`: run a shell script with a command string operand

`'mysql --host=localhost --user=root --password=root_pass'`: this is the command we are running _inside_ the container

`< 01-user-setup.sql`: read the file from stdin (on your local computer)

[alpinemariadb]: https://hub.docker.com/r/yobasystems/alpine-mariadb/
