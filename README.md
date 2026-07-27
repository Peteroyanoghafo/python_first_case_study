# Weather Impact Analysis System (Cropping Systems Assessment)

> **Course:** SmartBizCrux Python Study Group - Case Study 12  
> **Author:** Peter Osazemwengie Oyanoghafo  
> **Domain:** AgTech / Decision Support Systems  
> **Constraints:** Built strictly using core Python concepts (Variables, Data Types, Operators, Logical Control).

---

## Summary
In agricultural production, daily weather variations determines field operations and risk management. This project implements a Decision Support System developed for **AgriClimate Solutions Ltd.** The script evaluates daily microclimate data against crop-specific physiological thresholds to determine environmental favorability and automatically flag farms requiring immediate intervention.

The analysis evaluates two location scenarios (Kaduna — Maize; Benue — Rice) to demonstrate  how weather anomalies and lack of infrastructure (irrigation) trigger management alerts.

---

## Learning Objectives & Core Concepts Applied

* **Variables & Primitive Data Types:** Storing string descriptors, integer measurements, floating-point thresholds, and boolean state flags.
* **Arithmetic Operations:** Calculating environmental metrics such as rainfall deficits and temperature safety margins.
* **Augmented Assignment:** Updating variable values dynamically using assignment operators (`+=`).
* **Comparison & Threshold Logic:** Testing recorded weather values against upper and lower physiological limits using relational operators (`<=`, `>=`).
* **Boolean Algebra & Compound Logic:** Combining non-linear environmental constraints using logical operators (`AND`, `OR`, `NOT`).
* **Structured Output Generation:** Generating a formatted console report for field officers and farm managers.

---

## Industry Scenario & Data Inputs

Field officers collect daily weather metrics from various farming communities. The system processes raw readings against specific physiological requirements:

| Environmental Metric | Kaduna (Maize) | Benue (Rice - Challenge) | Evaluation Threshold |
| :--- | :---: | :---: | :--- |
| **Current Temperature (°C)** | 31 | 38 | Max Safe Temp: 35°C|
| **Initial Rainfall (mm)** | 18 | 12 | Min Required: 20mm (Kaduna) / 25mm (Benue) |
| **Mid-day Rainfall Additions** | +8 mm | 0 mm | Updated total evaluated |
| **Relative Humidity (%)** | 72% | 68% | Observation data  |
| **Wind Speed (km/h)** | 16 km/h | 21 km/h | Observation data  |
| **Irrigation Available** | `True` | `False` | Infrastructure flag |

---

## Programmatic Logic & Execution Flow

### 1. Data Initialization & Arithmetic Calculations
```python
# Primary Farm Setup (Kaduna)
farm_location = "Kaduna"
crop_type = "Maize"
temperature_C = 31
rainfall = 18
min_rainfall_required = 20
max_safe_temp_C = 35
irrigation_system_available = True

# Deficit and Margin Calculations
rainfall_difference = min_rainfall_required - rainfall  # 20 - 18 = 2 mm
temperature_margin = max_safe_temp_C - temperature_C    # 35 - 31 = 4 °C

# In-place rainfall update (Additional 8mm received later in the day)
rainfall += 8  # Updated rainfall = 26 mm
```
### 2. Boolean Threshold & Logical Evaluation
```python
# Threshold checks
rainfall_requirement_met = rainfall >= min_rainfall_required  # 26 >= 20 -> True
temperature_safe = temperature_C <= max_safe_temp_C          # 31 <= 35 -> True

# Cropping favorability logic (Requires BOTH conditions to be True)
cropping_favored = rainfall_requirement_met and temperature_safe  # True AND True -> True

# Management alert logic (Action required if conditions UNFAVORABLE OR NO IRRIGATION)
farmer_action_required = not cropping_favored or not irrigation_system_available  # False OR False -> False
```
### Analytical Findings & Bonus Answers
1.	Which farm received more total rainfall? <br>
Kaduna received 26 mm (18 mm + 8 mm) vs. Benue's 12 mm.<br>
Kaduna received 14 mm more rainfall than Benue.
3.	Which farm has a safer temperature for crop growth? <br>
Kaduna (True). <br>
Kaduna's temperature (31°C) is safely below the 35°C threshold. <br>
Benue recorded 38°C, exceeding the heat tolerance limit (False).
5.	Which farm meets the minimum rainfall requirement? <br>
Kaduna (True). <br>
Post-rain updates total 26 mm (exceeding the 20 mm threshold). <br>
Benue managed only 12 mm against a 25 mm crop requirement (False).
7.	Which farm exhibits favorable growing conditions? <br>
Kaduna (True). Both moisture and temperature parameters were within optimal ranges.
8.	Which farm requires immediate action from the farm manager? <br>
Benue (True). <br>
Kaduna requires no intervention (False).

## Extension Officer Recommendation & Field Decision
### Priority Field Visit Location: Benue Farm

#### Agronomic Rationale:
1.	Severe Thermal Stress: The recorded temperature of 38°C exceeds the physiological safety limit (35°C) for Rice, threatening increased evapotranspiration rates,, wilting and eventual vascular damage and death.
2.	Critical Moisture Deficit: Recorded rainfall (12 mm) fell short of the 25 mm minimum requirement by 13 mm.
3.	Absence of Mitigation Infrastructure: The farm lacks an operational irrigation system (irrigation_available = False), preventing supplementary watering to alleviate drought stress. Immediate emergency intervention or supplemental shading is necessary.

