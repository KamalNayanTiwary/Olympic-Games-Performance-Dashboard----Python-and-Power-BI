# 🏅 Olympic Games Performance Dashboard  

📌 **Project Objective**  
To build a **comprehensive Olympic Games Analysis Dashboard**, powered by **Python Kaggle API integration**, with the goal of delivering **end-to-end visibility** into:  

- Athlete demographics & participation statistics  
- Medal distribution by country, gender, and medal type  
- Performance benchmarking of top-performing nations  
- Gender parity in Olympic achievements  
- Age distribution analysis of athletes  

The project provides **actionable insights** to sports analysts, committees, and stakeholders, enabling them to:  

✔ Track country performance across Olympic Games  
✔ Analyze gender representation in achievements  
✔ Monitor athlete demographics & participation trends  
✔ Support data-driven sports development strategies  

---

## 📊 Dashboard Overview  

I designed **3 Dashboards** for a complete analysis:  

---

### 1️⃣ COUNTRY PERFORMANCE Dashboard – **Medals & Global Comparison**  
![COUNTRY Dashboard](screenshots/Screenshot1.png)  

The **Country Performance Dashboard** acts as the **executive snapshot** of the Olympic medal distribution across countries. It is designed for analysts, journalists, and national Olympic committees to understand **which nations lead the medal tally**.  

📊 **Key Metrics Displayed:**  
- **World Map Visualization** → global medal distribution  
- **Bar Charts** → Medal counts by nation (Gold, Silver, Bronze)  
- **Gender Split of Medals** → Male vs Female medal share  
- **KPI Cards** → Total Medals, Total Golds, Total Silver, Total Bronze  

📌 **Business Value:**  
- Provides a **single-page global performance overview**  
- Highlights **dominant nations (USA, China, France, GB)**  
- Assists in **benchmarking national Olympic strategies**  
- Shows **gender-based medal representation**  

📌 **Sample Insights:**  
- **USA dominates** across all medal categories  
- **France & China** show strong competitive performance  
- Balanced **male vs female medal distribution** in top nations  

---

### 2️⃣ ATHLETE ANALYSIS Dashboard – **Demographics & Age Trends**  
![ATHLETE Dashboard](screenshots/Screenshot2.png)  

The **Athlete Dashboard** focuses on the **demographics of athletes** — gender, age, and country participation. It is designed to help sports scientists, coaches, and committees **understand athlete characteristics**.  

📊 **Visuals & Analysis:**  
- **Age Distribution Histogram** → Peak performance between **21–30 years**  
- **Gender Distribution Donut Chart** → Near parity (M: 50.9%, F: 49.1%)  
- **Country Participation Breakdown** → Male vs Female athletes by nation  
- **Medal KPIs by Gender** → Female athletes slightly outperform in Gold & Silver  

📌 **Business Value:**  
- Highlights the **prime age group** for Olympic participation  
- Shows **gender parity achievement** in Olympics  
- Provides data for **future talent scouting & training investment**  

📌 **Sample Insights:**  
- Female athletes **slightly outperform males** in Gold & Silver medals  
- Peak participation observed in **early to late 20s**  
- Veteran athletes (36+ years) also contribute to medal wins  

---

### 3️⃣ GEOGRAPHICAL Dashboard – **Global Medal Distribution**  
![GEO Dashboard](screenshots/Screenshot3.png)  

The **Geographical Dashboard** zooms into the **spatial distribution of Olympic medals**. It helps federations and policymakers analyze **regional strengths and weaknesses**.  

📊 **Visuals & Analysis:**  
- **World Medal Map** → Country-wise medal tally  
- **Top Nation Highlights (USA)** → KPIs for quick comparison  
- **Continental Trends** → Participation & performance segmentation  

📌 **Business Value:**  
- Helps in **regional benchmarking**  
- Identifies **continental dominance** (e.g., North America, Europe, Asia)  
- Assists in **sports development planning by geography**  

📌 **Sample Insights:**  
- **USA is far ahead globally**, followed by China & France  
- Europe shows **high participation with broad medal spread**  
- Asia’s rise visible with **China, Japan, Korea performing well**  

---

## 📌 Project Background  

The Olympic Games involve thousands of athletes, hundreds of events, and global participation. Stakeholders need **real-time, accurate, and insightful dashboards** to answer questions like:  

- *Which countries are dominating the medal tally?*  
- *What is the gender split in medal wins?*  
- *At what age do athletes typically achieve Olympic success?*  
- *How do different nations compare across games?*  

This project addresses these needs by integrating **Python-based Kaggle data extraction** with **Power BI visualizations**, creating an **interactive and professional Olympic Analysis Dashboard**.  

