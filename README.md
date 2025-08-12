# -SearchSploit

Alright — let’s go deep into **SearchSploit** so you get the *full* picture, from installation to advanced tricks.
Think of it as your **offline Google for Exploit-DB**.

---

## **1. What is SearchSploit?**

SearchSploit is a command-line utility from **Exploit Database** that lets you search, copy, and inspect public exploits **offline**.
It comes pre-installed in **Kali Linux**, but you can install it on other systems too.

It’s useful for:

* Quickly finding exploits for a specific software version.
* Reviewing exploit code without visiting exploit-db.com.
* Copying exploit code to your own directories for testing in labs.

---

## **2. Installation**

On **Kali Linux**, it’s usually pre-installed.
Check:

```bash
searchsploit -h
```

If missing:

```bash
sudo apt update && sudo apt install exploitdb
```

On **other Linux**:

```bash
git clone https://gitlab.com/exploit-database/exploitdb.git
cd exploitdb
sudo cp -n searchsploit /usr/local/bin/
```

---

## **3. Updating the Database**

Since new exploits are added often:

```bash
searchsploit -u
```

This pulls the latest Exploit-DB archive.

---

## **4. Basic Usage**

**Syntax:**

```bash
searchsploit [keyword(s)]
```

**Examples:**

```bash
searchsploit apache
searchsploit windows 10
searchsploit openssl 1.1.1
```

**Output:**
You’ll see:

```
--------------------------------------------------------------------
 Exploit Title                              |  Path
--------------------------------------------------------------------
Apache HTTP Server 2.4.49 Path Traversal    |  exploits/linux/http/50383.py
```

---

## **5. Filtering & Matching Options**

* **Exact match**:

```bash
searchsploit -e "Apache 2.4.49"
```

* **Case-insensitive search** (default is already case-insensitive):

```bash
searchsploit -i apache
```

* **Exclude terms**:

```bash
searchsploit apache -x java
```

* **Show only exploit titles (no paths)**:

```bash
searchsploit -t apache
```

---

## **6. Copying Exploits for Editing**

SearchSploit doesn’t run exploits directly — you copy them first:

```bash
searchsploit -m exploits/linux/http/50383.py
```

This will copy the file to your current directory.

You can also combine:

```bash
searchsploit apache 2.4.49 -m
```

This copies **all matching exploits** to your working directory.

---

## **7. Viewing Exploit Details**

Instead of opening in an editor:

```bash
searchsploit -p exploits/linux/http/50383.py
```

This prints the file path in your system.

Or view the exploit without copying:

```bash
searchsploit -x exploits/linux/http/50383.py
```

---

## **8. Searching Exploit-DB Online**

SearchSploit can open the browser directly:

```bash
searchsploit -w apache
```

This will give a direct URL to the exploit page.

---

## **9. Integration with Nmap**

If you’ve scanned a target with **Nmap**, you can pipe results into SearchSploit:

```bash
nmap -sV target.com -oX scan.xml
searchsploit --nmap scan.xml
```

This will parse service versions from your Nmap XML and find matching exploits.

---

## **10. Practical Bug Bounty & Pentest Workflow**

**Example**:
You find a target running **Apache 2.4.49** during recon.

1. **Search for exploit**:

```bash
searchsploit "Apache 2.4.49"
```

2. **Copy exploit locally**:

```bash
searchsploit -m exploits/linux/http/50383.py
```

3. **Read exploit for context** (don’t run blindly!):

```bash
cat 50383.py
```

4. **Modify for your target’s host/port**.
5. **Test in lab first** before hitting production.

---

## **11. Common Options Cheat Sheet**

| Option            | Description                        |
| ----------------- | ---------------------------------- |
| `-u`              | Update database                    |
| `-m`              | Mirror (copy) exploit locally      |
| `-p`              | Print full path of exploit         |
| `-x`              | Examine exploit source code        |
| `-w`              | Show Exploit-DB web link           |
| `--nmap file.xml` | Search exploits based on Nmap scan |
| `-e`              | Exact match search                 |
| `-t`              | Titles only                        |

---

If you want, I can make you a **SearchSploit Mind Map** showing all commands, options, and workflow visually so you can keep it open during pentesting sessions. That’ll make it easier to remember.

Do you want me to make that? It’ll look like a **pentester’s quick-reference chart**.
