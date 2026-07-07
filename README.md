# Kagoj

Kagoj is a print vending machine system: end users pay to print documents from
their phone at a kiosk, which prints the job on a connected printer.

## Folder structure

- **backend/** — Node.js + Express API backed by PostgreSQL. Handles print
  jobs, payments, and machine state. See `backend/server.js`.
- **machine-agent/** — Python agent that runs on the mini PC attached to each
  vending machine. Polls the backend and drives the physical printer.
- **web-app/** — React + Vite + Tailwind CSS mobile-only PWA. This is what end
  users open on their phone to upload a file and pay to print.
- **admin-dashboard/** — Next.js app, password protected. Internal panel for
  monitoring machines, jobs, and payments.
- **qr-display/** — Static HTML/JS page shown on the kiosk screen itself. It
  displays a rotating QR code that end users scan to open `web-app`.
- **docs/** — Project documentation, including the database schema
  (`docs/schema.md`).

## Running locally

### backend

```bash
cd backend
cp .env.example .env   # then edit DATABASE_URL for your local Postgres
npm install
npm run dev            # http://localhost:4000, GET /health to verify
```

### web-app

```bash
cd web-app
npm install
npm run dev             # prints a local URL, default http://localhost:5173
```

### admin-dashboard

```bash
cd admin-dashboard
npm install
npm run dev              # http://localhost:3000
```

### machine-agent

```bash
cd machine-agent
python -m venv venv
venv\Scripts\activate     # on Windows; use `source venv/bin/activate` on macOS/Linux
pip install -r requirements.txt
cp .env.example .env       # then edit BACKEND_URL / MACHINE_ID
python main.py
```

### qr-display

Open `qr-display/index.html` directly in a browser, or serve the folder with
any static file server (e.g. `npx serve qr-display`).