---

## ⚙️ Technical Process  

### 🔹Step 1 — Data Import  
- Dataset sourced from **Kaggle – Paris 2024 Olympic Summer Games**  
- Data fetched using **Python Kaggle API script**  
### 🔹Step 2 — Data Cleaning & Preprocessing (Python / Kaggle API)

**🎯 Goal:** Convert raw CSV files downloaded from Kaggle into analysis-ready tables (consistent country names, age groups, flags for medals, cleaned data types).

### ⚙️ Environment / Setup
Install required packages:
```bash
pip install pandas numpy kaggle
```
**📥 Download & unzip dataset**
```import kaggle, pandas as pd, os

os.environ['KAGGLE_CONFIG_DIR'] = 'C:/Users/faies/.kaggle'
dataset = 'ploterim/panic-2024-olympic-summer-games'
download_path = 'C:/Users/faies/Downloads/Power BI_Imp Summary/Olympic/Source'

# Clear older files
for f in os.listdir(download_path):
    p = os.path.join(download_path, f)
    if os.path.isfile(p): os.unlink(p)

# Download & unzip from Kaggle
kaggle.api.dataset_download_files(dataset, path=download_path, unzip=True)

# Load CSVs
csv_files = ['athletes.csv','events.csv','medals.csv','teams.csv','venues.csv']
dataFrames = {f.split('.')[0]: pd.read_csv(os.path.join(download_path,f)) for f in csv_files}
```
**🧹 Cleaning steps**
```# Trim whitespace, uniform case, remove duplicates
df['country'] = df['country'].str.strip()
df = df.drop_duplicates(subset=['athlete_id','event','year'])

# Convert datatypes
df['age'] = df['age'].astype(int)

# Create Age Groups
bins = [0,20,25,30,35,40,45,50,100]
labels = ['≤20','21-25','26-30','31-35','36-40','41-45','46-50','51+']
df['Age_Group'] = pd.cut(df['Age'], bins=bins, labels=labels)

# Boolean flags
df['Has_Medal'] = df['medal'].notnull()
```
**🔍 Validation**
```
# Check for nulls
print(df[['athlete_id','country','age','gender','medal']].isnull().sum())

# Count unique athletes vs rows*
total_athletes = df['athlete_id'].nunique()
total_rows = len(df)
print(total_athletes, total_rows)
```
**💾 Export**
```
df.to_csv(os.path.join(download_path,'athletes_clean.csv'), index=False)
```
---

### 🔹Step 3 — Power BI Integration (Load & Connect)

🎯 **Goal:** Bring cleaned tables into Power BI with reproducible, automatable flow.

---

### ⚙️ Options

1️⃣ **Python Step in Power Query**  
- Go to: `Home → Get Data → Other → Python Script`  
- Paste your Python script (dataFrames will be returned as tables directly in Power BI).  

```python
# Example Python script inside Power BI (Power Query)
import pandas as pd

# Load cleaned CSVs from local path
athletes = pd.read_csv("C:/Users/faies/Downloads/Power BI_Imp Summary/Olympic/Source/athletes_clean.csv")
medals   = pd.read_csv("C:/Users/faies/Downloads/Power BI_Imp Summary/Olympic/Source/medals.csv")

# Return DataFrames for Power BI
athletes, medals
```
**2️⃣ Import Cleaned CSVs**
Use: Home → Get Data → Text/CSV
Point to athletes_clean.csv, medals.csv, etc.
Power BI will automatically detect schema.

**✅ Best Practice: Create a dedicated Date Table in Power Query**
```
Date = CALENDAR (DATE(2000,1,1), DATE(2030,12,31))
Year = YEAR('Date'[Date])
Month = FORMAT('Date'[Date], "MMM")
Quarter = "Q" & FORMAT('Date'[Date], "Q")
```
---

### 🔹Step 4 — Data Modeling & DAX (Relationships & Measures)

**🎯 Goal:** Model as a star schema and create robust KPIs.

**⭐ Schema**
Fact Table: Medals/Participation (athlete-event rows)
Dimensions: Athletes, Countries, Events, Teams, Date
```
Fact[athlete_id] → Athletes[athlete_id]  
Fact[country] → Countries[country]  
```
**📊 DAX Measures**
```
Total Medals = COUNTROWS('Medals')
Total Golds  = CALCULATE([Total Medals],'Medals'[Medal] = "Gold")
Total Silvers= CALCULATE([Total Medals],'Medals'[Medal] = "Silver")
Total Bronzes= CALCULATE([Total Medals],'Medals'[Medal] = "Bronze")

Male Medals  = CALCULATE([Total Medals], 'Athletes'[Gender] = "M")
Female Medals= CALCULATE([Total Medals], 'Athletes'[Gender] = "F")

Female Gold % = DIVIDE(
    CALCULATE([Total Golds], 'Athletes'[Gender] = "F"),
    [Total Golds], 0
)
```
**📅 Date Intelligence**
```
Medals YTD = TOTALYTD([Total Medals], 'Date'[Date])
Medals PrevYear = CALCULATE([Total Medals], SAMEPERIODLASTYEAR('Date'[Date]))
```
---

