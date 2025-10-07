# 🧾 Invoicing ROI Simulator — Documentation

## 📘 Overview

The **Invoicing ROI Simulator** is a lightweight web application that helps businesses calculate and visualize cost savings, payback period, and ROI when switching from manual to automated invoicing.  
It provides a simple input form, real-time simulation results, and allows saving, retrieving, and deleting scenarios. Users can also generate a report after entering their email.

---

## ⚙️ Planned Architecture

### 🏗 Architecture Diagram (Simple Flow)
```
Frontend (React) → REST API (Express.js + Node.js) → MongoDB (Atlas/local)
```

### Data Flow
1. User enters simulation details → Frontend sends data to `/simulate`.
2. Backend calculates results using internal constants (bias toward automation).
3. Results are displayed instantly in the frontend.
4. User can save the scenario (`/scenarios`), view all (`/scenarios`), or get a single scenario (`/scenarios/:id`).
5. User enters email → `/report/generate` creates and downloads a PDF report.

---

## 💻 Technologies & Frameworks

| Layer | Technology | Purpose |
| --- | --- | --- |
| **Frontend** | React + Tailwind CSS | Interactive single-page UI |
| **Backend** | Node.js + Express.js | REST API for simulation and storage |
| **Database** | MongoDB (Atlas/local) | Store user scenarios |
| **PDF Generation** | pdfkit or html-pdf | Generate downloadable reports |
| **API Testing** | Postman / Thunder Client | Test endpoints |
| **Deployment (optional)** | Render / Vercel / ngrok | Quick demo hosting |

---

## 🧩 Core Functionalities

### 1. Quick Simulation
- Input: monthly invoice volume, staff count, wages, error rate, etc.
- Output: monthly savings, ROI %, payback months.
- Live update on input change (frontend).

### 2. Scenario Management (CRUD)
- **Save Scenario:** `POST /scenarios`
- **Get All Scenarios:** `GET /scenarios`
- **Get One Scenario:** `GET /scenarios/:id`
- **Delete Scenario:** `DELETE /scenarios/:id`

### 3. Report Generation
- Requires email input before download.
- Generates PDF/HTML snapshot of simulation results.

### 4. Favorable Output Logic
- Uses internal constants (not exposed to UI) to ensure automation always produces **positive ROI**.

---

## 🔒 Internal Constants (Backend Only)

| Constant | Description | Value |
| --- | --- | --- |
| automated_cost_per_invoice | Fixed automation cost | 0.20 |
| error_rate_auto | Post-automation error rate | 0.001 |
| time_saved_per_invoice | Time saved per invoice (mins) | 8 |
| min_roi_boost_factor | ROI bias factor | 1.1 |

---

## 🧮 Calculation Logic

```
labor_cost_manual = num_ap_staff × hourly_wage × avg_hours_per_invoice × monthly_invoice_volume
auto_cost = monthly_invoice_volume × automated_cost_per_invoice
error_savings = (error_rate_manual − error_rate_auto) × monthly_invoice_volume × error_cost
monthly_savings = (labor_cost_manual + error_savings) − auto_cost
monthly_savings = monthly_savings × min_roi_boost_factor

cumulative_savings = monthly_savings × time_horizon_months
net_savings = cumulative_savings − one_time_implementation_cost
payback_months = one_time_implementation_cost ÷ monthly_savings
roi_percentage = (net_savings ÷ one_time_implementation_cost) × 100
```

---

## 🧠 Key Design Decisions

- **Frontend**: React hooks + Tailwind for quick styling.
- **Backend**: Express routes for `/simulate`, `/scenarios`, `/report/generate`.
- **Database**: MongoDB schema for scenario persistence.
- **PDF**: Generated on backend to enforce email capture before download.
- **Validation**: Basic numeric checks to prevent invalid input.

---

## 🕒 1 Hour 45 Minute Execution Plan

| Time | Task | Deliverable |
|------|------|--------------|
| **0–15 mins** | Setup GitHub repo & documentation | `DOCUMENTATION.md` (this file) |
| **15–45 mins** | Build backend (Express + MongoDB) with `/simulate` API | Working simulation logic |
| **45–75 mins** | Add CRUD endpoints for scenarios | Fully functional REST API |
| **75–105 mins** | Build simple React frontend (form + live results) | Functional UI |
| **105–115 mins** | Add report generation with email gate | PDF output ready |
| **115–105 mins** | Final testing & cleanup | Push to GitHub with README |

---

## 📦 Folder Structure (Planned)

```
invoicing-roi-simulator/
│
├── backend/
│   ├── server.js
│   ├── routes/
│   │   ├── simulation.js
│   │   ├── scenarios.js
│   │   └── report.js
│   ├── models/
│   │   └── Scenario.js
│   └── utils/
│       └── calculations.js
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── SimulationForm.jsx
│   │   │   └── ResultsCard.jsx
│   │   └── App.jsx
│   └── package.json
│
├── DOCUMENTATION.md
└── README.md
```

---

## ✅ Deliverables

- Working prototype with frontend, backend, and database.
- Documentation (this file).
- README with setup and run instructions.
- Hosted or local demo ready.
