# Low Engine Oil Pressure

## Objective

To identify and characterize the critical engine and vehicle parameters influencing low engine oil pressure scenarios. The goal is to enable proactive sensing by understanding normal operational behavior, and to effectively flag anomalies that may indicate early signs of failure - to reduce the “Stop Now” cases and convert them into the “Visit soon” cases.

## Process

|**Steps**|**Action**|
|---------|----------|
|Step 1 - Knowledge gaining|The existing rule-based sensing mechanisms were studied to understand current limitations and identify additional capabilities required for the POC.|
|Step 2 - Engagement with Mentor and Business Teams|Regular meetings were held with the mentor to deepen understanding of the technical track. Additional discussions were conducted with the Business Unit (BU) team to gather specific requirements and expectations.|
|Step 3 -  Identification of Key Parameters|Top 10 critical parameters relevant to low engine oil pressure were shortlisted using domain knowledge provided by the business team.|
|Step 4 - Data Collection|Healthy and unhealthy VINs were identified based on “stop now” cases. Relevant telematics and DTC datasets were then fetched from DAM for these VINs.|
|Step 5 - Preprocessing of the dataset|- Removing RPM = 0, coolant temp = 0.<br> - Categorizing vehicles into moving, idle, resting and other.<br> - Identifying if the vehicle is old or new using “TotalDistance” parameter.
|Step 6 - EDA|EDA was performed on both healthy and unhealthy VINs. The dataset was iteratively expanded by including more unique VINs and covering an average of three months of historical data per vehicle.|
|Step 7 - Model Building |Multiple models are being trained and evaluated to identify the most suitable approach for anomaly detection within the scope of the POC.|
|Step 8 - Validation|The developed models were validated against unseen VINs and failure patterns to ensure generalization and effectiveness in detecting low engine oil pressure cases not previously flagged.|


## Identifying Key Parameters

insert 1 image

## Data

- **Model**: PRO 3019  
- **Engine No**: E494  

### First Analysis

- **Format**: CSV  
- **Duration**: One-month  
- **Composition**:  
  - 15 Healthy Vehicles  
  - 15 Unhealthy Vehicles  
- **Size**:  
  - Rows: ~1.4L  
  - Columns: 20  
  - File Size: 34 MB

### Second Analysis

- **Format**: CSV  
- **Duration**: Three-month  
- **Composition**:  
  - 28 Healthy Vehicles  
  - 28 Unhealthy Vehicles  
- **Size**:  
  - Rows: ~8L  
  - Columns: 15  
  - Key Parameters: `["EngineSpeed", "EngineOilPressure", "EngineCoolantTemp"]`  
  - File Size: 45 MB

### Third Analysis (WIP)

- **Format**: CSV  
- **Duration**: Six-month  
- **Composition**:  
  - 35 Healthy Vehicles  
- **Size**:  
  - Rows: ~28.5L  
  - Columns: 13  
  - File Size: 354 MB

---

## Preprocessing of Data

1. Removing RPM = 0, CoolantTemp = 0 - After discussing with Business it was recommended to remove these values as they will not be affecting the Engine Oil Pressure - Target Variable
2. Each data point was assigned a vehicle status label based on vehicle speed and engine RPM:
- Resting: RPM is below idle threshold and vehicle speed is 0.
- Idle: RPM is within the idle range (700–900) and vehicle speed is ≤ 5 km/h.
- Moving: Vehicle speed is greater than 5 km/h.
- Other: Any other condition not covered above (e.g., high RPM at 0 speed, unexpected states).
3. Vehicles were categorized as New, Moderate, or Old based on TotalDistance:
- *New*: < 20,000 km
- *Moderate*: 20,000–100,000 km
- *Old*: > 100,000 km

insert 1 image

## EDA

### Plot 1 - Univariate Analysis: Oil Pressure Distribution

insert 1 image

- Healthy engines show a bimodal distribution with stronger concentration around 250-300 kPa
- Unhealthy engines display a more scattered distribution with lower central tendency (~150-200 kPa)
- Both distributions have significant data points at extreme values (near 0 and 1000 kPa)

### Plot 2 - Oil Pressure vs RPM

insert 1 image

- In both healthy and unhealthy engines, oil pressure generally increases with engine RPM
- Healthy engines consistently maintain higher median oil pressure across all RPM ranges
- The gap between healthy and unhealthy pressure is most pronounced at higher RPM ranges (2-3k RPM)

### Plot 3 - Oil Pressure Trend (Individual Vehicle)

insert 1 image

### Plot 4 - Correlation of each vin 

insert 2 images

- It is evident from the analysis of unhealthy VINs that vehicle behavior varies significantly across different units, even when they share the same model and engine configuration.
- The correlation between key parameters—such as RPM, vehicle speed, coolant temperature, and engine oil pressure—differs from one VIN to another.

### Plot 5 - Vehicle behaviour before and after 10 minutes of DTC trigger

insert 2 images

### Plot 6 - Vehicle Behaviour 15 minutes before and after DTC trigger

insert 2 images

## Model

### Isolation Forest

First attempt

insert 1 image 

Second attempt

insert 1 image 

- Initial attempts using Logistic Regression and Linear Regression did not yield satisfactory results on the current dataset. 

As a result, the focus has shifted towards exploring unsupervised learning techniques for more effective anomaly detection.











