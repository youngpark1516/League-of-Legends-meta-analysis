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

| Column Name         | Data Type |
|---------------------|-----------|
| gameid              | object    |
| league              | object    |
| gamelength          | int64     |
| position            | object    |
| result              | int64     |
| damagetochampions   | int64     |
| earnedgoldshare     | float64   |
| visionscore         | int64     |
| kills               | int64     |
| deaths              | int64     |
| assists             | int64     |
| goldat15            | float64   |
| csat15              | float64   |
| total cs            | float64   |
| champion            | object    |


### Data Cleaning

### Univariate Analysis

**Univariate analysis on damage done to champions by individuals**

<iframe
  src="assets/dist_damage.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

There are two peaks in the distribution, the first at around 8,000 damage and the second around 20,000 damage. The bimodal nature suggests that there is a more complex underlying pattern in damage distribution.

The distribution is heavily skewed to the right with a long tail extending up to 100000. The skew suggests that most of the observations were concentrated on the lower end of the range with the long tail implying that there are certain cases where players deal significantly higher damages.

**Univariate analysis on obtained gold at 15 minutes**

<iframe
  src="assets/dist_gold.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The histogram has a single peak at around 5000 gold indicating that most players have earned about this amount of gold by 15 minutes into the game. The peak is likely a typical gold level that players reach at 15 minutes, reflecting a common trend in professional games.

The distribution is slightly skewed rightwards, some players earning up to 10k. This indicates that there are some cases where a player earns significantly more gold but these instances are relatively rare, likely from obtaining significant kills from early game fights. 

### Bivariate Analysis

Bivariate analysis on earned gold share per position.

<iframe
  src="assets/position_vs_vision_bar.html"
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

An aggregate analysis was performed to understand the distribution of gold across different positions for winning and losing teams. Specifically, a pivot table was created to compare the average percentage of gold earned (earnedgoldshare) by each position between teams that won (result = 1) and teams that lost (result = 0). The mean was used as aggreagate function.

| result | top       | jng       | mid       | bot       | sup       |
|--------|-----------|-----------|-----------|-----------|-----------|
| 0      | 0.216337  | 0.181242  | 0.246962  | 0.255654  | 0.099805  |
| 1      | 0.213628  | 0.183764  | 0.240636  | 0.252545  | 0.109427  |

The aggregate shows that winning teams tend to jave allocated more gold to jungle and support roles compared to losing teams. While this may indicate that allocating greater gold to jungle and support may lead to better results, it may also be that being in a winning position in the game causes jungle and support to obtain more gold. Correlation not necessarily a causation. Regardless, I personally like to steal kills when playing suppport.

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

**Observed data**

| bot_greater | result   |
|-------------|----------|
| False       | 0.488718 |
| True        | 0.512186 |

**Hypothesis test result**
<iframe
  src="assets/hyp.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

We obtain a p-value of 0.0014, rejecting the null hypothesis at 5% significance level. This suggests that a team that had more gold allocated to the bot laner/ADC than mid laner at 15 minutes had higher likelihood of winning the game. This implies that investing greater gold to bot lane may lead to a significant advantage in winning a game in professional level of League of Legends.

## Framing a Prediction Problem


## Baseline Model


## Final Model


## Fairness Analysis