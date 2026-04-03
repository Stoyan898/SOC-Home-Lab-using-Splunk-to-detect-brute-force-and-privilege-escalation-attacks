# 🎣 Phishing Detection Lab (Splunk)

## 📌 Overview

This lab simulates phishing attacks against an Apache web server and demonstrates detection using Splunk.

Attack pattern:

* Multiple POST requests to `/login.php`
* Failed responses (HTTP 500)
* Repeated attempts from same IP

---

## ⚙️ Log Source

```bash
/var/log/apache2/access.log
```

Forwarded using Splunk Universal Forwarder.

---

## 🔍 Detection Queries

### Find phishing attempts

```spl
index=main "POST /login.php"
```

### Extract attacker IP

```spl
index=main "POST /login.php"
| rex "^(?<ip>\d+\.\d+\.\d+\.\d+)"
| stats count by ip
```

### Timeline

```spl
index=main "POST /login.php"
| timechart count
```

---

## 📊 Dashboard

### Overview

![dashboard](screenshots/01_dashboard_overview.png)

### Login attempts

![events](screenshots/02_search_login_events.png)

### Top attacker

![ip](screenshots/03_ip_stats.png)

### Activity over time

![time](screenshots/04_timechart.png)

### Raw logs

![logs](screenshots/05_raw_logs.png)

---

## ⚠️ Challenges & Fixes

### ❌ Logs not appearing

* Wrong path used
* Fixed: `/var/log/apache2/access.log`

---

### ❌ Permission denied

```bash
sudo chmod 644 /var/log/apache2/access.log
```

---

### ❌ No events in Splunk

* Issue with fishbucket
* Fixed by reset

```bash
sudo /opt/splunkforwarder/bin/splunk stop
sudo rm -rf /opt/splunkforwarder/var/lib/splunk/fishbucket/*
sudo /opt/splunkforwarder/bin/splunk start
```

---

### ❌ Data visible but not searchable

* Wrong query or index confusion
* Fixed using:

```spl
index=* access.log
```

---

## 🧠 Key Learnings

* Log ingestion troubleshooting
* SPL query writing
* Web attack detection
* Dashboard building

---

## 🚀 Conclusion

This lab demonstrates how phishing attacks can be detected using web logs and SIEM tools like Splunk.
