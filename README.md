

# Air Quality & Respiratory Health Analysis

This project explores the impact of air quality indicators on respiratory health outcomes using real-world data. We combine environmental data such as AQI, PM2.5, NO₂, and SO₂ with public health metrics like hospital visits and respiratory admissions to extract insights and patterns through data visualization, clustering, and statistical correlation.

---

## Project Overview

* **Dataset**: Includes columns like AQI, PM2.5, NO₂, SO₂, mask usage rate, hospital visits, mobility index, and respiratory admissions.
* **Objective**: Understand how air pollution and mobility influence respiratory health and group areas with similar environmental-health profiles.

---

## Key Analyses

### Correlation Analysis

* Weak correlation between mask usage rate and respiratory admissions.
* AQI and respiratory admissions show a slight inverse correlation.

### Q-Cut Grouping

```python
df['admission_group'] = pd.qcut(df['respiratory_admissions'], q=2, labels=['Low', 'High'])
df.groupby('admission_group')[['AQI', 'PM2.5', 'NO2', 'SO2']].mean()
```

* Compares mean pollution levels in areas with high vs. low respiratory admissions.

### Visualizations

* **Scatter plots** of mask usage vs respiratory admissions, colored by AQI.
* **Pairplot** showing clustering behavior in air-health variables.

### Clustering

```python
from sklearn.cluster import KMeans
from sklearn.preprocessing import StandardScaler

features = ['AQI', 'PM2.5', 'mobility_index', 'hospital_visits']
X_scaled = StandardScaler().fit_transform(df[features])

kmeans = KMeans(n_clusters=3, random_state=0).fit(X_scaled)
df['cluster'] = kmeans.labels_
```

* Groups regions based on pollution, mobility, and hospital visits.
* Pairplot reveals distinct environmental-health clusters.

---

## Insights

* Respiratory admissions vary significantly across pollution clusters.
* Mask usage rates don’t strongly correlate with reduced admissions in this dataset.
* Some regions with high pollution maintain lower admissions—factors like healthcare access or policy may be at play.


