# League of Legends Position Analysis


## Introduction

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning

### Univariate Analysis
Univariate analysis on damage done to champions by individuals.

<iframe
  src="assets/dist_damage.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The histogram shows a bimodal distribution heavily skewed to the right. 

The skew suggests that most of the observations were concentrated on the lower end of the range, with the long tail implying that there are certain cases where players deal significantly higher damages.

Further, the bimodal nature suggests that there is a more complex underlying pattern in damage distribution.


Univariate analysis on obtained gold at 15 minutes

<iframe
  src="assets/dist_gold.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The histogram shows a nearly normal graph with slight rightward skew. This suggests that the data is distributed in a balanced manner.

### Bivariate Analysis

Bivariate analysis on earned gold share per position.

<iframe
  src="assets/position_vs_share.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This bar graph shows the 


<iframe
  src="assets/position_vs_gold.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Interesting Aggregates
| result | top | jng | mid | bot | sup |
|-----------|-----------|-----------|-----------| -----------|-----------|
| 0 | 0.216391 | 0.181094 | 0.247049 | 0.255583 | 0.099883 |
| 1 | 0.213546 | 0.183561 | 0.240716 | 0.252594 | 0.109584 |


## Assessment of Missingness

### NMAR Analysis

### Missingness Dependency

<iframe
  src="assets/MAR.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Hypothesis Testing

<iframe
  src="assets/hyp.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Framing a Prediction Problem


## Baseline Model


## Final Model


## Fairness Analysis