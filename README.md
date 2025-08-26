# Human-vs-Bot
Detecting unusual user behavior in clickstream data through feature engineering and anomaly detection (Isolation Forest, entropy, session stats).

# 🤖 Humans vs. Bots: Feature Engineering for Web Behavior

This project is part of my **self-training in data science** and focuses on building a **feature engineering pipeline** to detect **unusual user behavior** (potential bots) in ad click data.

The dataset simulates **Google Ad Click sessions** in JSONL format, where each record contains:
- **User identifiers** (`tcid`, `tbid`, `session_id`)  
- **Device and environment info** (screen, viewport, user agent)  
- **Event sequences** (scrolls, touches, clicks, mouse moves, resizes, errors, etc.)

---

## 🎯 Project Goal
The main goal was **not** to build a predictive classifier, but to:
1. Explore and clean raw session & event data.  
2. Engineer meaningful features that capture **human-like vs. bot-like patterns**.  
3. Apply anomaly detection to identify suspicious sessions.  
4. Document the process in a **clear, interview-ready Jupyter Notebook**.

---

## 🛠️ Project Steps

### 1. Data Preparation
- Loaded **JSONL** data into Pandas DataFrames.  
- Flattened session-level and event-level structures.  
- Cleaned sparse fields and prepared features.

### 2. Exploratory Data Analysis (EDA)
- **Device distribution** (mobile, desktop, tablet, unknown).  
- **Screen vs. viewport ratios** to catch automation artifacts.  
- **Tabs per user** to detect scripted browsing.  
- **Event type distributions** (scrolls, touches, clicks, errors).  
- **Session lengths & inter-event gaps** to reveal unusual timing.  

### 3. Feature Engineering
Built **32 tab-level features** across 6 groups:
- **Activity & Timing:** event counts, session lengths, gaps.  
- **Event Diversity:** entropy of event types, dominant ratios.  
- **Scroll Behavior:** normalized depth, velocity stats.  
- **Spatial Interactions:** mouse/touch spreads, click spreads.  
- **Rare Event Ratios:** resize, error, visibility change, input rates.  
- **Device & Environment:** screen/viewport info, tab counts.

### 4. Modeling (Anomaly Detection)
- Applied **Isolation Forest** as the primary anomaly detector.  
- Flagged ~**2% of sessions** as anomalies.  
- Validated results with feature distributions:
  - Anomalies had **lower entropy** (repetitive actions).  
  - Some anomalies showed **20k+ events** per session.  

---

## 📊 Results
- Isolation Forest successfully identified **bot-like sessions** with:
  - Extremely high activity volumes.  
  - Very repetitive, low-entropy behavior.  
  - Unnatural scroll or error patterns.  
- Clear separation between normal and anomalous sessions was observed.  

---

## 💡 Key Learnings
- Feature engineering is **critical** for anomaly detection in user behavior.  
- **Entropy** and **normalized interactions** are powerful signals for bots.  
- Isolation Forest is a strong baseline, but can be extended with:
  - **One-Class SVM** for strict boundary detection.  
  - **Autoencoders** for non-linear patterns.  
  - **Clustering (DBSCAN)** for behavioral grouping.

---

## 🚀 Next Steps
- Extend the pipeline with user-level aggregation (combine multiple tabs).  
- Compare different anomaly detection models.  
- Build a simple **dashboard** to visualize suspicious sessions.  
- Experiment with threshold tuning for different business contexts.  

---

## 🧑‍💻 Tech Stack
- **Python** (Pandas, NumPy, Scikit-Learn, Matplotlib, Seaborn)  
- **Jupyter Notebook** for analysis and storytelling  

---

## 📌 Conclusion
This project demonstrates how **feature engineering + anomaly detection** can uncover **unusual user behavior** in web activity data.  
It was a great exercise in combining **EDA, feature design, and unsupervised modeling** to solve a real-world inspired problem.  

🔗 I’ll be sharing learnings and insights from this project on [LinkedIn](https://www.linkedin.com/).  
