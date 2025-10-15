### 🧩 **Basic Syntax**

```bash
chmod [options] [permissions] [file]
```

---

### 🔐 **Permission Types**

Each file or directory has **three permission sets**:

| Type  | User    | Group   | Others  |
| ----- | ------- | ------- | ------- |
| **r** | Read    | Read    | Read    |
| **w** | Write   | Write   | Write   |
| **x** | Execute | Execute | Execute |

---

### 🧮 **Permission Numbers (Octal Representation)**

| Symbol | Number | Meaning       |
| ------ | ------ | ------------- |
| `r`    | 4      | Read          |
| `w`    | 2      | Write         |
| `x`    | 1      | Execute       |
| `-`    | 0      | No permission |

Combine them per category:

* `7` → `rwx`
* `6` → `rw-`
* `5` → `r-x`
* `4` → `r--`

---

### ⚙️ **Examples**

| Command               | Meaning                              |
| --------------------- | ------------------------------------ |
| `chmod 777 file.txt`  | Full access for everyone             |
| `chmod 755 script.sh` | Owner can rwx, others can rx         |
| `chmod 644 file.txt`  | Owner rw, others read-only           |
| `chmod +x script.sh`  | Add execute permission               |
| `chmod -w file.txt`   | Remove write permission              |
| `chmod u+x file.sh`   | Add execute permission for user only |
| `chmod g-w file.txt`  | Remove write permission from group   |

---
