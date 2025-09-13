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

### 🔹 Step 1: Data Import  
- Dataset sourced from **Kaggle – Paris 2024 Olympic Summer Games**  
- Data fetched using **Python Kaggle API script**  
## Step 2 — Data Cleaning & Preprocessing (Python / Kaggle API)

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


