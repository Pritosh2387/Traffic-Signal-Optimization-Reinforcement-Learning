# 🚦 Climate-Aware Traffic Signal Optimization (Reinforcement Learning)

A Reinforcement Learning–based intelligent traffic signal control system that reduces congestion and CO₂ emissions using **Q-Learning**.

🔗 **Live API Deployment:**
https://carbonstop-ai.onrender.com

---

# 🌍 Project Overview

This project simulates a traffic intersection and trains a **Q-Learning agent** to optimize traffic light decisions.

The AI system learns to:

* 🚗 Reduce vehicle waiting time
* 🌱 Lower CO₂ emissions
* ⚖️ Balance traffic flow
* 🚑 Handle ambulance priority
* ⛔ Prevent lane starvation

The trained model is deployed using **FastAPI** and hosted on **Render**.

---

# 🔗 Live API

Deployed backend:

```text
https://carbonstop-ai.onrender.com
```

Try these endpoints:

## Health Check

```text
GET https://carbonstop-ai.onrender.com/health
```

Returns:

```json
{
  "status": "ok",
  "q_table_states": <number>
}
```

---

## Model Information

```text
GET https://carbonstop-ai.onrender.com/model-info
```

Returns:

* Model version
* Hyperparameters
* Available actions
* Features enabled

---

## Predict Traffic Action

```text
POST https://carbonstop-ai.onrender.com/predict
```

Example request:

```json
{
  "queue_NS": 5,
  "queue_EW": 10,
  "red_NS": 10,
  "red_EW": 20,
  "phase": 0,
  "hour": 14
}
```

Returns:

```json
{
  "action": "switch_phase",
  "carbon_intensity": 1.0,
  "explanation": "Switch the active green phase."
}
```

---

## Run Traffic Simulation

```text
POST https://carbonstop-ai.onrender.com/simulate
```

Simulates multiple steps and returns:

* Traffic queues
* CO₂ emissions
* Rewards
* Peak emission step

---

# 🧠 Reinforcement Learning Model

This project uses **Tabular Q-Learning** to train an intelligent traffic control agent.

---

## State Space

Each state contains:

(q_NS_bin, q_EW_bin, r_NS_bin, r_EW_bin, phase, carbon_bin)

Where:

* Queue sizes (NS/EW)
* Red signal duration
* Current green phase
* Carbon emission level

Queue bins:

0–4 → Low
5–9 → Medium
10–14 → High
15–19 → Very High
20+ → Extreme

---

## Action Space

The agent selects:

* `keep_green` → Maintain signal
* `switch_phase` → Change direction
* `extend_green` → Increase green duration

---

## Reward Strategy

Rewards encourage:

✅ Lower waiting time
✅ Balanced traffic
✅ Reduced emissions
✅ Correct signal decisions

Penalties occur for:

❌ Long red signals
❌ Traffic imbalance
❌ High emissions

---

# 📂 Project Structure

```bash
RL/
│
├── environment.py     # Traffic simulation logic
├── q_learning.py      # Q-learning training system
├── main.py            # FastAPI deployment API
├── q_table.json       # Trained model data
│
└── README.md
```

---

# ⚙️ Environment Simulation

The simulation includes:

* Vehicle arrival generation
* Queue management
* Signal phase control
* Carbon emission estimation
* Peak emission tracking

Carbon intensity changes based on time:

* 🌞 Day → Lower emissions
* 🌙 Night → Higher emissions

---

# 🚀 How to Run Locally

## Install dependencies

```bash
pip install fastapi uvicorn
```

---

## Train Model

```bash
python q_learning.py
```

Generates:

```text
q_table.json
```

---

## Run API

```bash
uvicorn main:app --reload
```

Server runs at:

```text
http://127.0.0.1:8000
```

---

# 🌱 Key Features

✅ Climate-aware traffic optimization
✅ Reinforcement Learning (Q-Learning)
✅ FastAPI deployment
✅ Render cloud hosting
✅ Emergency vehicle support
✅ CO₂ emission tracking
✅ Real-time prediction API

---

# 📊 Model Highlights

* Algorithm: Q-Learning
* Episodes: 10,000
* Learning Rate (α): 0.1
* Discount Factor (γ): 0.9
* Epsilon Decay Strategy
* Trained Q-table stored in JSON

---

# 🔮 Future Improvements

Possible extensions:

* Deep Q-Network (DQN)
* Multi-intersection coordination
* Real-time IoT traffic sensors
* Smart city integration
* Edge-based deployment

---
