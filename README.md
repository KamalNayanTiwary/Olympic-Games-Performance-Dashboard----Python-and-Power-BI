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

### 🔹 Step 2: Python Script (Data Extraction & Cleaning)  

```python
import kaggle
import pandas as pd
import os

os.environ['KAGGLE_CONFIG_DIR'] = 'C:/Users/faies/.kaggle'
dataset = 'ploterim/panic-2024-olympic-summer-games'
download_path = 'C:/Users/faies/Downloads/Olympic/Source'

# Clear old files
for file in os.listdir(download_path):
    file_path = os.path.join(download_path, file)
    if os.path.isfile(file_path):
        os.unlink(file_path)

# Download fresh dataset
kaggle.api.dataset_download_files(dataset, path=download_path, unzip=True)

csv_files = ['athletes.csv','events.csv','medals.csv','teams.csv','venues.csv']
dataFrames = {}
for file in csv_files:
    df = pd.read_csv(os.path.join(download_path, file))
    dataFrames[file.split('.')[0]] = df
➡️ Ensures latest Kaggle data is always synced with Power BI
```

🔹 Step 3: Power BI Integration

Data loaded into Power BI Desktop

Relationships modeled across Athletes, Events, Medals, Teams

KPIs & calculated columns created with DAX

🔹 Step 4: Dashboard Development

Page 1 → Country Performance

Page 2 → Athlete Analysis

Page 3 → Geographical Overview

Added filters & slicers for interactivity

🔹 Step 5: Validation

Cross-checked medal counts with official Olympic statistics

Ensured data accuracy & consistency

🚨 Business Problems Solved

Identified dominant countries in Olympic performance

Measured gender parity in sports achievements

Analyzed age distribution trends of medal winners

Provided regional insights for national sports committees

🔎 Insights & Recommendations
📌 Sports Development Strategy

Invest more in women’s sports programs (female athletes showing strong results)

Focus on youth training academies → athletes peak in their 20s

Utilize veteran experience in technical/endurance sports

📌 Policy & Investment

Benchmark against USA’s sports programs & investments

Strengthen funding for underrepresented regions

Promote grassroots development in Asia & Africa

📌 Talent Scouting

Scout talent in 21–30 years bracket

Identify countries with low medal count → potential for growth with proper support

📄 Olympic Games Report

The Olympic Games are more than sports — they represent global unity, competition, and excellence. However, with thousands of athletes and hundreds of events, data analysis is crucial to uncover insights.

This Olympic Dashboard was built to:

Track global medal distribution

Monitor country-level performance

Evaluate gender balance in medal wins

Analyze athlete demographics & age trends

📊 By consolidating these insights into interactive dashboards, Olympic committees and analysts can make data-driven strategic decisions.

🛠️ Tech Stack

Python (Pandas, Kaggle API) – Data import & preparation

Power BI Desktop – Visualization & dashboards

DAX – Custom KPIs & calculations

Excel – Validation checks

🚀 Future Improvements

Add predictive analysis → Which country may dominate next Olympics

Build real-time Power BI Service refresh with API integration

Incorporate athlete-level performance stats (records, personal bests)

Expand dataset → Include historical Olympic Games (2000–2024)

👨‍💻 Author & Contact

Kamal Nayan Tiwary
Data Analyst | Power BI & Python Enthusiast

📧 kamalnayantiwary73@gmail.com

🔗 LinkedIn


---
