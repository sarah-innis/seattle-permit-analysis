# **Analyzing New Residential Multifamily Construction in the City of Seattle**

This project explores new residential multfamily construction in the City of Seattle to answer:

* How is the multifamily housing supply changing within Seattle?
* Where are new multifamily housing being added?
* Are Seattle City Council Districts impacted differently by multifamily housing additions?
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

Where **YYYY** is the census year (2000, 2010, 2020) and **CODE** is a shared variable identifier. Variable identifiers are described below.

---
### **Population & Land (PL) Aggregations**

Each PL variable appears in the years listed below.

| Variable | Description                                      | Years Available  |
| -------- | ------------------------------------------------ | ---------------- |
| **PL_d** | Total Population                                 | 2000, 2010, 2020 |
| **PL_1** | One Race                                         | 2000, 2010, 2020 |
| **PL_2** | White Alone                                      | 2000, 2010, 2020 |
| **PL_3** | Black or African American Alone                  | 2000, 2010, 2020 |
| **PL_4** | American Indian and Alaska Native Alone          | 2000, 2010, 2020 |
| **PL_5** | Asian Alone                                      | 2000             |
| **PL_6** | Native Hawaiian and Other Pacific Islander Alone | 2000             |
| **PL_7** | Some Other Race Alone                            | 2000             |
| **PL_8** | Two or More Races                                | 2000             |
| **PL_9** | Hispanic or Latino                               | 2000             |
| **PL_T** | PL total                                         | 2000             |
| **PL_P** | One Race                                         | 2000             |
| **PL_W** | White Alone                                      | 2000             |
| **PL_B** | Black or African American Alone                  | 2000             |
| **PL_A** | American Indian and Alaska Native Alone          | 2000             |
| **PL_O** | Asian Alone                                      | 2000             |
| **PL_H** | Native Hawaiian and Other Pacific Islander Alone | 2000             |
| **PL_N** | Some Other Race Alone                            | 2000             |
| **PL_M** | Two or More Races                                | 2000             |
| **PL_U** | Hispanic or Latino                               | 2000             |

---

### **Population (P) Variables**

#### **Variables available across all years (2000, 2010, 2020)**

| Variable | Description                                                       | Years Available  |
| -------- | ----------------------------------------------------------------- | ---------------- |
| **P_10** | Not Hispanic or Latino                                            | 2000, 2010, 2020 |
| **P_11** | White Not Hispanic or Latino                                      | 2000, 2010, 2020 |
| **P_12** | Black or African American Not Hispanic or Latino                  | 2000, 2010, 2020 |
| **P_13** | American Indian and Alaska Native Not Hispanic or Latino          | 2000, 2010, 2020 |
| **P_14** | Asian Not Hispanic or Latino                                      | 2000, 2010, 2020 |
| **P_15** | Native Hawaiian and Other Pacific Islander Not Hispanic or Latino | 2000, 2010, 2020 |
| **P_16** | Some Other Race Not Hispanic or Latino                            | 2000, 2010, 2020 |

#### **Variables available for 2010 and 2020 only**

| Variable | Description                                 | Years Available |
| -------- | ------------------------------------------- | --------------- |
| **P_17** | Two or More Races Not Hispanic or Latino    | 2010, 2020      |
| **P_18** | Persons of Color                            | 2010, 2020      |
| **P_19** | 18 years and over                           | 2010, 2020      |
| **P_20** | Under 18 years                              | 2010, 2020      |
| **P_21** | Persons of color under 18 years             | 2010, 2020      |
| **P_22** | Housing units                               | 2010, 2020      |
| **P_23** | Housing units occupied                      | 2010, 2020      |
| **P_24** | Housing units vacant                        | 2010, 2020      |
| **P_25** | Group Quarters Institutional Population     | 2010, 2020      |
| **P_26** | Group Quarters Non-Institutional Population | 2010, 2020      |

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

### **Fields**

* **Year (integer):** Calendar year
* **Interest Rate (float):** Federal Funds Effective Rate
