# 🛡️ Uptime & Security Watchdog

An autonomous, 24/7 website monitoring system built with n8n, Docker, Telegram, and Google Sheets. Acts as a "Site Guardian" for small businesses — detecting downtime and slow response times instantly, without any human intervention.

---

## 🚨 The Problem

Small business websites go down or get brute-forced, and the owners have no idea until it's too late — losing customers, revenue, and trust.

## ✅ The Solution

An autonomous monitor that pings a target website every 15 minutes, detects issues in real time, alerts the owner instantly on Telegram, and logs every incident to Google Sheets for monthly uptime reports.

---

## ⚙️ How It Works

```
Schedule Trigger (every 15 min)
        ↓
HTTP Request → pings https://github.com
        ↓
Code Node → checks status code + response time
        ↓
IF Node → alertNeeded: true or false
        ↓
   true ──→ Telegram Alert sent to owner
        ↓
Google Sheets → logs every check regardless
```

### Workflow Logic

| Condition | Action |
|---|---|
| Status code ≠ 200 | Trigger alert |
| Response time > 3000ms | Trigger alert |
| Everything normal | Log only, no alert |

---

## 📊 What Gets Logged (Google Sheets)

Every 15-minute check is recorded with:

| URL | Status Code | Response Time | Timestamp | Alert Sent |
|---|---|---|---|---|
| https://github.com | 200 | 1245ms | 2026-06-07T05:00:00Z | No |
| https://github.com | 0 | 1835ms | 2026-06-07T05:15:00Z | Yes |

---

## 📱 Telegram Alert Example

```
🚨 ALERT: github.com is down or slow.
Status: 0
Response time: 1835ms
Time: 2026-06-07T05:15:24.010Z
```

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| **n8n** | Visual workflow automation engine |
| **Docker** | Runs n8n in an isolated container |
| **Telegram Bot API** | Real-time alert delivery |
| **Google Sheets** | Incident logging & monthly reports |
| **HTTP Request Node** | Pings the target website |

---

## 🚀 Setup Guide

### Prerequisites
- Docker Desktop installed
- n8n account (cloud or self-hosted)
- Telegram Bot Token (from @BotFather)
- Google account

### Step 1 — Run n8n via Docker
```bash
docker run -it --rm -p 5678:5678 -v n8n_data:/home/node/.n8n n8nio/n8n
```
Open `localhost:5678` in your browser.

### Step 2 — Set up credentials in n8n
- **Telegram:** Settings → Credentials → New → Telegram → paste your Bot Token
- **Google Sheets:** Settings → Credentials → New → Google Sheets → Sign in with Google

### Step 3 — Import the workflow
- In n8n, click the menu → Import from file
- Upload `watchdog_workflow.json` from this repo

### Step 4 — Configure
- Update the HTTP Request node URL to your target website
- Update the Telegram Chat ID to your own
- Update the Google Sheets document ID

### Step 5 — Activate
Toggle the workflow to **Active** — it will now run every 15 minutes automatically.

---

## 📈 Why This Matters

This project demonstrates real-world **DevOps and Site Reliability Engineering (SRE)** skills:

- **Proactive monitoring** — catches issues before customers do
- **Automated alerting** — zero manual intervention required
- **Incident logging** — full audit trail for monthly reporting
- **Scalable design** — swap the URL to monitor any website in seconds

These are critical skills used daily at companies like Cisco, Oracle, and Infosys.

---

## 🔄 Swapping the Monitored Website

To monitor any other website, just change one field in the HTTP Request node:
```
https://github.com  →  https://yourclientwebsite.com
```
That's it. The entire system adapts automatically.

---

## 👤 Author

**Arjun Singh Bhati**  
GitHub: [@cartibhati](https://github.com/cartibhati)

---

## 📄 License

MIT License — feel free to use and modify.
