# Dynamic Supply Chain & Logistics — Exploratory Data Analysis

## Project Overview

This project explores a logistics and supply chain dataset containing hourly operational records. The analysis examines transportation efficiency, shipment delays, traffic and port congestion, warehouse inventory, supplier reliability, cargo condition, driver-related indicators, shipping costs, and disruption risk.

The goal is to use exploratory data analysis (EDA), statistical summaries, visualizations, and derived features to identify operational patterns and translate them into practical business recommendations.

## Dataset

**File:** `dynamic_supply_chain_logistics_dataset.csv`

The uploaded dataset contains:

- **32,065 records**
- **26 original columns**
- **Timestamp range:** 1 January 2021 to 29 August 2024
- **Missing values:** 0 across the original dataset
- **Exact duplicate rows:** 0

The dataset description identifies the source as a Southern California logistics network and describes data from GPS tracking, IoT sensors, warehouse management systems, and external data providers. It covers transport modes and operational factors across logistics activities.

### Main data fields

The original columns include:

- **Time and location:** `timestamp`, `vehicle_gps_latitude`, `vehicle_gps_longitude`
- **Transport and delay:** `fuel_consumption_rate`, `eta_variation_hours`, `traffic_congestion_level`, `delivery_time_deviation`
- **Warehouse and order operations:** `warehouse_inventory_level`, `loading_unloading_time`, `handling_equipment_availability`, `order_fulfillment_status`, `historical_demand`
- **Weather, port, and cost:** `weather_condition_severity`, `port_congestion_level`, `shipping_costs`, `customs_clearance_time`
- **Supplier performance:** `supplier_reliability_score`, `lead_time_days`
- **Cargo and route risk:** `iot_temperature`, `cargo_condition_status`, `route_risk_level`
- **Driver and disruption indicators:** `driver_behavior_score`, `fatigue_monitoring_score`, `disruption_likelihood_score`, `delay_probability`, `risk_classification`

## Business Questions

The notebook investigates the following themes:

1. **Univariate analysis:** What do shipping costs, congestion, fulfillment-related fields, cargo condition, driver behavior, and fatigue distributions look like?
2. **Bivariate analysis:** How are congestion and delay related? How do supplier reliability, lead time, fatigue, driver behavior, port congestion, customs clearance, weather, fuel consumption, and shipping costs vary together?
3. **Multivariate analysis:** How do traffic, weather, and port conditions relate to delay and disruption scores? How do route risk, driver indicators, cargo temperature, inventory, demand, and lead time interact with operational outcomes?
4. **Temporal analysis:** How do congestion, fuel consumption, costs, demand, inventory, weather, disruption indicators, loading/unloading time, and customs clearance vary by hour, day, month, and year?

## Methodology

The Jupyter Notebook follows this workflow:

1. Load the original CSV and inspect its dimensions, columns, data types, and descriptive statistics.
2. Assess data quality by checking missing values, duplicate rows, timestamp validity, and the observed values of binary or bounded fields.
3. Parse timestamps and derive time features such as hour, day of week, month, and year.
4. Engineer additional analysis features, including:
   - `total_transit_latency`
   - `hour_of_day`, `day_of_week`, `month`, and `year`
   - `fuel_efficiency_ratio` (defined in this project as shipping cost divided by fuel-consumption rate)
   - a risk and human-factor composite
   - an inventory-to-demand ratio
5. Perform univariate, bivariate, multivariate, and temporal EDA.
6. Use descriptive statistics, correlations, grouped comparisons, and hypothesis testing where appropriate.
7. Summarize findings and propose operational recommendations.

All engineered columns are created in the notebook's in-memory analysis dataframe. The original CSV is not modified.

## Key Findings from the Uploaded Dataset

The following figures are calculated from the uploaded CSV and summarized in the notebook:

- The dataset contains **32,065 records and 26 original columns**.
- The observed timestamp range is **1 January 2021 to 29 August 2024**.
- The original file has **no missing cells and no exact duplicate rows**.
- Mean shipping cost is approximately **$459.37**, while the median is approximately **$389.00**.
- Shipping-cost skewness is approximately **0.387**, indicating a modest right skew in this dataset.
- **36.54%** of records have traffic congestion at or above 7 on the stated 0–10 scale.
- **61.02%** of records have port congestion at or above 7 on the stated 0–10 scale.
- The mean recorded `delay_probability` is approximately **0.699**.
- The mean recorded `disruption_likelihood_score` is approximately **0.804**.
- The `risk_classification` field contains three categories: High Risk (23,944 records), Moderate Risk (5,011 records), and Low Risk (3,110 records).

