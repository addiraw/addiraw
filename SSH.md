Sure ✅ Here’s the entire conversation’s details written directly in **Markdown format** (no extra wrapping, ready to use as `.md`):

# AWS SSH and Linux Command Guide

This guide covers how to connect to AWS EC2 via SSH, set proper permissions on key files, and handle directories or files with spaces in their names.

---

## 🔑 Connecting to AWS EC2 with SSH

### Prerequisites

1. **EC2 Instance** running on AWS.
2. **Key Pair (.pem file)** downloaded when you launched the instance.
3. **Public IP / DNS** of the EC2 instance (AWS Console → EC2 → Instances).
4. **SSH client** installed:

   * Linux/macOS → built-in.
   * Windows → PowerShell or PuTTY.

---

### Steps (Linux / macOS / Windows with PowerShell)

1. **Locate your `.pem` key file**
   Example: `my-key.pem`

2. **Set correct file permissions**:

   ```bash
   chmod 400 my-key.pem
   ```

3. **Connect via SSH**:

   ```bash
   ssh -i my-key.pem ec2-user@<PUBLIC-IP-OR-DNS>
   ```

   Replace:

   * `my-key.pem` → your key filename.
   * `ec2-user` → depends on AMI:

     * Amazon Linux → `ec2-user`
     * Ubuntu → `ubuntu`
     * CentOS → `centos`
     * RHEL → `ec2-user` or `ec2-user`
   * `<PUBLIC-IP-OR-DNS>` → e.g., `54.123.45.67` or `ec2-54-123-45-67.compute-1.amazonaws.com`

   Example:

   ```bash
   ssh -i my-key.pem ubuntu@54.123.45.67
   ```

---

### Windows with PuTTY

1. Convert `.pem` → `.ppk` using **PuTTYgen**.
2. Open **PuTTY** → enter your **Public IP** in “Host Name”.
3. Under **SSH → Auth**, browse and select `.ppk` key file.
4. Click **Open** to connect.

---

### Troubleshooting

* **Permission denied**:

  * Check you used the correct username (`ubuntu`, `ec2-user`, etc.).
  * Verify `.pem` file permissions (`chmod 400`).

* **Connection timed out**:

  * Ensure **Security Group** allows inbound SSH (port `22`).
  * Use **public IP/DNS**, not private.

---

## 🔐 Understanding `chmod` for Key Files

To use a `.pem` key, permissions must be restricted so **only the owner can read it**.

```bash
chmod 400 my-key.pem
```

* `4` → read permission
* `0` → no write/execute permission
* `400` → **owner can read, nobody else can do anything**

### Why not `chmod 777` or `chmod 644`?

Too open → SSH will throw:

```
Permissions 0644 for 'my-key.pem' are too open.
```

✅ After `chmod 400`, you can safely connect:

```bash
ssh -i my-key.pem ubuntu@<PUBLIC-IP>
```

---

## 📂 Handling Directories with Spaces

When a directory (or file) has spaces in its name, you must **quote or escape** it.

### 1. Use Quotes

```bash
cd "My Folder"
```

or

```bash
cd 'My Folder'
```

### 2. Use Backslash Escaping

```bash
cd My\ Folder
```

### 3. Use Tab Completion (Recommended)

Type a few letters, then press **Tab**:

```bash
cd My<tab>
```

This auto-completes to:

```bash
cd My\ Folder
```

---

## ✅ Notes

* These techniques apply in **AWS EC2** as well as local Linux/macOS terminals.
* Use the same quoting/escaping methods with `cat`, `nano`, or `vim` to open files with spaces.

---

Would you like me to also extend this with a **quick-reference cheat sheet section** at the end (like a one-page summary of all commands)?
