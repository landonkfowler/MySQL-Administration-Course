# 2-4 Running MySQL in a Container

## Prerequisites

- Docker Desktop installed and running
- Internet access to pull from the Oracle Container Registry

---

## Step 1: Pull the Image

Pull the MySQL 9.7 image from the Oracle Container Registry:

```bash
docker pull container-registry.oracle.com/mysql/community-server:9.7
```

Confirm the image was downloaded:

```bash
docker images
```

---

## Step 2: Start a Container

Run a new MySQL container in detached mode:

```bash
docker run --name mysql-demo --restart on-failure -e MYSQL_ROOT_PASSWORD=MyPassword1! -d container-registry.oracle.com/mysql/community-server:9.7
```

- `docker run` — Creates and starts a new container
- `--name mysql-demo` — Assigns the container a human-readable name instead of a random one
- `--restart on-failure` — Automatically restarts the container if MySQL stops unexpectedly — required to support the `RESTART` SQL statement
- `-e MYSQL_ROOT_PASSWORD=MyPassword1!` — Sets the root password via environment variable, skipping the auto-generated password flow
- `-d` — Runs the container in the background (detached mode), so the terminal isn't tied up
- `container-registry.oracle.com/mysql/community-server:9.7` — The full image name — Oracle's registry, the Community Server repository, pinned to the `9.7` tag

Check that the container is running:

```bash
docker ps --format "table {{.Names}}\t{{.Status}}\t{{.Ports}}"
```

> Wait until `STATUS` shows that it's running before connecting.

View the container logs:

```bash
docker logs mysql-demo
```

---

## Step 3: Connect to MySQL

Open the MySQL client inside the running container:

```bash
docker exec -it mysql-demo mysql -uroot -p
```

Enter the root password when prompted (`MyPassword1!`), then run SQL commands such as these:

```sql
SELECT VERSION();
SHOW DATABASES;
exit
```

---

## Step 4: Shell Access

Open a bash shell inside the container:

```bash
docker exec -it mysql-demo bash
```

View the MySQL data directory:

```bash
ls /var/lib/mysql
exit
```

---

## Step 5: Stop, Start, and Clean Up

Stop and restart a container:

```bash
docker stop mysql-demo
docker start mysql-demo
```

Remove the container (stop it first):

```bash
docker stop mysql-demo
docker rm mysql-demo
```