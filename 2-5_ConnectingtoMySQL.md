# 2-5 Connecting to MySQL

---

## Part 1: Local Connection via `mysql` Shell Client

On the Linux VM (SSH session or terminal):

1. Connect locally using the default socket:
   ```
   mysql -u root -p
   ```
   - Enter password when prompted
   - No `-h` flag is given, so `localhost` is assumed → socket connection

2. Confirm you're connected:
   ```sql
   STATUS;
   ```
   - Notice the `UNIX socket` line in the output

3. Show users and note hosts (for later):
   ```sql
   SELECT User, Host FROM mysql.user;
   ```

4. Exit:
   ```sql
   exit
   ```

5. Reconnect forcing TCP/IP instead of socket:
   ```
   mysql -h 127.0.0.1 -u root -p
   ```
   - Run `STATUS;` again — notice the connection now shows `TCP/IP` instead of socket

7. Exit:
   ```sql
   exit
   ```

---

## Part 2: Remote Connection via `mysql` Shell Client

From your **local machine's** terminal (not the VM):

1. Attempt to connect to the VM using its public IP:
   ```
   mysql -h <vm-public-ip> -u root -p
   ```

2. **Expected failure** (if `root` is `'root'@'localhost'` only):
   ```
   ERROR 1130 (HY000): Host '...' is not allowed to connect to this MySQL server
   ```
   - This is a great example of local-vs-remote user definition

3. Connect using a remote-capable demo account instead (e.g. `delmar`):
   ```
   mysql -h <vm-public-ip> -u delmar -p
   ```

4. Confirm success:
   ```sql
   STATUS;
   SHOW DATABASES;
   exit
   ```

---

## Part 3: GUI Connection via MySQL Shell for VS Code

On your local machine, in VS Code:

1. Open the Extensions view (`Cmd+Shift+X` / `Ctrl+Shift+X`)
2. Search for **"MySQL Shell for VS Code"** (publisher: Oracle)
3. Click **Install**, follow any prompts, and restart VS Code if prompted
4. Open the MySQL Shell icon in the Activity Bar
5. In the **DATABASE CONNECTIONS** view, click **+** to create a new connection
6. Fill in connection details:
   - Caption: `MySQL Demo VM`
   - Hostname: `<vm-public-ip>`
   - Port: `3306`
   - User name: `delmar`
7. Click **OK**, then open a SQL Script window from the new connection
8. Enter password when prompted
9. In the script, run:
   ```sql
   SELECT VERSION();
   SHOW DATABASES;
   ```
10. Notice that both the schema browser tree on the left and the result grid have the same output

---

## Takeaways

- Same underlying connection concepts (host, port, user, password) apply whether using CLI or GUI
- `localhost` → socket; `127.0.0.1` or a remote IP → TCP/IP
- A user account is scoped by host (`user@host`) — this is why `root` failed remotely but `delmar` succeeded