These are descriptive results for the uploaded file; they should not automatically be interpreted as calibrated operational KPIs.

## Important Data Quality and Interpretation Notes

The notebook deliberately reports observed values instead of silently forcing fields to match the dataset description.

- **Date coverage differs from the description:** the description says the dataset spans January 2021 to January 2024, but the uploaded CSV contains timestamps through **29 August 2024**.
- **Geographic coordinates should be validated:** some sample coordinates in the file do not appear consistent with a dataset limited to Southern California. Confirm the coordinate reference and geographic scope before making location-specific conclusions.
- **Fields described as binary may contain continuous values:** for example, `order_fulfillment_status`, `cargo_condition_status`, and `handling_equipment_availability` should be checked against the actual data dictionary and collection process.
- If `order_fulfillment_status` is not strictly encoded as 0 and 1, a verified on-time fulfillment percentage cannot be calculated from it. Any threshold-based proportion is only an exploratory proxy.
- Confirm the definitions, units, and valid ranges of score/probability fields before using them for operational decisions.
- Correlation and association do not prove causation. The dataset description does not establish a causal experiment or sampling design.
- The engineered `fuel_efficiency_ratio` follows the requested formula (`shipping_costs / fuel_consumption_rate`). It is a cost-to-fuel-rate ratio, not a conventional physical fuel-efficiency measure.

## Business Recommendations

The analysis suggests several actions to investigate and validate with operational teams:

1. **Congestion-aware dispatch:** evaluate congestion bands against ETA variation and delivery-time deviation; consider route-specific planning buffers during high-congestion periods.
2. **Port and customs coordination:** examine the relationship between port congestion and customs clearance time; review documentation readiness and appointment scheduling.
3. **Supplier performance monitoring:** track supplier reliability alongside lead-time patterns and warehouse inventory buffers; assess whether supplier-specific safety-stock policies are justified.
4. **Driver fatigue management:** investigate whether fatigue indicators align with driver behavior and risk categories; review shift and rest practices where supported by operational evidence.
5. **Cargo condition monitoring:** investigate temperature readings and cargo-condition values by route and risk group, using cargo-specific acceptable temperature ranges.
6. **Shipping-cost control:** compare shipping costs with fuel consumption, customs clearance time, and route-risk groups before changing routes or negotiating rates.
7. **Data governance:** validate field definitions, units, encodings, and score ranges—especially fields described as binary or as bounded probabilities—before publishing performance KPIs.

These are recommendations for further operational review, not claims that the observed associations establish cause and effect.

## Repository Structure

Keep the notebook and original dataset together so the notebook can load the CSV using its relative filename.

```text
Dynamic-Supply-Chain-Logistics-EDA/
├── Dynamic_Supply_Chain_Logistics_EDA.ipynb
├── dynamic_supply_chain_logistics_dataset.csv
├── README.md
└── presentation.pptx
```

The presentation may be submitted as a PDF instead of a PowerPoint file.

## How to Run the Notebook

### 1. Clone or download the repository

```bash
git clone <your-github-repository-url>
cd Dynamic-Supply-Chain-Logistics-EDA
```

### 2. Install the required packages

```bash
pip install pandas numpy matplotlib scipy seaborn jupyter nbclient
```

### 3. Launch Jupyter Notebook

```bash
jupyter notebook
```

Open `Dynamic_Supply_Chain_Logistics_EDA.ipynb` and run the cells from top to bottom.

**Important:** Keep `dynamic_supply_chain_logistics_dataset.csv` in the same directory as the notebook. The notebook expects this filename.

## Tools and Libraries

- Python
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- Seaborn
- SciPy

## Deliverables

- [x] Exploratory Data Analysis notebook (`.ipynb`)
- [ ] Final presentation (`.pptx` or `.pdf`)
- [x] Project README (`.md`)
- [x] Original dataset (`.csv`)

## Conclusion

This project provides a structured exploratory view of logistics and supply chain operations. It combines data-quality checks, feature engineering, statistical analysis, and visual exploration to identify patterns related to congestion, delays, costs, inventory, supplier performance, cargo condition, and operational risk.

The findings should be treated as exploratory until the dataset's geographic scope, field encodings, score definitions, and operational meaning are confirmed with the data provider.
