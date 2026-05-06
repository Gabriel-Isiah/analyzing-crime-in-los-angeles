#LA Crime Data Analysis — LAPD EDA Project

An exploratory data analysis of Los Angeles crime data, built on a DataCamp project and extended with additional personal EDA, visualizations, and written interpretations.

---

##  Project Overview

This project analyzes real crime data from the Los Angeles Police Department (LAPD), sourced from [LA Open Data](https://data.lacity.org/). The goal was to uncover patterns in criminal behavior across time, location, age group, and crime type — insights that could help law enforcement allocate resources more effectively.

The DataCamp-guided portion focused on answering three structured analytical questions. I extended the project with my own exploratory analysis, covering victim demographics, crime type frequency, area-level patterns, and weapon usage.

---

##  Dataset

**File:** `crimes.csv`

| Column | Description |
|---|---|
| `DR_NO` | Official file number (year + area ID + sequence) |
| `Date Rptd` | Date the crime was reported |
| `DATE OCC` | Date the crime occurred |
| `TIME OCC` | Time in 24-hour military format |
| `AREA NAME` | LAPD patrol division name |
| `Crm Cd Desc` | Crime type description |
| `Vict Age` | Victim age in years |
| `Vict Sex` | Victim sex (F/M/X) |
| `Vict Descent` | Victim ethnicity/descent code |
| `Weapon Desc` | Weapon used (if applicable) |
| `Status Desc` | Case status |
| `LOCATION` | Street address of incident |

---

##  Analysis Breakdown

### Data Preparation
- Loaded the dataset with `TIME OCC` forced to string type to preserve leading zeros
- Inspected shape, data types, null counts, and cardinality across all columns
- Converted `DATE OCC` and `Date Rptd` from object to datetime
- Converted `Vict Age` from object to integer
- Parsed `TIME OCC` into separate `Hour` and `Minute` integer columns for time-based analysis

### My Own EDA (Extended)

**Victim Age Distribution**
Plotted a histogram of victim ages and noted that younger adults are overrepresented in reported incidents — likely reflecting a mix of exposure patterns, population structure, and reporting behavior rather than raw risk alone.

**Top Crime Types**
Filtered to the 10 most frequent crime categories and visualized with a horizontal bar chart. Identity theft ranked as the most reported offense, followed by simple assault and vehicle burglary — suggesting the dataset skews heavily toward non-violent and property crimes.

**Crime by Area**
Ranked all 21 LAPD patrol divisions by incident count. Central division recorded the highest number of reports, followed by Southwest and 77th Street.

**Weapon Usage**
Analyzed the top 10 weapon descriptions. "Strong-arm" (physical force without a weapon) was the most common entry, followed by "unknown weapon" and "verbal threat" — indicating many incidents either don't involve a weapon or have incomplete reporting.

### DataCamp Questions Answered

| Question | Finding |
|---|---|
| Peak crime hour? | **12 PM (noon)** — `peak_crime_hour = 12` |
| Area with most night crimes (10 PM–4 AM)? | **Central** — `peak_night_crime_location = "Central"` |
| Crime frequency by victim age group? | **18–25 and 26–34** had the highest counts — stored as `victim_ages` Series |

---

## Skills Demonstrated

- **Data cleaning** — type conversion, string parsing, null inspection
- **Feature engineering** — extracting hour/minute from military time strings, binning ages into labeled groups with `pd.cut()`
- **Exploratory data analysis** — distribution analysis, frequency ranking, time-based and geographic segmentation
- **Data visualization** — histograms, count plots, and bar charts using `seaborn` and `matplotlib`
- **Written interpretation** — explaining what each chart shows and what caveats apply (e.g., reporting bias vs. actual risk)
- **Pandas** — `value_counts()`, `loc[]` filtering, `idxmax()`, `sort_index()`, `astype()`, `pd.to_datetime()`

---

## What I Learned

- How to handle mixed-type columns (like time stored as a zero-padded string) correctly at load time
- How to use `pd.cut()` with custom bins and labels to create meaningful age group categories
- That visualizing "weapon used" requires filtering to top-N first — otherwise the chart is unreadable
- The importance of adding interpretive commentary alongside charts, especially noting when findings might reflect reporting artifacts rather than ground truth
- How nighttime crime patterns can differ from overall patterns by area — useful for resource allocation problems

---

## Libraries Used

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

---

*Dataset provided by DataCamp, originally sourced from [Los Angeles Open Data](https://data.lacity.org/).*