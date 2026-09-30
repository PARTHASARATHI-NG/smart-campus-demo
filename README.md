Smart Campus Entrance Monitoring & Decision-Support System

This repository contains the interactive frontend prototype for a multi-source fusion hub designed to solve the "last-mile" campus bottleneck caused by railway level-crossing closures, specifically modeled for Amrita Vishwa Vidyapeetham, Ettimadai (ETMD).

🚀 Overview

The Smart Campus Entrance Monitor is a web-based dashboard that helps students, faculty, and campus drivers make informed routing decisions before arriving at the campus gates. It achieves this by fusing two data streams:

Physical Ground Truth: Live gate status (Open/Closed) derived from external cameras.

Predictive Telemetry: Live train arrival and schedule data from nearby railway stations.

🏗️ Production vs. Demonstration Mode

This current frontend index.html file serves as a Demonstration Prototype.

Production Architecture: In the final deployment, a dedicated backend server (e.g., Node.js or Python) will securely hold private API keys to fetch live Indian Railways running-status data. Simultaneously, a local workstation will ingest live RTSP video feeds from the gates and run a YOLO-based Computer Vision (CV) model to automatically detect if the gate boom barriers are open or closed. The backend will then push these real-time states to this web interface.

Current Demo Mode: Because browsers block frontend requests to unauthenticated APIs (CORS restrictions), this prototype uses a robust Synthetic Data Generator. It dynamically creates realistic train schedules (e.g., Palakkad MEMU, West Coast Express) synced directly to the user's system clock. Furthermore, the automated YOLO CV inputs are simulated using manual "Set Open / Set Closed" toggle buttons on the dashboard for demonstration purposes.

✨ Key Features

🧠 Smart Recommendation System (Decision Engine)

The core of this system is a hybrid rule-based decision engine that analyzes both gate statuses and train ETAs to provide dynamic, intelligent routing advice:

Clear Route: If both gates are open and no trains are nearby, it recommends the primary Railway Gate.

Pre-emptive Rerouting: If the primary gate is open but a train is $\le$ 15 minutes away, the system warns the user that the gate will likely close soon and suggests using the Alternate Gate.

Active Rerouting: If the primary gate is closed but the Alternate Gate is open, it advises immediate rerouting.

Complete Blockage: If both gates are closed, it issues a critical alert and calculates an expected reopening time based on a built-in 11-minute timer (triggered upon closure).

📊 Real-Time Status Dashboard

Visual badges and dynamic UI color coding (Green/Amber/Red) indicating campus accessibility.

Countdown timer for expected railway gate reopening.

🔮 Future Implementations

We plan to expand the system's capabilities with the following features:

Real API Backend: Replacing the synthetic data with a live, authenticated backend relaying real railway telemetry.

Live Camera Feeds: Replacing the static placeholders with actual low-latency video streams from the edge cameras.

Live Traffic Density & Queue Estimation: Upgrading the YOLO model to not only detect the gate status but also count the number of vehicles waiting. This will allow the dashboard to display live traffic volume at each gate, helping users choose the entrance with the shortest wait time even when both gates are open.

💻 How to Run the Demo

Since this is a self-contained prototype, no complex build steps or installations are required.

Clone or download this repository.

Open the index.html file in any modern web browser (Chrome, Firefox, Safari, Edge).

Alternatively, view the live demo via GitHub Pages: https://parthasarathi-ng.github.io/smart-campus-demo/
