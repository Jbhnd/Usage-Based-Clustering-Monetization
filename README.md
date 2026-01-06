# Usage-Based Clustering & Monetization

This project analyzes mobile phone usage data to **segment users by engagement level** and **assign pricing tiers** using **K-Means clustering**.
The output supports **product strategy, monetization, and dashboarding**.

---

## Project Overview

**Goal:**
Identify distinct user usage patterns (Light, Medium, Heavy users) based on mobile behavior and translate these segments into **pricing tiers and revenue forecasts**.

**Key Outcomes:**

* Daily and per-user usage metrics
* User segmentation via K-Means clustering

* Tier-based pricing strategy
* Aggregated datasets for visualization tool(Tableau)
* Revenue forecast by usage tier

---

## Business Use Case

This project simulates how a product or company could:

* Segment users based on engagement
* Design fair, usage-based pricing
* Forecast revenue by tier
* Monitor engagement trends over time

---

## Data Source

* **Dataset:** Mobile Phone Usage Dataset (MPUD)
* **Granularity:** Event-level sensor data
* **Participants:** First 120 users
* **Sensors Used:**

  * `Screen` — screen-on events
  * `App` — app usage sessions
  * `Notif` — notifications received

> Over **10M raw rows**, reduced to ~2.3M relevant events after filtering.

---

## Tech Stack

* **Python**
* **Pandas / NumPy**
* **Scikit-learn**
* **Matplotlib / Seaborn**
* **SciPy**
* **Tableau (downstream visualization)**

---

## Feature Engineering

### Daily Metrics (Per User)

* **Screen-on time (hours/day)**
  Estimated using unique active hours × 0.5 hrs
* **App sessions per day**
* **Notifications per day**

### Aggregated User Metrics

Computed as **per-user daily averages**:

* `avg_daily_screen_time`
* `avg_daily_sessions`
* `avg_daily_notifications`

---

## Data Cleaning & Outlier Handling

* Removed missing critical fields
* Filtered only relevant sensors
* Used **IQR method** to remove extreme outliers for:

  * Screen time
  * App sessions

This improves clustering stability and interpretability.

---

## Clustering Approach

### Feature Scaling

```text
MinMaxScaler applied to:
- avg_daily_screen_time
- avg_daily_sessions
```

### Usage Score

```text

usage_score = mean(scaled_screen_time, scaled_sessions)
```

### Optimal K Selection

* Used **Elbow Method (SSE)**
* Chosen **K = 3**

### Final Clusters

| Cluster | Tier   | Description    |
| ------- | ------ | -------------- |
| 0       | Light  | Low engagement |
| 1       | Medium | Moderate usage |
| 2       | Heavy  | Power users    |

---

## Pricing Strategy

| Tier   | Monthly Price (USD) |
| ------ | ------------------- |
| Light  | $5                  |
| Medium | $15                 |
| Heavy  | $30                 |

Each user is automatically assigned:

* Usage tier
* Price point
* Cluster label

---

## Revenue Forecast

Revenue is estimated by summing tier prices across users:

* Visualized via bar chart
* Aggregated by usage tier
* Useful for product & finance teams

---

## Included Visuals

* Distribution of screen time and sessions
* Cluster comparison bar charts
* Elbow curve for K selection
* Revenue forecast by tier

---

## 📌 Key Takeaway

This project demonstrates how **raw behavioral data** can be transformed into:

* Actionable user segments
* Monetization strategies
* Executive-ready dashboards

A practical example of **data science driving product decisions**.

---

## How to Run

```bash

pip install pandas numpy matplotlib seaborn scikit-learn scipy
python analysis.py
```

Ensure the MPUD dataset is placed in:

```text
./mpud/mobile_phone_use/data/
```

---
