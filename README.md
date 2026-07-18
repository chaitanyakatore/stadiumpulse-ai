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
*   **IP-Based Rate Limiting**: Custom sliding window rate limiting mapped to auth attempts (60/15m), AI generation requests (60/15m), and general telemetry polls (1000/15m) to prevent DDoS attacks and API key quota abuse.
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
npm start
```
Open [http://localhost:3000](http://localhost:3000) in your web browser.

---

## 📖 Detailed Step-by-Step User Manual

Here is the walkthrough script to test all the features of StadiumPulse AI like a production reviewer:

### 1. The Gateway Launcher (`/`)
When you load the app, you arrive at the central **Access Portal Launcher**. This simulates a secure portal gateway:
*   Click **Launch Dashboard** to open the operator dashboard.
*   Click **Launch Staff App** to open the mobile volunteer companion.
*   Click **Launch Concierge** to open the public spectator app.

---

### 2. Operations Control Center (`/operations`)
*   **Accessing the Dashboard**: Click "Launch Dashboard". You will be intercepted by the **Secure SSO Login**.
    *   *Option A*: Log in using `operator` / `password123`.
    *   *Option B*: Click **Register Now** at the bottom, fill out a new profile, submit, and log in with your new user credentials!
*   **Reviewing live crowd alerts**: Under **Live Venue Density Map**, you will see stadium gates and concourses color-coded:
    *   `Green` = Safe Flow (Nominal capacity).
    *   `Yellow` = Attention (Elevated congestion).
    *   `Red` = Critical (Risk of gridlock).
*   **Synthesizing Multi-Agency Playbooks**: Select a zone labeled `ELEVATED` or `CRITICAL` on the map blueprint:
    *   Click on the **Coordinated Playbook** tab in the briefing container at the bottom.
    *   Google Gemini will compile specific, structured safety instructions for four separate agencies (Stewards, Security, Medical, Transit) side-by-side.
*   **Compiling AI Announcer Scripts**: Select a surging zone, scroll to the Action Dispatch card on the bottom-right, and click **Compile AI Broadcast Script**:
    *   An announcer PA script in English will be synthesized.
    *   Mobile app push notifications translated into four languages (EN, ES, FR, PT) will be displayed.
*   **Executing Copilot Dispatches**: Look at the **Gemini AI Copilot Sidebar** on the right:
    *   It lists active safety suggestions, confidence scores, and predicted impacts.
    *   Click **Execute Command** on a suggestion. The platform automatically populates the target fields and transmits the order to field volunteers!

---

### 3. Field Staff Companion (`/volunteer`)
*   **Logging In**: Click "Launch Staff App" on the home gateway. Sign in using `volunteer` / `password123`.
*   **Receiving Dispatches**: When the Operations Control lead transmits an order, it instantly pops up on the volunteer's list of active task directives.
*   **Resolving Crowd bottlenecks**: Press **Acknowledge** on any dispatch item. The directive is cleared, the event log updates, and the stadium zone's risk level on the operations map immediately drops back to `Safe Flow`!
*   **Reporting Live Incidents**: Scroll down to the **Report Field Crowd Incident** form:
    *   Select a zone (e.g. `Gate 3`), write a description (e.g. `Ticketing outage causing a heavy queue backup`), select `Critical`, and click **Transmit Alert**.
    *   Switch to the `/operations` dashboard and see the timeline feed immediately flash the volunteer's live report!

---

### 4. Spectator Concierge Portal (`/fan`) — *Public Access*
*   **No Login Needed**: Click "Launch Concierge" on the gateway.
*   **Wayfinding Route Calculator**: Scroll to the **Wayfinding Assistant** card:
    *   Select your match day ticket section (e.g., `Section 114`) and your destination (e.g., `Nearest Exit Hub`).
    *   Click **Find Path**. The application draws a path line on the stadium blueprint, guiding you around the active crowd bottlenecks!
*   **Gemini Support Chat**: Ask Gemini natural language questions, e.g.:
    *   *"What objects are banned inside the stadium?"*
    *   *"Is there a shuttle bus delay at Gate 1?"*
    *   Gemini reads live stadium telemetry to give you welcoming, real-time answers.

---

### 5. Developer Scenario Simulation (`/dev`)
*   Go to **Access Scenario Simulation Room** at the bottom of the portal launcher.
*   Click **Inject Gate 1 Ticketing Outage** or **Inject Transit Hub Shuttle Delay**:
    *   The simulation alters the crowd levels, triggering active telemetry warnings, timeline audits, and AI suggestions across the dashboards!
