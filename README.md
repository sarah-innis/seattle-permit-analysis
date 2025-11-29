# **Analyzing New Residential Construction in the City of Seattle**

This project explores new residential construction in the City of Seattle to answer:

* How is the housing supply changing within Seattle?
* Where is new housing being added?
* Are Seattle City Council Districts impacted differently by housing additions?
* As the population grows, how do we expect the number of large multifamily buildings per resident to change?

The goal is to understand how Seattle’s Council Districts are experiencing densification and whether multifamily housing availability per resident is declining—informing key action areas in the Seattle housing crisis.

---

# **Data Sources**

All datasets are from federal sources or the Seattle Open Data Portal and are Public Domain. See `LICENSE.txt` for details.

---

## **1. Building Permit Data**

**File:** `Building_Permits_20251106.csv`
**Source:** Seattle City Open Data
**URL:** [https://data.seattle.gov/Built-Environment/Building-Permits/76t5-zqzr/about_data](https://data.seattle.gov/Built-Environment/Building-Permits/76t5-zqzr/about_data)

### **Fields**

* **PermitNum (text):** Unique permit number
* **PermitClass (text):** Project type (e.g., Single Family/Duplex, Commercial, Multifamily)
* **PermitClassMapped (text):** Residential or Non-Residential
* **PermitTypeMapped (text):** Permit category (Building, Demolition, Grading, etc.)
* **PermitTypeDesc (text):** Additional permit type detail (e.g., addition/alteration)
* **Description (text):** Free-text description of project
* **HousingUnits (number):** Units at start of project
* **HousingUnitsRemoved (number):** Units removed
* **HousingUnitsAdded (number):** Units added
* **EstProjectCost (number):** Estimated cost (parts + labor)
* **AppliedDate (timestamp):** Application accepted date
* **IssuedDate (timestamp):** Permit issuance date
* **ExpiresDate (timestamp):** Permit expiration date
* **CompletedDate (timestamp):** Date all inspections completed
* **StatusCurrent (text):** Most recent completed process step (≈20 values)
* **RelatedMup (text):** Related land-use permit
* **OriginalAddress1 / City / State / Zip (text):** Project location
* **ContractorCompanyName (text):** Contractors associated with permit
* **Link (URL):** Permit details online
* **Latitude / Longitude (number):** Location coordinates
* **Location1 (location):** Mapped location
* **TotalDaysPlanReview (number):** Days from application to completion of plan review
* **DaysInitialPlanReview (number):** Days until initial plan review completed
* **DaysPlanReviewCity (number):** Days until all plan reviews completed
* **DaysOutCorrections (number):** Days applicant spent correcting issues
* **NumberReviewCycles (number):** Number of review cycles
* **InitialReviewCompleteDate (timestamp):** Initial review completion
* **PlanReviewCompleteDate (timestamp):** All plan reviews completed
* **DaysIssuePermitCity (number):** Days between application and issuance
* **ReadyToIssueDate (timestamp):** City ready-to-issue date
* **Zoning (text):** Zoning code at parcel
* **DwellingUnitType (text):** Type of housing built
* **StandardPlan (text):** Whether a pre-approved DADU plan was used
* **DependentBuilding (text):** Whether dependent on another permit
* **ParentPermitNum (text):** Parent permit number
* **HousingCategory (text):** Housing type created

---

## **2. Seattle City Council Districts**

**Folder:** `council_districts/`
**Source:** Seattle City Open Data
**URL:** [https://data-seattlecitygis.opendata.arcgis.com/datasets/SeattleCityGIS::city-of-seattle-council-districts-2024-redistricting-data-2000-2020/explore](https://data-seattlecitygis.opendata.arcgis.com/datasets/SeattleCityGIS::city-of-seattle-council-districts-2024-redistricting-data-2000-2020/explore)

### **Core Fields**

* **COUNCIL_DI (category):** Council district ID
* **AREA_ACRES (float):** Area in acres
* **AREA_SQMI (float):** Area in square miles
* **DISPLAY_NA (text):** Display name
* **geometry (geometry):** District polygon

---

### **Census & Redistricting Fields**

These fields encode census population and land data for 2000, 2010, and 2020.
Field names follow the structure:

```
FYYYY_<CODE>
```

Where **YYYY** is the census year (2000, 2010, 2020) and **CODE** is a shared variable identifier.

---

#### **Population & Land (PL) Aggregations**

Each PL variable appears in the years listed below.

| Variable | Description                    | Years Available  |
| -------- | ------------------------------ | ---------------- |
| **PL_d** | Population & land category “d” | 2000, 2010, 2020 |
| **PL_1** | PL category 1                  | 2000, 2010, 2020 |
| **PL_2** | PL category 2                  | 2000, 2010, 2020 |
| **PL_3** | PL category 3                  | 2000, 2010, 2020 |
| **PL_4** | PL category 4                  | 2000, 2010, 2020 |
| **PL_5** | PL category 5                  | 2000             |
| **PL_6** | PL category 6                  | 2000             |
| **PL_7** | PL category 7                  | 2000             |
| **PL_8** | PL category 8                  | 2000             |
| **PL_9** | PL category 9                  | 2000             |
| **PL_T** | PL total                       | 2000             |
| **PL_P** | PL population                  | 2000             |
| **PL_W** | PL W category                  | 2000             |
| **PL_B** | PL B category                  | 2000             |
| **PL_A** | PL A category                  | 2000             |
| **PL_O** | PL O category                  | 2000             |
| **PL_H** | PL H category                  | 2000             |
| **PL_N** | PL N category                  | 2000             |
| **PL_M** | PL M category                  | 2000             |
| **PL_U** | PL U category                  | 2000             |

---

#### **Population (P) Variables**

##### **Variables available across all years (2000, 2010, 2020)**

| Variable | Description           | Years Available  |
| -------- | --------------------- | ---------------- |
| **P_10** | Population measure 10 | 2000, 2010, 2020 |
| **P_11** | Population measure 11 | 2000, 2010, 2020 |
| **P_12** | Population measure 12 | 2000, 2010, 2020 |
| **P_13** | Population measure 13 | 2000, 2010, 2020 |
| **P_14** | Population measure 14 | 2000, 2010, 2020 |
| **P_15** | Population measure 15 | 2000, 2010, 2020 |
| **P_16** | Population measure 16 | 2000, 2010, 2020 |

##### **Variables available for 2010 and 2020 only**

| Variable | Description           | Years Available |
| -------- | --------------------- | --------------- |
| **P_17** | Population measure 17 | 2010, 2020      |
| **P_18** | Population measure 18 | 2010, 2020      |
| **P_19** | Population measure 19 | 2010, 2020      |
| **P_20** | Population measure 20 | 2010, 2020      |
| **P_21** | Population measure 21 | 2010, 2020      |
| **P_22** | Population measure 22 | 2010, 2020      |
| **P_23** | Population measure 23 | 2010, 2020      |
| **P_24** | Population measure 24 | 2010, 2020      |
| **P_25** | Population measure 25 | 2010, 2020      |
| **P_26** | Population measure 26 | 2010, 2020      |

---

## **3. Population Forecast Data**

**File:** `Pop_Interest_Per_Year.xlsx`
**Source:** City of Seattle Office of Economic & Revenue Forecasts
**URL:** [https://view.officeapps.live.com/op/view.aspx?src=https%3A%2F%2Fwww.seattle.gov%2Fdocuments%2FDepartments%2FOERF%2FForecasts%2F2025%2FOERF_EcoForecast_KS_2025Q4_202510%25202025-10-11.xlsx&wdOrigin=BROWSELINK](https://view.officeapps.live.com/op/view.aspx?src=https%3A%2F%2Fwww.seattle.gov%2Fdocuments%2FDepartments%2FOERF%2FForecasts%2F2025%2FOERF_EcoForecast_KS_2025Q4_202510%25202025-10-11.xlsx&wdOrigin=BROWSELINK)

### **Fields**

* **Year (integer):** Calendar year
* **Population (integer):** Population of Snohomish + King County

---

## **4. Interest Rate Data**

**File:** `Pop_Interest_Per_Year.xlsx`
**Source:** Board of Governors of the Federal Reserve System (US), Federal Funds Effective Rate [FEDFUNDS], retrieved from FRED, Federal Reserve Bank of St. Louis; https://fred.stlouisfed.org/series/FEDFUNDS, November 19, 2025.
**URL:** [https://fred.stlouisfed.org/series/FEDFUNDS](https://fred.stlouisfed.org/series/FEDFUNDS)

### **Fields**

* **Year (integer):** Calendar year
* **Interest Rate (float):** Federal Funds Effective Rate
