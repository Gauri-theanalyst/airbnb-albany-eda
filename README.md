# Airbnb Albany EDA - What Actually Drives Pricing?
### Exploratory Data Analysis on 426 real Airbnb listings using Python

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-4C72B0?style=flat&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat&logo=jupyter&logoColor=white)

---

## Project Overview

This project explores what actually drives Airbnb pricing in Albany, New York - the state capital - using a real snapshot of 426 listings scraped in September 2024.

The goal wasn't just to describe the data. It was to challenge assumptions - like whether highly rated listings charge more (they don't), and whether the most expensive listings are actually bad value per person (they often are).

**Dataset:** Inside Airbnb - Albany, NY (September 2024)  
**Tool:** Python (Pandas, Matplotlib, Seaborn)  
**Listings analysed:** 426  
**Columns reduced:** 75 → 22 relevant features  

---

## Key Findings at a Glance

| Finding | Insight |
|---|---|
| 🏠 Size is the #1 price driver | Accommodates has 0.53 correlation with price - stronger than any other factor |
| ⭐ Reviews don't affect price | Review score correlation with price is just 0.09 - guests pay for space, not stars |
| 🏘️ Two-tier neighbourhood market | Fifteenth Ward ($198) and Eighth Ward ($195) are nearly double most other areas |
| 👑 Superhosts don't charge more | Median price is identical - $105 vs $105.50 - but superhosts score 4.87 vs 4.62 on reviews |
| 👥 Group stays offer better value | Price per person negatively correlates with group size (-0.33) - bigger groups pay less per head |
| 🛏️ Room type matters - 2x difference | Entire homes median $120 vs private rooms $65 per night |
| 💰 Outliers are legitimate | The $1,750 listing sleeps 7 - at $250/person it's a genuine premium, not a data error |

---

## Project Structure

```
airbnb-albany-eda/
│
├── README.md
├── airbnb_eda.ipynb          ← main analysis notebook
│
└── Dataset/
    ├── listings.csv          ← primary dataset used
    ├── calendar.csv          ← availability data (not used in this analysis)
    └── reviews.csv           ← review text data (not used in this analysis)
```

---

## Analysis Sections

### 1 - Data Cleaning & Preparation
- Reduced 75 columns to 22 relevant features
- Fixed price column from string (`$120.00`) to float (`120.0`)
- Handled missing values across bathrooms, bedrooms, beds, and review scores
- Created derived column: `price_per_person = price / accommodates`

### 2 - Price Distribution
- Right skewed distribution - majority of listings cluster between $75-$150
- Mean ($128) overstates typical price due to luxury outliers - median ($104) is more representative
- Investigated top 10 most expensive listings - all legitimate large-capacity entire homes

### 3 - Neighbourhood Analysis
- Clear two-tier market: Fifteenth Ward ($198) and Eighth Ward ($195) vs rest at $95-$144
- Sixth Ward is the most active market (97 listings) at a competitive $101 median
- Premium neighbourhoods have significantly fewer listings - exclusivity drives price

### 4 - Room Type Comparison
- Entire homes command roughly 2x the price of private rooms ($120 vs $65 median)
- Entire homes show much wider price variation - private rooms are more predictably priced
- Shared rooms excluded - only 2 listings in dataset

### 5 - Superhost Analysis
- Superhost badge doesn't translate to higher prices at the median level
- Real advantage is review scores: 4.87 vs 4.62 - driving better Airbnb search ranking
- Superhosts list more premium/larger properties, explaining higher average (not median) price

### 6 - Correlation Heatmap
- Accommodates (0.53), bedrooms (0.44), beds (0.42) are strongest price drivers - all size metrics
- Review scores barely correlate with price (0.09) - quality perception doesn't justify premium
- Accommodates, bedrooms and beds correlate strongly with each other (0.75-0.78) - all measuring property size

### 7 - Review Score vs Price Scatter
- No clear upward trend - scattered cloud confirms 0.09 correlation
- Listings at every price point cluster at 4.8-5.0 ratings
- Guests appear to rate relative to price expectations - a $30 room and $600 mansion can both earn 5 stars

---

## Most Interesting Finding

**Raw price rankings are misleading.**

The $1,379 Luxe Urban Farmhouse appeared to be the second most expensive listing. But it accommodates 12 guests - at $114.92 per person it's actually competitively priced compared to a $271 hotel suite for 2 ($135.50 per person).

Normalising by capacity completely reverses the perceived value of listings. This is the kind of insight that only appears when you look beyond the headline number.

---

## Python Skills Demonstrated

```python
# Data manipulation
pd.read_csv() · .groupby() · .agg() · .sort_values() · .value_counts()
.dropna() · .fillna() · .astype() · .map() · .copy()

# Feature engineering
df['price_per_person'] = df['price'] / df['accommodates']

# Visualisation
sns.histplot() · sns.violinplot() · sns.boxplot()
sns.heatmap() · sns.scatterplot() · plt.barh()
plt.figure() · plt.tight_layout() · plt.ylim()

# Analysis
.corr() · .describe() · .isnull().sum()
```

---

## About This Project

Part of my analytics portfolio built during the final trimester of my Master's in Business Analytics. Built from scratch — every line of code written and understood, not copied from tutorials.

This is Project 2 of 3. Project 1 covered SQL-based customer behaviour analysis on 780,000+ e-commerce transactions.

---

*Dataset: Inside Airbnb - Albany, NY (September 2024)*  
*Analyst: Gauri | Master's in Business Analytics | Based in Australia*
