# RetainAI – Intelligent Revenue Defense Engine

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![FastAPI](https://img.shields.io/badge/FastAPI-0.95%2B-green)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-blue)
![Stripe](https://img.shields.io/badge/Stripe-Payments-635bff)
![License](https://img.shields.io/badge/License-MIT-grey)

**RetainAI** is a drop-in retention infrastructure that helps SaaS companies recover revenue lost to voluntary churn. It intercepts cancellation requests and serves dynamic, personalized offers (pauses, discounts) based on customer value, reducing churn by up to 15%.

> **🔴 Live Demo:** [https://churnkey-demo.onrender.com](https://churnkey-demo.onrender.com)
>
> **👤 Test Credentials:**
> * **Email:** `admin@retainai.com`
> * **Password:** `password123`

---

## ⚡️ Key Technical Highlights

* **Multi-Tenant Architecture:** Engineered a scalable backend using **FastAPI** and **PostgreSQL** that isolates data for concurrent client organizations, ensuring strict data privacy and security.
* **Low-Latency Decision Engine:** Implemented a logic engine that processes user signals and serves retention offers in **sub-50ms**, ensuring no friction during the critical offboarding flow.
* **Framework-Agnostic SDK:** Built a lightweight (<5kb) Vanilla JS widget that injects complex UI components into third-party React/Vue/Angular billing flows via CORS without degrading host site performance.
* **Revenue Verification:** Integrated **Stripe Webhooks** to verify "save" events in real-time, enabling a performance-based billing model where fees are only charged on recovered revenue.

---

## 🛠 Tech Stack

| Component | Technology | Description |
| :--- | :--- | :--- |
| **Backend** | Python (FastAPI) | High-performance async API for logic processing. |
| **Database** | PostgreSQL (Neon) | Relational data storage for tenants, users, and offers. |
| **Frontend SDK** | Vanilla JavaScript | Lightweight, zero-dependency widget for client integration. |
| **Payments** | Stripe API | Subscription management and webhook event handling. |
| **Infrastructure** | Docker / Render | Containerized deployment with auto-scaling capabilities. |

---

## 🏗 Architecture

The system consists of two distinct parts:
1.  ** The Dashboard (SaaS):** Where founders configure their retention logic, offers, and view analytics.
2.  **The SDK (Widget):** A JavaScript snippet embedded in the client's app that communicates with the RetainAI API to render the cancellation flow overlay.

```mermaid
graph LR
    A[Client User] -->|Clicks Cancel| B(RetainAI JS SDK)
    B -->|GET /offer| C{FastAPI Logic Engine}
    C -->|Check Value| D[(PostgreSQL)]
    C -->|Return Offer| B
    B -->|Accept Offer| E[Stripe API]
    E -->|Webhook| C