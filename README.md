# Employee Project Analytics & Data Cleaning Pipeline

*A Python data analysis project demonstrating data wrangling, cleaning, and business analytics on employee-project datasets*

## 📋 Project Overview

**Business Context:**
An organization manages multiple projects across employees of varying seniority levels and geographic locations. The challenge was to consolidate data from disparate sources, handle missing values intelligently, and extract actionable business insights about project costs, employee performance, and compensation analysis.

**Solution:**
I built a comprehensive data pipeline that cleans messy datasets, handles missing values using domain-aware imputation techniques, integrates multiple data sources, and performs exploratory analysis to answer key business questions.

## 🎯 Key Deliverables & Findings

| Finding | Impact | Business Implication |
|---------|--------|---------------------|
| Missing Cost Values | Recovered using moving average imputation | Enabled accurate project cost tracking |
| Employee-Project Mapping | Consolidated 3 data sources into unified dataset | Single source of truth for project allocation |
| Bonus Analysis | Identified bonus distribution by designation & project success | Optimized compensation structure |
| Geographic Distribution | Mapped 5 employees across 5 international cities | Insights for remote work strategy |

**Key Statistics:**
- **Total Projects Analyzed**: 14 projects
- **Total Employees**: 5 (Designation levels: 2 or 3)
- **Geographic Spread**: 5 countries (Paris, London, Berlin, New York, Madrid)
- **Project Status Breakdown**: 8 Finished, 3 Ongoing, 3 Failed
- **Total Project Cost**: ₹26.27M (before imputation)

## 🔧 Methodology & Technical Approach

### 1. Data Consolidation
Created three source dataframes:
- **Project DataFrame**: 14 projects with ID, Name, Cost (with missing values), and Status
- **Employee DataFrame**: 5 employees with demographic information (ID, Name, Gender, City, Age)
- **Seniority DataFrame**: Employee designation levels (2-3 scale indicating seniority)

### 2. Data Cleaning & Missing Value Treatment
**Challenge**: Two missing cost values in the project dataset
**Technique**: Running/Moving Average Imputation
```python
# Applied moving average to fill missing cost values
project_data['Cost'] = project_data.groupby('ID')['Cost'].transform(
    lambda x: x.fillna(x.rolling(window=2, min_periods=1).mean())
)
