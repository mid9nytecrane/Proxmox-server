# Setting Up a File Server in Proxmox

## What Is a File Server? 🗄️

A file server is centralized, network-attached storage that lets multiple users share files with one another. You can also use it to store your personal files and access them remotely.

---

## Part 1: Creating a Container (CT) in Proxmox

> **Prerequisite:** Proxmox must already be installed on your machine (an old laptop or PC works fine for a homelab setup).

### Step 1 — Download the TurnKey Fileserver Template

1. Open the Proxmox web console.
2. In the left sidebar, go to **Datacenter > [Your Node] > local**.
3. Click **CT Templates > Templates**.
4. In the template browser, search for **"turnkey fileserver"**.
5. Select it and click **Download**.
6. Wait for the download to finish — the task popup will show **"Task OK"** (or "Task done"). Once it does, close the popup.

![Local storage view](Screenshot 2025-11-05 091152.png)

### Step 2 — Create the Container

1. Go to **CT Templates**, select the template you just downloaded, and click **Create CT**.

   ![Selecting downloaded template](Screenshot 2025-11-05 092948 2.png)

2. **General tab** — Set a hostname and password for the container, then click **Next**.

   ![General settings](Screenshot 2025-11-05 094512.png)

3. **Template tab** — Set storage to **local**, select your downloaded template from the dropdown, then click **Next**.

   ![Template selection](Screenshot 2025-11-05 094550.png)

4. **Disks tab** — Enter your preferred disk size, then click **Next**.

   ![Disk size](Screenshot 2025-11-05 094613.png)

5. **CPU tab** — Set cores to **2** (a file server doesn't need much CPU, so 2 cores is sufficient), then click **Next**.

   ![CPU cores](Screenshot 2025-11-05 094639.png)

6. **Memory tab** — Leave the default settings, then click **Next**.

   ![Memory settings](Screenshot 2025-11-05 094657.png)

7. **Network tab** — Configure as follows:
   - Check **IPv4**
   - Check **Static**
   - **IPv4/CIDR**: enter your preferred static IP address (e.g. `192.168.1.23/24`)
   - **Gateway (IPv4)**: enter your router's gateway address

   Then click **Next**.

   > ⚠️ **Note:** Make sure each octet in your IP address is between 0–255 (e.g. `192.168.1.23`, not `192.168.450.23`, which isn't a valid IPv4 address).

   ![Network configuration](Screenshot 2025-11-05 094714.png)

8. **DNS tab** — Leave the defaults, then click **Next**.

   ![DNS settings](Screenshot 2025-11-05 094733.png)

9. **Confirm tab** — Review your configuration summary, then click **Finish**.

   ![Confirmation screen](Screenshot 2025-11-05 094754.png)

---

## Part 2: Setting Up Samba (Windows File Sharing) on TurnKey

### Step 1 — Access Webmin

1. Enter the TurnKey container's IP address in your browser.
2. Click **Webmin**.

   ![Webmin login page](Screenshot 2025-12-31 022142.png)

3. If this is your first time connecting, click **Advanced > Accept the Risk and Continue** to bypass the self-signed certificate warning.
4. Log in to Webmin using the password you set when creating the container in Proxmox.

   ![Webmin dashboard](Screenshot 2025-12-31 022649.png)

### Step 2 — Create Users

1. In the left sidebar, select **System**.
2. Under System, click **Users and Groups**.

   ![Users and Groups](Screenshot 2025-12-31 020742.png)

3. Click **Create a new user** and fill in the required details for each user who needs access.

### Step 3 — Configure Samba Shares *(to complete)*

> This section is still in progress. Next steps to document:
> - Navigate to **Tools > Samba Windows File Sharing**
> - Create a new share and point it to your target directory
> - Set read/write permissions per user or group
> - Test access from a Windows/Mac/Linux client via the container's IP

---

### Notes
- Image links use Obsidian's `![[filename]]` embed syntax — re-open this file in Obsidian (with the images in the same vault) to see them rendered inline.
- Fixed a typo in the original IP example (`192.168.450.23/24` → not a valid address).
