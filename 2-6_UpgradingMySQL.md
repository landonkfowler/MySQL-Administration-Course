# 2-6 Upgrading MySQL

---

## Step 1 — Record the Server Version

Connect from the terminal:

```bash
mysql -u root -p
```

In the MySQL client, confirm the current version:

```sql
SELECT VERSION();
```

---

## Step 2 — Check the Available Version and Preview the Upgrade

Back at the terminal prompt:

```bash
sudo apt-get update
apt-cache policy mysql-community-server
sudo apt-get -s install mysql-server
```

- Review **Installed** and **Candidate** versions in the package policy output.
- Show the simulated transaction (using -s).
- Confirm the intended version and review the proposed package changes before continuing. 

---

## Step 3 — Apply the Upgrade

```bash
sudo apt-get install mysql-server
```

Review the proposed changes against the simulation before accepting. With `mysql-server` already installed, this command upgrades it along with the required MySQL packages. Oracle directs users to this targeted command for the server and client upgrade and documents that MySQL restarts automatically after the APT update. On startup, MySQL performs any required internal upgrade work. [Upgrading with the MySQL APT Repository](https://dev.mysql.com/doc/refman/9.7/en/linux-installation-apt-repo.html#repo-qg-apt-upgrading) · [What the upgrade process upgrades](https://dev.mysql.com/doc/refman/9.7/en/upgrading-what-is-upgraded.html)

---

## Step 4 — Verify the Service and Version

Check that the service is active and review recent startup messages. If startup fails, inspect the MySQL error log as well.

```bash
systemctl status mysql --no-pager
sudo journalctl -u mysql -n 50 --no-pager
mysql -u root -p
```

In the MySQL client, confirm the new version:

```sql
SELECT VERSION();
```