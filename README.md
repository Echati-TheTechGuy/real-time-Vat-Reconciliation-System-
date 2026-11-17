[README.md](https://github.com/user-attachments/files/34968911/README.md)

# VATSync — Real-Time VAT Reconciliation System


---

## What is VATSync?

VATSync is a dual-portal web application that enables SMEs in Zimbabwe to reconcile their VAT records in real-time against ZIMRA's TaRMS (Tax Administration and Revenue Management System). It was developed as a final-year capstone project demonstrating real-world integration between taxpayer-side VAT management and tax authority administration.

**Two portals:**
- **SME Portal** (port 3000) — businesses view their VAT position, transaction history, compliance status, and download VAT 7 CSV exports
- **ZIMRA TaRMS Panel** (port 3001) — ZIMRA officers post transactions, manage exchange rates, and monitor all registered SMEs

---

## System Requirements

- Windows 10 or 11
- Python 3.10 or later — https://www.python.org/downloads/
- Node.js 18 or later — https://nodejs.org/
- Internet connection (first-time setup only, to install packages)

---

## First-Time Setup (run once only)

Open Command Prompt as Administrator and run these commands in order:

### Step 1 — Set up the Python backend

```
cd C:\path\to\VATSync\backend
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
```

### Step 2 — Install SME frontend dependencies

```
cd C:\path\to\VATSync\sme-frontend
npm install
```

### Step 3 — Install ZIMRA frontend dependencies

```
cd C:\path\to\VATSync\zimra-frontend
npm install
```

After setup is done once, you never need to run these commands again.

---

## Running the System (every time)

Double-click **START_VATSYNC.bat**

This opens three windows and two browser tabs automatically:
- SME Portal → http://localhost:3000
- ZIMRA Panel → http://localhost:3001
- Backend API → http://localhost:5000

To stop: close the three black Command Prompt windows.

---

## Demo Login Credentials

**SME Portal (http://localhost:3000)**
| TIN | Business | Password |
|-----|----------|----------|
| 2020202020 | Wenyasha Investiments | vat000 |
| 2003030303 | Demo Business 1 | any password |
| 2019012345 | Demo Business 2 | any password |

**ZIMRA TaRMS Panel (http://localhost:3001)**
| Username | Password |
|----------|----------|
| zimra_admin | zimra2026 |

---

## Project Structure

```
VATSync/
├── START_VATSYNC.bat          ← Double-click to run everything
├── SETUP_FIRST_TIME.bat       ← Run once on a new machine
├── README.md                  ← This file
│
├── backend/
│   ├── app.py                 ← Flask REST API (port 5000)
│   ├── core.py                ← Business logic, VAT calculations
│   ├── db.py                  ← SQLite database helper
│   ├── vatreconcile.db        ← SQLite database (all data lives here)
│   ├── requirements.txt       ← Python dependencies
│   └── demo_auth.py           ← Authentication module demo/test script
│
├── sme-frontend/
│   ├── src/App.jsx            ← SME portal (React.js)
│   ├── index.html
│   ├── package.json
│   └── vite.config.js
│
└── zimra-frontend/
    ├── src/App.jsx            ← ZIMRA admin panel (React.js)
    ├── index.html
    ├── package.json
    └── vite.config.js
```

---

## Technical Stack

| Layer | Technology |
|-------|-----------|
| Backend | Python 3, Flask, Flask-CORS |
| Database | SQLite (vatreconcile.db) |
| SME Frontend | React.js 18, Vite |
| ZIMRA Frontend | React.js 18, Vite |
| Currency | Dual USD/ZiG with RBZ exchange rates |
| Auth | Bearer token sessions (in-memory) |

---

## Important Notes

1. **After a power cut or restart** — the backend loses its in-memory sessions. Simply log out and log back in. Your data in the database is always safe.

2. **The database file** `backend/vatreconcile.db` contains all your registered businesses and posted transactions. Back this file up regularly.

3. **Ports used:** 3000 (SME), 3001 (ZIMRA), 5000 (Backend). Make sure no other software uses these ports.

---

*VATSync — Developed by Chatikobo Elison, Midlands State University, 2026*
