## ⚙️ Execution Steps


1.Run the Data Integration and Cleaning File in the Additional Data folder. It requires three inputs.
1)Kaggle Railways Data(from common dataset) 2) Geocodes(from common dataset) 3) Census Data ( from Additional Data Folder). 

2.The output is generated in both .gpkg and .csv format (uncomment if necessary)

3.The output(.gpkg) would be used by Railway Desert Indicator file to do the main modeling.

----------------------------------------------------------------------------------------------------------------------------------------------------------

# 🚆 Railway Accessibility Analysis in India

## 📌 Overview
This project analyzes railway accessibility across India using a data-driven approach. We construct a **Railway Access Score (RAS)** to measure how well each station is served relative to its expected service level, accounting for infrastructure, demand, development, and social vulnerability.

The goal is to identify **under-served regions ("railway deserts")** and understand how accessibility aligns with socio-economic need.

---

## 🎯 Objectives
- Measure railway accessibility at the station level
- Adjust for structural and socio-economic factors using statistical modeling
- Identify regions that are over- or under-served relative to expectations
- Incorporate equity considerations using a Social Vulnerability Index (SVI)

---

## 🧠 Methodology

### 1. Data Integration
We combine multiple datasets:
- Indian Railways dataset (train frequency, station info)
- Census data (demographics, workforce, literacy)
- GDP/productivity data
- Geographic shapefiles for district mapping
- SHRUG dataset for socio-economic indicators

---

### 2. Feature Engineering
Key variables constructed:
- `unique_trains`: number of distinct trains per station (response)
- `terminal_count`: network centrality
- `efficiency_index`: service quality proxy
- `hr_index`: development index (PCA)
- `SVI`: Social Vulnerability Index (PCA)

---

### 3. Modeling
We use a **Negative Binomial GLM** to model train counts:

log(𝜇𝑖 )= 𝛽0 +x⊤
𝑖 𝜷 +log(Population𝑖 +1)

Three models were tested:
- **Model 1**: Infrastructure + Development  
- **Model 2**: + Demand  
- **Model 3**: + Social Vulnerability (final model)

Model selection was based on **10-fold cross-validation**.

---

### 4. Railway Access Score (RAS)

We compute a model-adjusted accessibility score:

\[
RAS_i = \log\left(\frac{y_i}{\hat{\lambda}_i}\right)
\]

Then convert to percentile:

\[
RASrank_i = \frac{\text{rank}(r_i)}{n}
\]

- Higher RAS → better service than expected  
- Lower RAS → under-served relative to context  

---

## 📊 Key Results
- Infrastructure is the strongest driver of accessibility  
- Development significantly improves access  
- Social vulnerability shows a meaningful but weaker effect  
- Model 3 performs best (lowest prediction error)  
- Strong regional disparities persist even after controls  

---

## 🗺️ Visualizations
- District-level RAS choropleth
- SVI vs RAS quadrant classification
- Model comparison tables

---

## ⚠️ Limitations
- District-level aggregation hides local variation  
- Data is ~15 years old  
- Possible endogeneity between access and development  
- Proxy variables used for demand and vulnerability  

---

## 🔮 Future Work
- Use updated census and mobility data  
- Compute RAS at finer spatial granularity  
- Incorporate passenger flow / ticketing data  
- Build composite RAS from multiple approaches  

---

## 🛠️ Tech Stack
- Python (pandas, numpy, statsmodels)
- GeoPandas (spatial analysis)
- Matplotlib / Seaborn (visualization)
- Scikit-learn (PCA, cross-validation)

---

