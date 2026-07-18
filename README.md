# StadiumPulse AI — FIFA World Cup 2026 Operations Platform

StadiumPulse AI is a premium, enterprise-grade AI Operations Platform built on Material Design 3 principles to optimize stadium safety, field coordination, and spectator wayfinding during the FIFA World Cup 2026. 

It is designed to solve the root challenge of multi-agency incident coordination, replacing manual checklists and siloed operations with a unified Google Gemini-powered co-pilot.

👉 **Live Application Deployed on Render**: [https://stadiumpulse-ai-j3ji.onrender.com](https://stadiumpulse-ai-j3ji.onrender.com)

---

## 🚀 Key Features

*   **Coordinated Multi-Agency Playbooks**: Powered by Google Gemini, the platform dynamically generates real-time, task-based directives for four crucial stadium agencies (FIFA Stewards, Security Command, Medical, and Transit) based on active crowd density alerts.
*   **Decoupled Multi-Portal Gateways**: Clean separation of workspaces into dedicated applications to ensure security, mobile performance, and spectator safety:
    *   **Operations Control Dashboard**: Heatmap density maps, telemetry dials, chronological timelines, and action dispatch controls.
    *   **Staff Companion Portal**: Mobile-friendly incident reports and active dispatches checklist with instant acknowledgment feedback loops.
    *   **Spectator Wayfinding Concierge**: Multilingual support chat and low-congestion pathfinding calculators.
*   **Enterprise Security & SSO**: Custom session management using JSON Web Tokens (JWT) stored in secure `HttpOnly` cookies. Passwords are cryptographically encrypted using PBKDF2 with unique salts. Includes full user registration and password recovery security flows.
*   **IP-Based Rate Limiting**: Custom sliding window rate limiting mapped to auth attempts (5/15m), AI generation requests (15/15m), and general telemetry polls (1000/15m) to prevent DDoS attacks and API key quota abuse.
*   **Dual-Mode Storage Engine**: Repository pattern connecting to a live PostgreSQL pool on Render in production while falling back to a local encrypted file DB for development.

---

## 🛠️ Technology Stack

*   **Backend**: Node.js, Express.js
*   **Database**: PostgreSQL (Production/Render), Local JSON Failover
*   **AI Integration**: Google GenAI SDK (`gemini-2.5-flash`)
*   **Styling**: Material Design 3, Vanilla CSS
*   **Security**: JSON Web Tokens (JWT), Cookie-Parser, Cryptographic PBKDF2 Password Hashing, Custom IP Rate Limiters

---

## 💻 Local Quick Start

To clone and run the application locally:

### 1. Prerequisites
Ensure you have Node.js (version 18+) installed.

### 2. Installation
```bash
git clone https://github.com/chaitanyakatore/stadiumpulse-ai.git
cd stadiumpulse-ai
npm install
```

### 3. Environment Setup
Create a `.env` file at the root directory and add your credentials:
```env
# Google Gemini API Key
GEMINI_API_KEY=your_gemini_api_key_here

# PostgreSQL connection (Optional, falls back to local DB if empty)
DATABASE_URL=postgres://username:password@host:port/database
```

### 4. Running the Diagnostics Test
Run the automated testing suite to verify database migrations, cryptographic password encryption, and reset flows:
```bash
node scratch/db_test.js
```

### 5. Start the Server
```bash
n start
```
Open [http://localhost:3000](http://localhost:3000) in your web browser.
