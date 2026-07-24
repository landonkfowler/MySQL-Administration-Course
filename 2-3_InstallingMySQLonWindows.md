# 2-3 Installing MySQL on Windows

## Step 1: Install Microsoft Visual C++ Redistributable
- Go to https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170
- Download and install the version appropriate for your architecture under "Latest supported Redistributable version"

---

## Step 2: Download the MSI
- Go to https://dev.mysql.com/downloads/
- Go to "MySQL Community Server"
- Select your version
- Select your operating system
- Download the MSI installer

---

## Step 3: Run the MSI
- Run it as administrator
- Follow prompts

---

## Step 4: Configure with MySQL Configurator
- When the MSI finishes, leave the checkbox selected for running MySQL Configurator and click finish.

### Type and Networking
- Choose server config type:
  - **Development** — minimal memory (good for workstations)
  - **Server** — moderate memory
  - **Dedicated** — maximum memory
  - **Manual** — no optimization, use defaults
- Connectivity: TCP/IP enabled by default
  - Classic MySQL Protocol port: **3306**
  - X Protocol port: **33060**

### Accounts and Roles
- Set the **root password** (required)

### Windows Service
- MySQL runs as a Windows Service by default
- Service name: `MySQL97`
- Starts automatically at boot (default)
- Runs as Network Service under Standard System Account

### Server File Permissions
- Data folder: `C:\ProgramData\MySQL\MySQL Server 9.7\Data`
- Default: full control for service user and Administrators only

### Apply Configuration
- Click **Execute** to apply all settings
- Watch the Configuration Steps tab for progress

---

## Step 5: Verify
- Check the service with PowerShell
```powershell
Get-Service -Name MySQL97
```
- If in doubt about the name, run this
```powershell
Get-Service -Name "MySQL*"
```

---