# COVID-19 Data Visualizations

**Project:** COVID-19 — 10 Visualizations using Matplotlib & Seaborn  
**Author:** Kinjal Luhar  

---

## 📌 Project Overview
This repository contains a Jupyter Notebook that builds **10 distinct visualizations** from a COVID-19 dataset (country-wise data).  
Each plot includes:
- **What it shows**
- **Why it’s useful**
- **Insights** from the visualization  

Screenshots of each plot are saved inside the `Graph_Screenshots/` folder and linked below.  

Dataset source: https://www.kaggle.com/datasets/imdevskp/corona-virus-report
 

---

## 📂 Files in Repository
- `covid_visualization.ipynb` → Jupyter Notebook with code & plots  
- `country_wise_latest.csv` → Dataset file  
- `Graph_Screenshots/` → Folder containing saved screenshots of all graphs  
- `requirements.txt` → Python libraries required  
- `README.md` → Project documentation  

---

## 📊 Plot Index (10 Visualizations)

Below each plot you will find: Purpose, Code snippet, Insight, and Screenshot.

---

### 01 — Top 10 Countries by Confirmed Cases (Bar Plot)
**Purpose:** Show which countries have the highest confirmed cases.  
**Insight:** Confirms global hotspots like USA, India, Brazil, etc.  

```python
top10_confirmed = df.nlargest(10, 'Confirmed')
plt.figure(figsize=(10,6))
sns.barplot(data=top10_confirmed, x="Confirmed", y="Country/Region", palette="Reds_r")
plt.title("Top 10 Countries by Confirmed Cases")
plt.savefig("Graph_Screenshots/01_top10_confirmed.png")
plt.show()
```

![Uploading 01_top10_confirmed.png…]()

---

### 02 — Top 10 Countries by Deaths (Bar Plot)
**Purpose:** Compare fatality counts across countries.  
**Insight:** Highlights the worst-affected countries in terms of deaths.  

```python
top10_deaths = df.nlargest(10, 'Deaths')
plt.figure(figsize=(10,6))
sns.barplot(data=top10_deaths, x="Deaths", y="Country/Region", palette="Greys_r")
plt.title("Top 10 Countries by Deaths")
plt.savefig("Graph_Screenshots/02_top10_deaths.png")
plt.show()
```
<img width="1000" height="600" alt="02_top10_deaths" src="https://github.com/user-attachments/assets/a524e7d5-2789-4371-b32d-9ee06ec0de96" />

---

### 03 — Distribution of Confirmed Cases (Histogram)
**Purpose:** See how cases are distributed across all countries.  
**Insight:** Shows skewness — majority countries have low counts, few have very high.  
```python
plt.figure(figsize=(8,6))
sns.scatterplot(data=df, x="Confirmed", y="Deaths", size="Confirmed", hue="Deaths", alpha=0.6, palette="viridis")
plt.title("Confirmed vs Deaths (Country-wise)")
plt.savefig("Graph_Screenshots/03_confirmed_vs_deaths.png")
plt.show()

```
<img width="800" height="600" alt="03_confirmed_vs_deaths" src="https://github.com/user-attachments/assets/836b333c-4bf8-426f-9a18-2ab180d468a5" />

---

### 04 — Distribution of Deaths (Histogram)
**Purpose:** Understand spread of deaths per country.  
**Insight:** Few countries contribute to the majority of global deaths.  
```python
plt.figure(figsize=(8,6))
sns.histplot(df["Confirmed"], bins=40, kde=True, color="blue")
plt.title("Distribution of Confirmed Cases")
plt.savefig("Graph_Screenshots/04_distribution_confirmed.png")
plt.show()
```
<img width="800" height="600" alt="04_distribution_confirmed" src="https://github.com/user-attachments/assets/fc96f02b-c461-444a-8bb4-b6ab77525e47" />

---

