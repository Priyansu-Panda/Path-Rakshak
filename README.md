This is a comprehensive `README.md` file designed for your project **"Path Rakshak"** (Protector of the Path).

It is structured to tell the "story" of your project—moving from the raw research data to the final application logic—making it perfect for a GitHub repository or a project report.

-----

# 🛡️ Path Rakshak: AI-Powered Road Safety Advisor

> **"Moving from Static Analysis to Dynamic Advisory"**

**Path Rakshak** is a machine learning-based safety advisory tool designed for commuters in Bangalore. Unlike standard navigation apps that focus on the *fastest* route, Path Rakshak focuses on the *safest* route.

It analyzes historical accident data to predict potential risks based on the user's **Location**, **Time of Travel**, and **Mode of Transport**.

-----

## 📖 Table of Contents

1.  [The Origin Story](https://www.google.com/search?q=%23-the-origin-story)
2.  [What It Does](https://www.google.com/search?q=%23-what-it-does)
3.  [How It Works (The Architecture)](https://www.google.com/search?q=%23-how-it-works-the-architecture)
4.  [Tech Stack](https://www.google.com/search?q=%23-tech-stack)
5.  [Installation & Usage](https://www.google.com/search?q=%23-installation--usage)
6.  [Future Scope](https://www.google.com/search?q=%23-future-scope)

-----

## 📜 The Origin Story

This project started as an analysis of the **Intel Collision Detection System (CDS)** dataset. The initial dataset contained raw sensor logs from buses in Bangalore during 2018 (Forward Collision Warnings, Pedestrian Alerts, Overspeeding).

**The Problem:**
Raw data is useless to a daily commuter. Knowing that "400 accidents happened in 2018" doesn't help someone deciding whether to take a bike or a cab at 6 PM today.

**The Evolution:**
We transformed this **Static Research** (Project 2) into a **Dynamic Product**.

1.  **Phase 1 (EDA):** We visualized where accidents happen.
2.  **Phase 2 (The Brain):** We trained a K-Means Clustering model to group scattered accidents into 50 distinct "Hotspot Zones."
3.  **Phase 3 (The App):** We built a logic engine that takes a user's specific context and cross-references it with our "Hotspot Database" to generate real-time advice.

-----

## 🎯 What It Does

When a user inputs their journey details, Path Rakshak generates a **Trip Risk Dashboard**.

### Inputs:

  * **Origin:** (e.g., "Jayanagar")
  * **Destination:** (e.g., "MG Road")
  * **Time:** (e.g., "18:00" / 6 PM)
  * **Mode:** (e.g., "Motorcycle")

### Outputs (The Dashboard):

The model returns a structured risk assessment:

1.  **Categorical Warnings:** "High Risk," "Route passes through Accident Hotspot."
2.  **Specific Alerts:** "This zone is high-risk for **Motorcycles**."
3.  **Time Sensitivity:** "You are traveling during Peak Accident Hours."
4.  **Numerical Score:** A Risk Score (e.g., **8.5/10**) calculated based on historical frequency.
5.  **Actionable Advice:** "Reduce speed to 30km/h," or "High-Visibility Gear Required."

-----

## ⚙️ How It Works (The Architecture)

The system operates in three distinct layers:

### Layer 1: The Translator (Geocoding)

Since the model works on mathematical coordinates (Lat/Lon) but users speak in place names, we implemented a **Geocoding Layer**.

  * **Approach:** It first checks a local dictionary of popular Bangalore locations (fast & offline).
  * **Fallback:** If the location is unknown, it uses the `Geopy` library (OpenStreetMap API) to fetch real-time coordinates.

### Layer 2: The "Brain" (K-Means Clustering)

Instead of treating accidents as thousands of random dots, we used **Unsupervised Learning (K-Means)**.

  * **Algorithm:** `KMeans(n_clusters=50)`
  * **Function:** It identified 50 geographical centers where accident density was highest.
  * **Profiling:** For each cluster, the model "memorized" the metadata:
      * *Peak Risk Time* (e.g., Evening Rush)
      * *Primary Hazard* (e.g., Pedestrian Crossing vs. Speeding)
      * *Severity Level*

### Layer 3: The Advisor (Logic Engine)

This is the inference engine that runs when a user queries the system:

1.  **Plot Route:** Calculates the user's start, end (and potentially midpoint) coordinates.
2.  **Proximity Check:** Measures the Euclidean distance between the user and the nearest "Hotspot Center."
3.  **Dynamic Scoring:**
      * *Base Score:* Derived from the hotspot's total accident count.
      * *Time Penalty:* Adds risk if user time matches Hotspot Peak Time (+1.5 risk).
      * *Mode Penalty:* Adds risk if user vehicle matches Hotspot Risk Mode (e.g., Bike at a Highway Junction).

-----

## 💻 Tech Stack

  * **Language:** Python 3.x
  * **Machine Learning:** Scikit-Learn (K-Means Clustering)
  * **Data Processing:** Pandas, NumPy
  * **Geospatial:** Geopy (Nominatim API)
  * **Visualization:** Matplotlib, Seaborn (for the research phase)

-----

## 🚀 Installation & Usage

### Prerequisites

```bash
pip install pandas numpy scikit-learn geopy matplotlib
```

### Running the Model

1.  **Load the Database:** Ensure the `hotspot_db` is trained (run the training cell in the notebook).
2.  **Call the Function:**
    ```python
    # Example Query
    path_rakshak(
        start="Jayanagar",
        end="Whitefield",
        time_hour=19,
        mode="Motorcycle"
    )
    ```

-----

## 🔮 Future Scope

1.  **API Integration:** Connect with Google Maps API to analyze the *exact* path turn-by-turn, rather than just Start/End points.
2.  **Live Traffic Data:** Ingest real-time congestion data to adjust risk scores dynamically.
3.  **Weather Overlay:** Add weather API to increase risk scores during rain/fog (Bangalore monsoons).
4.  **Crowdsourcing:** Allow users to report new hazards (potholes, broken lights) to update the Hotspot Database in real-time.

-----

### 📝 Disclaimer

*This project uses historical data (2018) for demonstration purposes. The risk scores are probabilistic estimates based on past trends, not guarantees of future events.*