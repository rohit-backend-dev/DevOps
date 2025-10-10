# ☁️ AWS EC2: Create and Connect a Virtual Machine (VM) Using Windows + MobaXterm

## 🧩 Step 1: Log in to Your AWS Account

### 🔗 Link → [https://aws.amazon.com/console](https://aws.amazon.com/console)

1. Click **“Sign In to the Console.”**
2. Enter your **root** or **IAM** credentials.
   (If you don’t have one, create a **free AWS account** → [https://aws.amazon.com/free](https://aws.amazon.com/free))
3. Once logged in → type **EC2** in the **search bar** and click it.

📍 You’ll now be inside the **EC2 Dashboard** — this is where you manage your virtual machines.

---

## ⚙️ Step 2: Create a New Virtual Machine (EC2 Instance)

### 🖱️ Click → **Launch Instance**

You’ll see a form — fill it carefully 👇

---

### 🧱 **1. Name and Tags**

* Name it something simple:

  ```
  MyFirstVM
  ```

---

### 🪟 **2. Choose the Operating System (AMI)**

You’ll see a list of “Amazon Machine Images (AMI)”
Pick one according to your need:

| Type        | Recommended Image                            | Link                                                                 |
| ----------- | -------------------------------------------- | -------------------------------------------------------------------- |
| **Linux**   | Ubuntu Server 22.04 LTS (Free-tier eligible) | [Ubuntu AMI Info](https://cloud-images.ubuntu.com/locator/)          |
| **Windows** | Microsoft Windows Server 2019 Base           | [Windows AMI Info](https://aws.amazon.com/marketplace/pp/B07QQB7GXJ) |

👉 For DevOps practice, **choose “Ubuntu Server 22.04 LTS”**.

---

### ⚡ **3. Instance Type**

Choose:

```
t2.micro
```

✅ Free-tier eligible (1 CPU, 1 GB RAM)

---

### 🔐 **4. Key Pair (Login Credentials)**

1. Click **Create new key pair**
2. Enter name: `mykeypair`
3. Key pair type: `RSA`
4. File format: `.pem`
5. Click **Create key pair**

💾 A file `mykeypair.pem` will be **downloaded automatically** —
**save it safely** (you’ll need it to log in).

📂 Example location:

```
C:\Users\Rohit\Downloads\mykeypair.pem
```

---

### 🌐 **5. Network Settings**

1. Select “Allow SSH traffic from anywhere” (for now)
2. Later, you can restrict it to your IP for security.

---

### 💾 **6. Storage**

Keep default:

```
8 GiB (Free tier)
```

---

### ✅ **7. Launch Instance**

Click **Launch instance** → wait 30–40 seconds.

🎉 You’ve created your first **EC2 virtual machine (VM)**!

---

## 🧠 Step 3: Check Your Instance

Go to → **EC2 Dashboard → Instances → Running Instances**

You’ll see something like:

```
Instance ID: i-0abcd1234
Instance state: Running
Public IPv4 address: 3.111.87.201
```

📌 Copy the **Public IPv4 address** —
You’ll use it to connect from MobaXterm.

---

## 💻 Step 4: Connect Using MobaXterm (on Windows)

---

### 🧰 Step 4.1 – Install MobaXterm

🔗 Download Link → [https://mobaxterm.mobatek.net/download.html](https://mobaxterm.mobatek.net/download.html)

1. Choose **Home Edition → Installer edition**
   (example: `MobaXterm_Installer_v24.2.exe`)
2. Install normally (Next → Next → Finish)
3. Open **MobaXterm**

---

### 🔑 Step 4.2 – Load Your Private Key (.pem file)

You can use `.pem` directly in new MobaXterm versions.
If yours doesn’t support it:

1. Open **MobaKeyGen** (comes with MobaXterm)
   📍 Shortcut: MobaXterm → Tools → MobaKeyGen
2. Click **Load** → select your `mykeypair.pem`
3. Click **Save private key** → name it `mykeypair.ppk`

Now you have `mykeypair.ppk` for older SSH tools too.

---

### 🌐 Step 4.3 – Create SSH Session in MobaXterm

1. Click **Session → SSH**
2. Fill out:

   * **Remote host:** your EC2 **Public IPv4 address** (e.g. `3.111.87.201`)
   * **Username:**

     * For Ubuntu: `ubuntu`
     * For Amazon Linux: `ec2-user`
3. Go to **Advanced SSH settings**

   * Check ✅ “Use private key”
   * Browse and select your **`mykeypair.pem`**
4. Click **OK → Connect**

---

### 🔐 Step 4.4 – Accept Fingerprint

When asked:

```
Are you sure you want to continue connecting (yes/no)?
```

Type `yes` → hit Enter.

You’ll now see:

```bash
Welcome to Ubuntu 22.04 LTS
ubuntu@ip-172-31-xx-xx:~$
```

✅ You are now inside your EC2 Virtual Machine!

---

## 🧰 Step 5: Test and Install Something

Try running a few commands:

```bash
whoami               # should show 'ubuntu'
ls                   # list files
sudo apt update      # update package list
sudo apt install nginx -y  # install a web server
```

When done, open your **browser** →
Go to `http://<your-public-ip>` (like `http://3.111.87.201`)

If you see the **Nginx welcome page**, your VM is running a web server successfully 🎉

---

## 🔒 Step 6: Stop or Terminate to Avoid Charges

1. Go back to your **EC2 Dashboard**
2. Select your instance → **Instance state**

   * Choose **Stop** → keeps the VM (no compute charge)
   * Choose **Terminate** → deletes everything (permanent)

💡 Stopping is safer if you want to reuse it later.

---

## 🧭 Summary Table

| Step | Action                  | Tool/Website       | Link                                                                               |
| ---- | ----------------------- | ------------------ | ---------------------------------------------------------------------------------- |
| 1    | Sign in to AWS Console  | Browser            | [aws.amazon.com/console](https://aws.amazon.com/console)                           |
| 2    | Launch new EC2 instance | AWS EC2            | [EC2 Dashboard](https://console.aws.amazon.com/ec2/)                               |
| 3    | Download `.pem` key     | Browser            | Auto-download                                                                      |
| 4    | Install MobaXterm       | MobaXterm          | [mobaxterm.mobatek.net/download.html](https://mobaxterm.mobatek.net/download.html) |
| 5    | Connect via SSH         | MobaXterm          | –                                                                                  |
| 6    | Test server (Nginx)     | Browser + Terminal | –                                                                                  |
| 7    | Stop/Terminate instance | AWS Console        | –                                                                                  |

---
