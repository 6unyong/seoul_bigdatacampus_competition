# seoul_bigdatacampus_competition
A spatial optimization project implementing the Maximal Covering Location Problem (MCLP) to maximize public facility coverage

---

# 🏆 [2023 Seoul Big Data Campus Contest] Optimal Facility Location Project (MCLP)

**Team:** 김이박이
**Topic:** Optimal location selection for public amenities/vulnerable groups using Seoul public data and the MCLP optimization algorithm.

This repository contains the analytical pipeline, geospatial data processing, and mathematical optimization code (Maximal Covering Location Problem - MCLP) used for the **2023 Seoul Big Data Campus Contest**. The project aims to identify the optimal locations for new urban facilities to maximize public benefit using spatial data.

---

## 📌 Project Overview
When expanding urban infrastructure (e.g., acoustic traffic signals for the visually impaired, welfare facilities for the elderly, EV charging stations), achieving the highest efficiency within a limited budget is crucial. This project identifies specific areas in Seoul where demand exceeds current supply and applies the **MCLP (Maximal Covering Location Problem) algorithm** to propose optimal priority installation locations that maximize demand coverage.

### Key Objectives
* **Data-Driven Decision Making:** Calculates a demand index based on precise spatial and demographic data from the Seoul Big Data Campus, rather than intuition or simple heuristics.
* **Spatial Optimization (MCLP):** Mathematically derives the coordinates of $P$ optimal locations that cover the maximum demand (weight) within a predefined service radius ($S$).
* **Geospatial Visualization:** Intuitively maps the optimal locations and beneficiary zones using Python visualization libraries.

---

## 📊 Data Sources
This analysis integrates public and restricted data provided by the **Seoul Big Data Campus**.
* **Demand Data (Demand Points):** Target population (e.g., disabled, elderly) residential and floating population data, related public facility locations, public transit (subway, bus) ridership history, etc.
* **Supply Data (Candidate Sites):** Existing facility locations and potential candidate coordinate data (e.g., crosswalks, existing infrastructure).
* **Other Spatial Data:** Administrative district boundaries, road network data, and accident-prone area polygons.

---

## 🛠 Methodology

### 1. Spatial Preprocessing
* Divides the target area (specific districts or the entirety of Seoul) into spatial units such as Hexagons or Grids.
* Aggregates derived variables such as population density, floating population, and accessibility within each grid using spatial joins.

### 2. Demand Scoring & Weighting
* Calculates the final 'Demand Weight (Score)' for each grid using methodologies like AHP (Analytic Hierarchy Process) or Min-Max Scaling.
* Grids with high concentrated demand are designated as the main targets for the MCLP model.

### 3. Optimization Algorithm: MCLP
~~~python
# Objective Function: Maximize the total covered demand
# Constraints:
# 1. A demand point is covered if at least 1 facility is located within distance S
# 2. The total number of newly installed facilities equals P
~~~
* **Parameters:** Target number of installations ($P$), effective coverage radius of the facility ($S$ meters).
* **Algorithm:** Formulates the problem as a Mixed Integer Linear Program (MILP) to determine the optimal binary state (`0` or `1`, indicating installation status) for each candidate site.

### 4. Evaluation & Visualization
* Visually compares the coverage radii of existing locations versus the newly recommended sites using libraries like Folium and GeoPandas.
* Quantifies the reduction of service blind spots and the expected increase in the beneficiary population.

---

## 💻 Tech Stack & Requirements

This code handles the entire process from data preprocessing to spatial optimization and visualization in a Python environment.

~~~bash
# Core Data Science & Spatial Analysis
pip install pandas numpy geopandas shapely

# Optimization Solvers (Choose based on your specific implementation)
pip install pulp      # Or pyomo, gurobipy, etc.

# Visualization
pip install matplotlib seaborn folium mapclassify
~~~

---

## 🚀 How to Run

1. Place your preprocessed demand points and candidate sites datasets (`.csv` or `.geojson`) in the `data/` directory. *(Note: Due to contest security regulations, original Seoul Big Data Campus data is not uploaded. Please use sample data to test the pipeline.)*
2. Open the `MCLP.ipynb` notebook.
3. In the Hyperparameters section, adjust the coverage radius (`RADIUS`) and the target number of facilities (`NUM_FACILITIES`) according to your analysis scenario.
4. Run the cells sequentially to execute the optimization model and render the final map visualization.

---

## 🏆 Expected Effects
* **Efficient Budget Execution:** Establishes a scientific basis for prioritizing limited municipal budgets where they are most urgent and impactful.
* **Enhanced Citizen Safety & Convenience:** Drastically reduces transportation and welfare blind spots through data-driven location selection.
