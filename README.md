# Nexthikes-Bike-Sharing-Data-Architecture
Developed a complete end-to-end data architecture and interactive analytics solution for NextHikes, a bike-sharing company, by integrating three disjointed CSV datasets containing ride records, weather conditions, and user information.

**NextHikes Operations Team**  
**Prepared by: Sumit Lokhande**  

## Project Overview
This project involved building a complete **data architecture and analytics solution** for NextHikes bike-sharing operations using three disjointed CSV files. The goal was to transform raw, fragmented data into a clean, dynamic, and insightful analytics system (Management Cockpit) that reveals true business drivers — especially the dominance of commuter (registered) users.

The final deliverable is a robust Excel-based analytics dashboard with engineered features, statistical validation, and actionable strategic recommendations.


## What I Did – Project Journey

### SECTION 1: Initial Data Ingestion & Structural Integration

- **Integrated three separate CSV files** into a single unified dataset:
  - Performed **horizontal join** (merge) on the first two files using the **instant** column as the Primary Key.
  - Used **Append** method for the third dataset, ensuring perfect column alignment to prevent data shifting.
- **Data Type Overhaul**:
  - Converted `dteday` to Short Date format.
  - Ensured `hr` (0-23) remained as Integer for proper chronological sequencing.
  - Converted the entire dataset into an **Official Excel Table** for dynamic updates (formulas, pivots, and slicers auto-refresh when new data is added).

### SECTION 2: Data Auditing & Integrity ("Gut-Check")

- Performed **Cross-Footing validation**:
  - Created check column: `=[@casual] + [@registered] = [@cnt]`
  - Validated all **17,379 rows** — every row returned TRUE (no data loss during merging/appending).
- Investigated missing values in `atemp` column (~10-12 blank records):
  - Attempted imputation using `AVERAGEIFS` based on hour and day.
  - Realized imputed values were unreliable → **Decision**: Deleted the `atemp` column entirely to maintain data honesty and integrity over artificial completeness.

### SECTION 3: Feature Engineering (Making Data Tell a Story)

- **Translated weekday codes** into human-readable names:
  - Formula: `=CHOOSE([@weekday]+1, "Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat")`
- **Created "Rush Hour" binary flag** (most complex formula):
  - Defined as 7-9 AM and 4-7 PM (commuter peaks).
  - Formula: `=IF(OR(AND([@hr]>=7,[@hr]<=9), AND([@hr]>=16,[@hr]<=19)), "Rush Hour", "Other")`
- **Converted weather codes** into descriptive text using IFS:
  - 1 → Clear, 2 → Cloudy, 3 → Rain/Snow
- These engineered features made slicers and charts manager-friendly and removed the need for a data dictionary.

### SECTION 4: The Analysis Engine (5-Pivot Strategy)

Built a comprehensive pivot table system:

1. **The Pulse** – Hourly average demand (`hr` vs avg `cnt`) → "Camel Hump" pattern
2. **User Type Breakdown** – Casual vs Registered by weather conditions
3. **Efficiency Analysis** – Demand using the "Rush Hour" flag (Money Chart)
4. **Calendar View** – Monthly demand breakdown for promotion planning
5. **Summary Weather Check** – High-level weather impact overview

### SECTION 5: Statistical Deep-Dive

- Calculated key statistics in a dedicated worksheet:
  - Registered users = **92%** of total business
  - Strongest correlation: **Hour (0.366)**
  - Strongest negative correlation: **Humidity (-0.254)**
  - Standard Deviation of demand: **50.986** (extremely volatile)
  - Overall Average demand: **58.3**

### SECTION 6: Management Dashboard & KPI Cards

- Built a clean **"Management Cockpit"** dashboard:
  - KPI Cards at the top: Total Rentals, Avg/Hr, Peak Demand
  - Four linked charts from main pivots
  - Independent slicers (deliberately not connected) for flexible "compare & contrast" analysis

### SECTION 7–8: Key Quantitative Insights

**Major Findings:**

- **Commuter Power**: 92% Registered vs 8% Casual → NextHikes is primarily a **commuter utility**, not a tourist business.
- **Weather Resilience**: Demand only drops ~14% in bad weather (Clear: 61.6 avg | Bad: 53.1 avg).
- **Humidity Paradox**: Humidity has stronger negative impact (-0.254) than temperature has positive impact (0.229).
- **Weekday Advantage**: Weekday average (60.6) is ~30% higher than weekend (46.6).
- **Volatility Factor**: Standard Deviation nearly matches the mean → business is highly "spiky".

### SECTION 9: Strategic Recommendations (3-Pillar Strategy)

1. **Rush Hour Priority** – Ensure maximum staff and bike availability during 7-9 AM and 4-7 PM.
2. **Targeted Subscription Marketing** – Focus on loyalty programs for existing registered users (especially top 10% commuters).
3. **Humidity-Based Alerts** – Implement app push notifications or targeted discounts on high-humidity days to boost ridership during natural dips


## Key Technical Decisions

- Prioritized **data honesty** over completeness (deleted `atemp`).
- Used **dynamic Excel Tables** for future-proofing.
- Created **human-friendly features** instead of keeping numeric codes.
- Kept slicers independent for maximum analytical flexibility.
- Focused heavily on **commuter behavior** based on 92% registered user dominance.


## Tools & Technologies Used

- Microsoft Excel (Advanced)
- Excel Tables
- Pivot Tables & Charts
- Advanced Formulas (CHOOSE, IFS, OR/AND, AVERAGEIFS, CORREL, etc.)
- Cross-Footing Data Validation
- Dashboard Design (KPI Cards + Slicers)


## Business Impact

This project transformed raw, disjointed CSV files into a powerful decision-making cockpit that clearly proves:

> **NextHikes is a commuter transit system.**  
> Success depends on understanding rush-hour patterns, registered user behavior, and managing demand volatility.

The architecture is scalable, auditable, and ready for future data additions.

**For:** NextHikes Operations Team
