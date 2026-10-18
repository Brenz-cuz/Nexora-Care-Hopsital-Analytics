# Nexora-Care-Hopsital-Analytics
Power BI healthcare analytics project analysing patient flow, bed occupancy, staffing performance, capacity forecasting and scenario planning across 39 fictional UK hospitals.

**Project overview**
Nexora Care is a fictional healthcare organisation operating 39 hospitals across the UK. I developed a three-page Power BI dashboard to bring together admissions, emergency department activity, bed occupancy, elective surgery and staffing information for operational planning.
The project combines data cleaning, dimensional modelling, DAX measures, exploratory analysis, a 30-day occupancy forecast and interactive scenario planning.
**Business problem**
Hospital planners need to balance emergency demand, elective activity, beds and staff. Analysing these datasets separately can make emerging capacity pressures difficult to identify. This project provides a consolidated view of demand, capacity and staffing.
**Dashboard pages**
1. Patient Flow and Admission Overview: Admissions, discharges, ED arrivals, length of stay and elective cancellations.
2. Bed Capacity and Staffing Performance: Bed utilisation, weekday patterns, staffing gaps and a 30-day occupancy forecast with a 95% confidence interval.
3. Capacity Forecast and Scenario Planning: What-if parameters for emergency admission spikes, flu-related demand and discharge delays

## Dashboard Preview

### 1. Patient Flow and Admission Overview
![Patient Flow Dashboard](Nexora%20Admission%20Overview%20Dashboard.png)
Covers admissions, discharges, ED arrivals, admission types, length of stay and elective-surgery cancellations.

### 2. Bed Capacity and Staffing Performance
![Bed Capacity Dashboard](Nexora%20Bed%20Capacity%20Dashboard.png)
Shows staffed capacity, occupancy patterns, workforce performance, ward-level peaks and a 30-day occupancy forecast with a 95% confidence interval.

### 3. Capacity Forecast and Scenario Planning
![Scenario Planning Dashboard](Nexora%20Capacity%20Scenario%20Dashboard.png)
Uses What-if controls for emergency admission spikes, flu-related demand surges and discharge delays to estimate changes in occupancy, available beds and potential shortfalls.

**Dataset description**
The model combined five operational datasets and a shared hospitals dimension:

Data set: Admissions and discharges	
Key information: Admission and discharge datetimes, type, source, ward, specialty and length of stay
Purpose : Analyse patient inflow, outflow and stays
Data set: Bed occupancy
Key information: Total, staffed, occupied and closed beds; hospital, ward and observation datetime
Purpose : Monitor operational bed use
Data set: ED arrivals
Key information: Arrival datetime, mode, triage category, outcome, admission time and bed requests
Purpose : Assess emergency demand
Data set: Elective surgery 
Key information: schedule	Surgery date, procedure group, specialty, required ward/bed type and status	
Purpose : Explore scheduled demand and cancellations
Data set: Staffing and resources
Key information: Planned and actual staffing, role, hospital, ward, date and safe-staffing indicator
Purpose : Compare workforce provision against plans
Data set: Hospitals dimension
Key information: Hospital ID, name, city, region and size tier	
Purpose : Support consistent hospital and regional filtering

The cleaned admissions dataset contained approximately 1.25 million distinct admissions (September 2024–August 2026). The ED dataset contained approximately 1.96 million distinct arrivals. All five operational datasets covered the same 39 hospitals. The elective schedule extended to November 2026.

**Data cleaning and preparation**
I used Power Query to:
- Trim and clean text, remove non-printing characters and standardise categories such as ward, specialty, bed type and staff role.
- Preserve meaningful missing values: for example, blank discharge information for patients not yet recorded as discharged, and missing staffing observations rather than incorrectly interpreting them as zero staff.
- Label missing procedure groups Not Recorded.
- Remove exact duplicates and review potential staffing duplicates using hospital, ward, date and staff role.
- Create consistent admission, discharge, ED-arrival and occupancy dates, along with calendar attributes.
- Recalculate length of stay from admission and discharge datetimes.
- Use distinct counts where appropriate to avoid inflating admissions, ED arrivals and surgery KPIs.
  
**Data modelling**
I structured the model around the five operational fact tables, a shared Hospitals dimension and a Calendar/Date table. This supported hospital and region filters, time trends, weekday comparisons and drill-down analysis. DAX measures were organised in a dedicated measures table.
The tables support comparisons across common dimensions, but the project does not assume direct patient-level linkage across every operational dataset.
**DAX measures and analysis**
The project developed measures for admissions and discharges, ED conversion, capacity utilisation, workforce performance and scenario planning. Selected analytical definitions documented in the project report include:

