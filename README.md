# 🏥 MediCare Hospital — AI Navigation & Administrative Assistance Agent

An interactive hospital indoor navigation and smart administrative assistant system inspired by the **National Health Systems Resource Centre (NHSRC)** Indian Public Health Standards (IPHS) hospital layout architecture.

The project features a full **2D multi-floor blueprint floor plan**, an intelligent **BFS shortest-path route planner** with step-by-step walking directions, a real-time **search directory**, and an **AI Administrative Assistant Chatbot** for appointment booking, emergency protocols, doctors' visiting hours, and department navigation.

---

## 📋 Table of Contents
- [✨ Key Features](#-key-features)
- [🏗️ Architecture & Technology Stack](#️-architecture--technology-stack)
- [📁 Project Structure](#-project-structure)
- [⚙️ Prerequisites](#️-prerequisites)
- [🚀 Quick Start Guide](#-quick-start-guide)
- [🔧 Configuration (.env)](#-configuration-env)
- [🌐 REST API Reference](#-rest-api-reference)
- [🗺️ How to Use the Navigation Map](#️-how-to-use-the-navigation-map)
- [🤖 Interacting with the AI Assistant](#-interacting-with-the-ai-assistant)
- [🔍 Troubleshooting](#-troubleshooting)
- [📜 Disclaimer](#-disclaimer)

---

## ✨ Key Features

1. **Interactive Multi-Floor Blueprint Map**:
   - 4-Floor layout: **Ground Floor, 1st Floor, 2nd Floor, and 3rd Floor**.
   - Floor selector buttons with instant view switching.
   - Distinct visual color coding for **Emergency, Pharmacy, OPD, Inpatient Wards, ICUs, Diagnostics (Lab/X-Ray), Administration, and Vertical Transit (Lifts & Stairs)**.
   - Clickable rooms showing room number, department head/specialty, floor, and description.

2. **Graph-Based Shortest Path Navigation (BFS)**:
   - Select any starting point and destination in the hospital.
   - Calculates the shortest route navigating corridors, elevators, and stairs across multiple floors.
   - Visual path highlighting with floor-by-floor breakdown.
   - Turn-by-turn walking instructions with estimated distance (meters) and walking time (minutes/seconds).

3. **AI Administrative Assistant Chatbot**:
   - Natural language queries for rooms, doctors, departments, visiting hours, and admission steps.
   - Guides patients on required registration documents and OP/IP processes.
   - Instant emergency protocol trigger and pharmacy hours check.

4. **Hospital Directory & Live Search**:
   - Search departments, doctors, specialties, and wards in real-time.
   - Direct "Navigate Here" action triggers map routing to the chosen location.

5. **Quick Action Panels**:
   - 🚨 **Emergency**: Direct route from entrance, trauma triage instructions, emergency hotline.
   - 💊 **Pharmacy**: Operating hours, OTC/prescription pickup points, floor location.
   - 📋 **Appointments**: Required documents checklist and step-by-step registration flowchart.

---

## 🏗️ Architecture & Technology Stack

- **Backend**: Node.js & Express.js (REST API, graph route computation, query processing).
- **Frontend**: Vanilla HTML5, CSS3 (Modern Glassmorphism & Responsive Layout), and Vanilla JavaScript (SVG/Canvas Blueprint rendering & State Management).
- **Data Engine**: JSON-backed graph network defining topological hospital nodes and walkway edges.
- **Port**: Default `3000` (customizable via `.env`).

---

## 📁 Project Structure

```text
IRIS/
├── package.json              # Root project configuration & convenience scripts
├── README.md                 # Project guide & documentation
├── normal.html               # Legacy prototype layout
├── server/
│   ├── .env                  # Environment variables (PORT, HOST)
│   ├── package.json          # Backend server dependencies & start scripts
│   ├── server.js             # Express API server & BFS pathfinding engine
│   └── data/
│       └── hospital-data.json # Complete hospital rooms, graph nodes & connections
└── public/
    ├── index.html            # Main web application entry point
    ├── css/
    │   └── style.css         # Complete styling, animations, and responsive layout
    └── js/
        └── app.js            # Frontend logic, map rendering, UI state & API clients
```

---

## ⚙️ Prerequisites

Before running the application, make sure you have installed:
- [Node.js](https://nodejs.org/) (Version **16.x** or higher, Node **18+** / **20+** recommended).
- **npm** (comes packaged with Node.js).

Check your installed versions by opening a terminal:
```bash
node -v
npm -v
```

---

## 🚀 Quick Start Guide

### Method 1: Running from the Root Directory (Recommended)

1. Open a terminal in the project root folder (`IRIS/`):
   ```bash
   cd c:\Users\reshs\OneDrive\Desktop\IRIS
   ```

2. Install dependencies (if not already installed):
   ```bash
   npm run install:server
   ```

3. Start the server:
   ```bash
   npm start
   ```

4. Open your web browser and navigate to:
   ```text
   http://localhost:3000
   ```

---

### Method 2: Running directly from the `server/` Directory

1. Open your terminal and change into the `server/` folder:
   ```bash
   cd server
   ```

2. Install packages:
   ```bash
   npm install
   ```

3. Run the server:
   ```bash
   npm start
   ```
   *(Or for auto-reloading if you have `nodemon` installed: `npx nodemon server.js`)*

4. Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## 🔧 Configuration (.env)

The server configuration is located in [server/.env](file:///c:/Users/reshs/OneDrive/Desktop/IRIS/server/.env):

```env
PORT=3000
HOST=localhost
```

- To change the port, update `PORT=<your_port>` and restart the server.

---

## 🌐 REST API Reference

The backend provides comprehensive JSON endpoints consumed by the frontend or external clients:

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/api/floors` | List all 4 floors and their descriptions |
| `GET` | `/api/locations` | Get all clickable hospital locations, coordinates, and types |
| `GET` | `/api/departments` | Full list of medical departments, descriptions, and services |
| `GET` | `/api/doctors` | List of doctors, specialties, room numbers, and OPD timings |
| `GET` | `/api/wards` | Inpatient wards, room numbers, bed capacities, and types |
| `GET` | `/api/pharmacy` | Pharmacy operating hours, location, and services |
| `GET` | `/api/emergency` | Emergency room details, ambulance entry, and triage route |
| `GET` | `/api/appointments` | Required registration documents and appointment guidelines |
| `GET` | `/api/search?q=:query` | Global search across locations, doctors, departments & wards |
| `GET` | `/api/route?from=:id&to=:id` | BFS shortest route path with walking directions and metrics |
| `POST` | `/api/assistant` | Natural language query processing (`{ "message": "..." }`) |

#### Example Route Calculation Request:
```bash
curl "http://localhost:3000/api/route?from=main-entrance&to=icu"
```

---

## 🗺️ How to Use the Navigation Map

1. Navigate to the **Interactive Map** tab from the top navigation or sidebar.
2. **Floor Switching**: Click on **Ground Floor**, **1st Floor**, **2nd Floor**, or **3rd Floor** to inspect each level.
3. **Room Inspection**: Click on any room or department in the blueprint to view its:
   - Official room number.
   - Operating department.
   - Floor level.
   - Services offered.
4. **Finding a Route**:
   - In the **Navigation Panel**, pick a **Starting Point** (e.g. *Main Entrance* or *Reception*).
   - Pick a **Destination** (e.g. *Room 102 - Cardiology OPD* or *Room 201 - Operation Theatre*).
   - Click **"Find Route"**.
   - The map highlights the shortest walking path and displays the estimated walking time, total distance in meters, and step-by-step turns.

---

## 🤖 Interacting with the AI Assistant

Click on the **AI Assistant** tab or widget. You can ask queries like:
- *"Where is Cardiology?"*
- *"How do I reach Room 204?"*
- *"What documents do I need for appointment registration?"*
- *"Where is the pharmacy and what are its timings?"*
- *"Take me to Emergency"*
- *"When does Dr. Sharma visit?"*
- *"Which floor is the ICU on?"*

The assistant provides exact room numbers, floor levels, instructions, and offers a 1-click **"Navigate Here"** button on the map.

---

## 🔍 Troubleshooting

### 1. `Error: listen EADDRINUSE: address already in use :::3000`
This means another process (or a previous instance of the server) is already running on port 3000.

**To resolve on Windows:**
1. Open PowerShell and find the PID using port 3000:
   ```powershell
   netstat -ano | findstr :3000
   ```
2. Terminate the process (replace `<PID>` with the number in the rightmost column):
   ```powershell
   taskkill /PID <PID> /F
   ```
3. Alternatively, change `PORT=3001` in [server/.env](file:///c:/Users/reshs/OneDrive/Desktop/IRIS/server/.env) and start the server again.

### 2. `Cannot find module 'express'`
Run npm install in the server directory:
```bash
cd server
npm install
```

---

## 📜 Disclaimer

*This application is a demonstration and prototype system built for the project **"AI Hospital Navigation & Administrative Assistance Agent"**. The floor layout and organizational structure are inspired by the standard guidelines of the National Health Systems Resource Centre (NHSRC) Indian Public Health Standards (IPHS 2022), but it is a fictitious demo hospital and not an official NHSRC hospital facility.*
