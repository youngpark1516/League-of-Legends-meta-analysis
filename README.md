# League of Legends Position Analysis


## Introduction

| Column            | Description                                                             |
|-------------------|-------------------------------------------------------------------------|
| gameid            | Unique identifier for the game.                                         |
| league            | The league in which the game was played (e.g., TSC).                    |
| gamelength        | Length of the game in seconds.                                          |
| position          | The role of the player (top, jng, mid, bot, sup)                        |
| result            | Outcome of the game for the player (1 for win, 0 for loss).             |
| damagetochampions | Total damage dealt by the player to champions.                          |
| earnedgoldshare   | Proportion of total team gold earned by the player.                     |
| visionscore       | Player's vision score, reflecting warding and vision contributions.     |
| kills             | Number of kills made by the player.                                     |
| deaths            | Number of times the player died.                                        |
| assists           | Number of assists made by the player.                                   |
| goldat15          | Gold earned by the player at 15 minutes into the game.                  |
| csat15            | Creep score (minions killed) by the player at 15 minutes.               |
| total cs          | Total creep score by the player by the end of the game.                 |
| champion          | The champion played by the player in the game.                          |


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

| result | top       | jng       | mid       | bot       | sup       |
|--------|-----------|-----------|-----------|-----------|-----------|
| 0      | 0.216391  | 0.181094  | 0.247049  | 0.255583  | 0.099883  |
| 1      | 0.213546  | 0.183561  | 0.240716  | 0.252594  | 0.109584  |


## Assessment of Missingness

### NMAR Analysis

### Missingness Dependency

<iframe
  src="assets/MAR_obs.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/MAR.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Hypothesis Testing
In this hypothesis test, I aim to determine whether allocating greater gold to the bot/ADC (Attack Damage Carry) compared to the mid laner at 15 minutes has a significant impact on the likelihood of winning the game. This investigation is vital for understanding optimal gold distribution strategies in League of Legends and their influence on game results.

**Null Hypothesis (H~0~)**: Allocating greater gold to the ADC than the mid laner at 15 minutes does not lead to a higher likelihood of winning the game compared to allocating greater gold to the mid laner.

**Alternative Hypothesis (H~a~):** Allocating greater gold to the ADC than the mid laner at 15 minutes does lead to a higher likelihood of winning the game compared to allocating greater gold to the mid laner.

**Test Statistic:** Signed difference in winrate (mean) between games where the ADC had greater gold at 15 minutes and games where the mid laner had greater gold at 15 minutes. Difference in mean is used as the aim is to compare a central tendency between two groups.

**Significance Level**: 5%

<iframe
  src="assets/hyp.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

We obtain a p-value of 0.0003, rejecting the null hypothesis at 5% significance level. This suggests that a team that had more gold allocated to the bot laner/ADC than mid laner at 15 minutes had higher likelihood of winning the game. This implies that investing greater gold to bot lane may lead to a significant advantage in winning a game in professional level of League of Legends.

## Framing a Prediction Problem


## Baseline Model


## Final Model


## Fairness Analysis