Net Patient Flow = Total Admissions - Total Discharges
ED Conversion Rate = ED Admissions / Total ED Arrivals
Bed Occupancy Rate = Occupied Beds / Staffed Beds
Closed Beds = Total Beds - Staffed Beds
These are business definitions, not a copy of the exact DAX source code. The Power BI model also includes measures for staffing performance, elective cancellations, available capacity and scenario-driven bed demand.

The analysis considered seasonal demand, inflow versus outflow, ED admissions, length of stay, occupancy by weekday, planned versus actual staffing, and projected capacity under selected assumptions.

**Key findings**
Metric and	Result
Admissions	Approximately =  1.25 million
Discharges	Approximately = 1.24 million
Net patient flow =	+5,310 admissions minus discharges
ED conversion rate = Approximately 26.1%
Elective-surgery cancellation rate	= 8.17%
Highest weekday occupancy = Friday: 83.08%
Lowest weekday occupancy = Sunday: 65.17%
Overall staffing gap	Actual assignments = approximately 10.2% below planned
Recorded safe-staffing rate	= Approximately 84%
General Medicine average length of stay	= Approximately 5.76 days
General Medicine peak occupied-bed value = 136 beds

**What the findings suggest:**
- Admissions, ED activity and occupancy showed recurring winter pressure, supporting earlier seasonal preparations.
- Friday occupancy exceeded Sunday occupancy by 17.91 percentage points, highlighting a pattern worth investigating in relation to discharges and elective scheduling.
- General Medicine combined a long average stay with the highest recorded peak occupied-bed value among the specialities reviewed.
- Staffing assignments were below plan across the three recorded roles. The data does not independently establish why those gaps occurred.
- The scenario-planning baseline showed approximately 75% occupancy, but averages across the hospital network can conceal local pressure.
  
**Capacity forecasting and scenario planning**
The second dashboard includes a 30-day occupancy forecast with a 95% confidence interval. The third uses interactive What-if parameters representing emergency spikes, flu-related surges and discharge delays.
With the controls set to zero, the documented baseline showed an average of 8.33 occupied beds and 11.15 staffed beds per occupancy observation, approximately 75% occupancy, 2.83 available beds and zero average bed shortfall. These values are observation-level averages, not totals across all 39 hospitals.
Forecasts and scenarios provide planning indicators, not guaranteed outcomes or clinical predictions.

**Strategic recommendations**
1. Plan ahead for winter demand: Review staffing and operational bed capacity before recurring seasonal peaks.
2. Investigate end-of-week patient flow: Examine discharge coordination, elective scheduling and weekend service arrangements around periods of higher occupancy.
3. Prioritise General Medicine for review: Investigate prolonged stays and potential discharge or transfer delays rather than assuming a single cause.
4. Align staffing with demand: Review shortfalls by hospital, ward, role and high-pressure period.
5. Record elective cancellation reasons: Add standardised reason categories; the existing dataset gives the cancellation rate but not its causes.
6. Use scenario testing routinely: Document assumptions, compare moderate and severe cases, and validate results before operational decisions.
   
**Limitations and next steps**
- The analysis used static data extracts, not a real-time hospital feed.
- Occupancy observations were periodic snapshots, not continuous patient-level bed movements.
- Operational datasets could be compared by shared dimensions but were not directly linked at patient level in all cases.
- Cancellation reasons were unavailable, so their causes cannot be established from this analysis.
- Scenario outputs depend on user assumptions; forecasts need holdout-period validation.
Potential next steps include automated refresh, forecast-accuracy monitoring, hospital-specific forecasts, stronger elective and emergency demand modelling, cancellation-reason analysis and operational alerts.

**Conclusion**
This project demonstrates how Power BI can integrate fragmented hospital operations data into a clearer decision-support view. Seasonal demand patterns, end-of-week occupancy pressure, lengthy General Medicine stays and gaps between planned and actual staffing all highlight areas where earlier investigation could improve planning.
The key lesson is that usable bed capacity depends on more than the number of physical beds: staffing, patient flow and discharge processes matter as well. Combining historical analysis, forecasting and interactive scenarios helps planners explore those pressures more systematically.

**Repository contents**
- README.md - project overview, methods, findings and recommendations (this page)
- ![Patient Flow Dashboard](Nexora%20Admission%20Overview%20Dashboard.png)
- ![Bed Capacity Dashboard](Nexora%20Bed%20Capacity%20Dashboard.png)
- ![Scenario Planning Dashboard](Nexora%20Capacity%20Scenario%20Dashboard.png)
- [Schema DIagram](Nexora%20Schema%20Diagram.png)
- [Nexora DAX Measures](Nexora_Care_DAX_Measure_Library_Final.xlsx
- [Nexora Methodology](Nexora_Care_Methodology_and_Final_Report%201.pdf)
