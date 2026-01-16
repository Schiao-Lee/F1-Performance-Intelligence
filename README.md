# F1 Big Data Analytics Project – Power BI Dashboard

This folder contains the Power BI analytics layer of the project **“F1 Big Data Analytics: From Ingestion to Intelligence.”**
It transforms curated Formula 1 data (1950–2024) from the Databricks Gold layer into an interactive, production‑style performance intelligence system.

The dashboard is designed not as a static report, but as a multi‑level analytical product supporting executive monitoring, driver evaluation, team strategy analysis, circuit risk profiling, and lap‑by‑lap diagnostics.

---

## System Context

```
Kaggle API
   ↓
Databricks (Bronze → Silver → Gold, Delta Lake, Unity Catalog)
   ↓
Power BI Semantic Model (Star Schema)
   ↓
Incremental Refresh + Aggregation Tables
   ↓
Interactive Dashboards & Drill‑through Analytics
```

---

## Data Model (Semantic Layer)

The Power BI model follows a star schema optimized for analytical workloads.

### Dimensions

* Dim_Races
* Dim_Drivers
* Dim_Constructors
* Dim_Circuits
* Date

### Fact Tables

* **Fact_Results** – race outcomes and championship points
* **Fact_Pit_Stops** – pit stop operations
* **Fact_Lap_Times** – lap‑level telemetry (incremental refresh enabled)
* **Fact_Lap_Agg** – aggregated lap statistics (race × driver grain)

### Semantic Enhancements

Business‑friendly display fields are implemented for slicers and tooltips:

* Driver Display → `Name (Nationality)`
* Race Display → `Year + Round + Race Name`
* Circuit Display → `Circuit Name – Country`

---

## Engineering Features

### Incremental Refresh

Applied to high‑volume fact tables:

* Fact_Lap_Times
* Fact_Pit_Stops

Configuration:

* Archive window: **3 years**
* Refresh window: **last 7 days**

This enables scalable refresh performance while preserving long‑term historical data.

### Aggregation Table (Fact_Lap_Agg)

Lap‑level data (~580k rows) is reduced to race‑driver aggregates (~11k rows):

* Average lap time
* Best lap time
* Lap count

This table powers most pace and consistency visuals, significantly improving interactivity and query performance.

### Measure Layer

All business logic is centralized in a dedicated measures table, including:

* Championship metrics: points, wins, podiums, top‑10 finishes
* Reliability metrics: DNF rate, finish rate
* Operational metrics: average pit duration, pit stops per race
* Pace metrics: average and best lap times

---

## Dashboard Pages

### 1. Executive Overview

High‑level season summary combining sporting results and operational efficiency.

**Key visuals:**

* KPI cards (points, wins, podiums, finish rate, pit duration, races)
* Championship trend by round
* Top drivers and constructors ranking
* Pit stop efficiency vs championship performance scatter plot

**Purpose:** explain *who dominates the season and why*.

![Executive Overview](page_1.png)

---

### 2. Driver Performance Deep Dive

Driver‑centric diagnostics of racecraft, consistency, and pace.

**Key visuals:**

* Driver KPI profile
* Grid vs finish position scatter (racecraft analysis)
* Average lap time trend across rounds
* Lap consistency proxy (standard deviation)
* Race‑by‑race performance table

**Purpose:** decompose driver performance beyond total points.

![Driver Performance Deep Dive](page_2.png)

---

### 3. Constructor & Strategy

Team‑level operational efficiency and reliability analysis.

**Key visuals:**

* Constructor KPI cards
* Pit duration vs points per race scatter
* DNFs by constructor
* Performance matrix by circuit country

**Purpose:** evaluate how strategy execution and reliability affect championship outcomes.

![Constructor & Strategy](page_3.png)

---

### 4. Race & Circuit Intelligence

Circuit‑level pace and risk profiling.

**Key visuals:**

* Circuit KPI cards (pace, best lap, lap volume, DNF rate)
* DNF rate ranking by circuit
* Fastest circuits by average lap time
* Pit duration vs circuit pace scatter

**Purpose:** identify high‑risk and high‑sensitivity circuits for strategic planning.

![Race & Circuit Intelligence](page_4.png)

---

### 5. Drill‑through: Race Detail (Lap‑by‑Lap)

Interactive diagnostic page accessible via right‑click drill‑through from any aggregated view.

**Key visuals:**

* Lap‑by‑lap pace evolution line chart
* Pit stop details table

**Purpose:** connect executive‑level KPIs to telemetry‑level root cause analysis.

![Race Detail – Lap by Lap](page_5.png)

---

## Skills Demonstrated

* Data warehouse modeling (Medallion architecture, star schema)
* Power Query engineering
* Incremental refresh design
* Aggregation table strategy
* Advanced DAX measure development
* Performance‑oriented BI modeling
* Analytical UX design (cross‑filtering, drill‑through, tooltips)

---

## File

* `motorsport_performance_intelligence.pbix`

---

## License & Data Source

The dataset is based on publicly available Formula 1 historical data retrieved via the Kaggle API and is used strictly for educational and analytical purposes.

---

*Part of the F1 Big Data Analytics Project: From Ingestion to Intelligence.*