### 05 — Confirmed vs Deaths (Scatter Plot)
**Purpose:** Relationship between confirmed cases and deaths.  
**Insight:** Clear positive correlation (more cases → more deaths).  
```python
plt.figure(figsize=(8,6))
sns.histplot(df["Deaths"], bins=40, kde=True, color="red")
plt.title("Distribution of Deaths")
plt.savefig("Graph_Screenshots/05_distribution_deaths.png")
plt.show()

```
<img width="800" height="600" alt="05_distribution_deaths" src="https://github.com/user-attachments/assets/cf46b417-ca17-4c74-af17-5d87f3f55bed" />

---

### 06 — Active vs Confirmed (Joint/Regression Plot)
**Purpose:** Check trend between active cases and total confirmed.  
**Insight:** Larger outbreaks maintain high active cases.  
```python
plt.figure(figsize=(8,6))
sns.boxplot(y=df["WHO Region"], x=df["Deaths"]/df["Confirmed"]*100, palette="coolwarm")
plt.title("Case Fatality Rate (%) by WHO Region")
plt.xlabel("Fatality Rate (%)")
plt.savefig("Graph_Screenshots/06_fatality_rate.png")
plt.show()

```

<img width="800" height="600" alt="06_fatality_rate" src="https://github.com/user-attachments/assets/70b5e12a-3961-4078-9d01-1658ec99a5c7" />

---

### 07 — Case Fatality Rate by WHO Region (Box Plot)
**Purpose:** Compare fatality rates across WHO regions.  
**Insight:** Some regions show higher variability and outliers.  
```python
df["Recovery Rate"] = df["Recovered"] / df["Confirmed"] * 100
plt.figure(figsize=(8,6))
sns.violinplot(x="WHO Region", y="Recovery Rate", data=df, palette="Set2")
plt.title("Recovery Rate by WHO Region")
plt.savefig("Graph_Screenshots/07_recovery_rate.png")
plt.show()

```
<img width="800" height="600" alt="07_recovery_rate" src="https://github.com/user-attachments/assets/8d46cdc1-199a-40b6-8bfd-1d4863238bb6" />

---

### 08 — Recovery Rate by WHO Region (Violin Plot)
**Purpose:** Visualize density of recovery rates by region.  
**Insight:** Regions differ in recovery efficiency.  
```python
plt.figure(figsize=(6,4))
sns.heatmap(df[["Confirmed","Deaths","Recovered","Active"]].corr(), annot=True, cmap="Blues")
plt.title("Correlation Heatmap")
plt.savefig("Graph_Screenshots/08_correlation_heatmap.png")
plt.show()

```
<img width="600" height="400" alt="08_correlation_heatmap" src="https://github.com/user-attachments/assets/eba60137-df55-493b-aca8-4d3e1cb28eda" />

---

### 09 — Correlation Heatmap
**Purpose:** Show correlation between confirmed, deaths, recovered, and active cases.  
**Insight:** Confirmed is strongly correlated with deaths and recovered.  
```python
sns.jointplot(data=df, x="Confirmed", y="Active", kind="reg", height=7, color="green")
plt.savefig("Graph_Screenshots/09_active_vs_confirmed.png")
plt.show()

```
<img width="700" height="700" alt="09_active_vs_confirmed" src="https://github.com/user-attachments/assets/506a32ad-8a19-41cb-b56d-56799b6dc13d" />

---

### 10 — Top 5 Countries (Stacked Bar Plot)
**Purpose:** Compare Confirmed, Deaths, Active, and Recovered for top countries.  
**Insight:** Quick multi-metric comparison across global hotspots.  
```python
top5 = df.nlargest(5, 'Confirmed')
top5.set_index("Country/Region")[["Confirmed","Deaths","Recovered","Active"]].plot(kind="bar", figsize=(10,6))
plt.title("Top 5 Countries: Confirmed, Deaths, Recovered, Active")
plt.savefig("Graph_Screenshots/10_top5_comparison.png")
plt.show()

```
<img width="1000" height="600" alt="10_top5_comparison" src="https://github.com/user-attachments/assets/99610199-a035-4d10-9c48-652d9813906b" />

---

## ⚙️ Requirements
Install dependencies using:
  pip install -r requirements.txt

📌 Closing Notes

This project demonstrates how data visualization can uncover meaningful insights from COVID-19 data.
The plots show global trends, correlations, and regional comparisons that highlight the pandemic’s impact.