### 🔹Step 5 — Dashboard Development (Design & UX)  
🎯 **Goal:** Create three professional and interactive pages with consistent design, layout, and color theme.

**Page 1 — Country Performance**
- **KPI Cards:** Total Athletes, Total Medals, Total Gold Medals  
- **Visualizations:** Country-wise medal tally, year-wise performance trend, top 10 countries comparison  
- **UX Focus:** Allow users to easily see which country performed best and how trends changed over time

**Page 2 — Athlete Analysis**
- **Visualizations:** Gender distribution, age distribution, sports-wise participation  
- **Insights:** Analyze male vs. female athlete participation and success across age groups  
- **UX Focus:** Interactive filters like “Sport” or “Year” for customized analysis

**Page 3 — Medal Insights**
- **Visualizations:** Medal distribution by type (Gold, Silver, Bronze), top-performing athletes, country contribution  
- **Insights:** Compare medal trends and top achievers  
- **UX Focus:** Maintain visual hierarchy, ensuring charts and KPIs are easy to read

---

### 🔹Step 6 — Data Modeling & Relationships  
🎯 **Goal:** Establish logical relationships between datasets in Power BI  

- Clean and transform data before creating relationships using **primary and foreign keys**  
- Implement **star schema design**: fact table for medals & dimension tables for country, athlete, and event  
- Validate relationships to ensure visuals are accurate and responsive

---

### 🔹Step 7 — DAX Calculations & KPIs  
🎯 **Goal:** Create custom measures and KPIs for deeper insights  

**Examples of DAX Measures:**  
- `Total Medals = SUM(Medals[Count])`  
- `Gold Medal Percentage = DIVIDE(SUM(Medals[Gold]), SUM(Medals[Total]))`  
- `Average Age = AVERAGE(Athletes[Age])`  

- Implement advanced calculations like Year-over-Year medal growth and gender parity index  
- Highlight KPIs using cards and conditional formatting for better readability

---

### 🔹Step 8 — Interactivity & Filters  
🎯 **Goal:** Make the dashboard interactive and user-friendly  

- Add **Slicers** for Year, Country, Sport, and Gender  
- Enable **Drill-through** and **Tooltips** for detailed insights  
- Use **conditional formatting** and dynamic visuals for easy trend detection  
- Ensure responsive design for different screen sizes

---

### 🔹Step 9 — Testing & Optimization  
🎯 **Goal:** Ensure the dashboard is accurate, responsive, and high-performing  

- Verify data refresh and calculations for correctness  
- Optimize performance by reducing unnecessary columns and using aggregation tables  
- Conduct cross-browser and device testing  
- Final review for visual alignment, color consistency, and readability

---

### 📊 Business Problems Solved

This dashboard provided **clear answers to critical business questions**:  
- Which countries dominate Olympic performance and how trends have evolved.  
- The state of **gender parity** in global sports achievements.  
- Age-group insights showing when athletes typically reach peak performance.  
- Regional disparities in medal distribution, useful for committees to **redirect focus and resources**.  

---

### 📌 Key Recommendations

Based on insights from the dashboard, several **strategic recommendations** were made:  
- Invest more in **women’s sports programs**, given the increasing success of female athletes.  
- Prioritize athlete development in the **21–30 age group**, as this is the performance peak.  
- Leverage **veteran athletes** in endurance and technical events for experience-driven results.  
- Benchmark and learn from **USA’s sports training systems and funding models** to improve long-term performance.  

---

### 🛠 Tech Stack

- 🐍 **Python (Pandas, Kaggle API)** → Data extraction and preprocessing  
- 📊 **Power BI** → Data visualization and interactive dashboarding  
- ➗ **DAX** → Calculated measures and KPIs  
- 📑 **Excel** → Cross-validation of data and manual checks  

---

### 🚀 Future Enhancements

The project can be extended with advanced features such as:  
- **Predictive medal forecasting** using machine learning models.  
- Integration of **real-time API refresh** for live Olympic updates.  
- Expansion of dataset to cover **historical Olympic Games (2000–2024)** for trend analysis.  
- Development of **role-based dashboards** tailored for Coaches, Committees, and Sponsors.  

---
