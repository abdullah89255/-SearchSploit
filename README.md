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

Got it — you want **lots** of real-world SearchSploit examples so you can see how it works in different pentesting scenarios.
I’ll give you **15+ hands-on examples** from basic searches to advanced integrations.

---

## **1. Simple Keyword Search**

```bash
searchsploit apache
```

Finds all exploits containing “apache” in their title or description.

---

## **2. Multiple Keywords**

```bash
searchsploit apache 2.4
```

Search for exploits related to Apache version 2.4.

---

## **3. Exact Match Search**

```bash
searchsploit -e "Apache 2.4.49"
```

Finds only entries with exactly `Apache 2.4.49`.

---

## **4. Case-Sensitive Search**

```bash
searchsploit -c Windows
```

Matches only “Windows” with a capital W.

---

## **5. Exclude Keywords**

```bash
searchsploit apache -x java
```

Find Apache exploits but exclude anything related to Java.

---

## **6. Search and Copy Exploit**

```bash
searchsploit openssl 1.1.1 -m
```

Search for exploits related to OpenSSL 1.1.1 and **mirror** (copy) them to the current directory.

---

## **7. View Exploit Code without Copying**

```bash
searchsploit -x exploits/linux/remote/12345.py
```

Opens the exploit so you can read its code directly.

---

## **8. Get Local Path to Exploit**

```bash
searchsploit -p exploits/multiple/remote/12345.txt
```

Prints the **absolute path** to the exploit file in your system.

---

## **9. Search and Open Web Link**

```bash
searchsploit -w apache 2.4.49
```

Gives a clickable link to the Exploit-DB website for that exploit.

---

## **10. Use with Nmap Scan**

```bash
nmap -sV target.com -oX scan.xml
searchsploit --nmap scan.xml
```

Parses service versions from an **Nmap XML** file and looks up matching exploits automatically.

---

## **11. Search by EDB-ID**

If you know the **Exploit-DB ID**:

```bash
searchsploit 50383
```

This finds the exact exploit for Apache 2.4.49 Path Traversal.

---

## **12. Search in Titles Only**

```bash
searchsploit -t wordpress
```

Finds only exploits with “wordpress” in the **title**.

---

## **13. Update Database**

```bash
searchsploit -u
```

Fetches the latest exploits from Exploit-DB.

---

## **14. Save Results to a File**

```bash
searchsploit mysql > mysql_exploits.txt
```

Saves all MySQL exploit results to a text file.

---

## **15. Combine Search and Web Output**

```bash
searchsploit -w -t "Drupal 8.8"
```

Shows only titles containing “Drupal 8.8” and gives their web links.

---

## **16. Find Exploits for Specific OS**

```bash
searchsploit windows 10 local
```

Search for local privilege escalation exploits for Windows 10.

---

## **17. Search by Vulnerability Type**

```bash
searchsploit "SQL injection"
```

Find all exploits related to SQLi vulnerabilities.

---

## **18. Find WordPress Plugin Exploits**

```bash
searchsploit "WordPress plugin" -t
```

Lists only plugin-related vulnerabilities in WordPress.

---


