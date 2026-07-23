# Installing MySQL on Linux

This guide covers installing MySQL on Ubuntu using the MySQL APT Repository.

---

## Step 1 — Download the MySQL APT Config Package

Download the `mysql-apt-config` package from Oracle's official repository:

```bash
wget https://dev.mysql.com/get/mysql-apt-config_0.8.39-1_all.deb
```

---

## Step 2 — Install the Config Package

```bash
sudo dpkg -i mysql-apt-config_0.8.39-1_all.deb
```

An interactive dialog will appear (text-based, works over SSH). Use it to select the MySQL server version to install.

Select **Ok** when done.

---

## Step 3 — Update the Package Index

```bash
sudo apt-get update
```

This step is mandatory — it loads the MySQL package metadata from the newly added repository.

---

## Step 4 — Install MySQL Server

```bash
sudo apt-get install mysql-server
```

This installs the MySQL server, client, and database common files. During installation you will be prompted to set a password for the `root` account.

---

## Step 5 — Verify the Service is Running

MySQL starts automatically after installation. Confirm it is running:

```bash
systemctl status mysql
```

---

## Step 6 — Secure the Installation

This is optional, but recommended. (More details on configuration in later lessons.)

```bash
sudo mysql_secure_installation
```

This interactive script helps you:

- Set (or change) the `root` password
- Remove anonymous users
- Disable remote `root` login
- Remove the test database