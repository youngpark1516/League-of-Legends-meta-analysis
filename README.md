# League of Legends Position Analysis

## Introduction

### General introduction

### Dataset introduction
The dataset provides a wide range of columns that capture gameplay metrics and match outcomes from professional League of Legends (LoL) esports matches throughout the year 2024. 

The dataset contains 116,064 rows and 161 columns with extensive detail of the each game. Below is a brief introduction to the columns that this project will focus on:

| Column              | Description                                                             |
|---------------------|-------------------------------------------------------------------------|
| `gameid`            | Unique identifier for the game.                                         |
| `league`            | The league in which the game was played (e.g., TSC).                    |
| `gamelength`        | Length of the game in seconds.                                          |
| `position`          | The role of the player (top, jng, mid, bot, sup)                        |
| `result`            | Outcome of the game for the player (1 for win, 0 for loss).             |
| `damagetochampions` | Total damage dealt by the player to champions.                          |
| `earnedgoldshare`   | Proportion of total team gold earned by the player.                     |
| `visionscore`       | Player's vision score, reflecting warding and vision contributions.     |
| `kills`             | Number of kills made by the player.                                     |
| `deaths`            | Number of times the player died.                                        |
| `assists`           | Number of assists made by the player.                                   |
| `goldat15`          | Gold earned by the player at 15 minutes into the game.                  |
| `csat15`            | Creep score (minions killed) by the player at 15 minutes.               |
| `total cs`          | Total creep score by the player by the end of the game.                 |
| `champion`          | The champion played by the player in the game.                          |

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning

**Column filtering**
First, only the desired columns for the following analysis were selected. These included `gameid`, `league`, `patch`, `gamelength`, `position`, `result`, `damagetochampions`, `earnedgoldshare`, `visionscore`, `kills`, `deaths`, `assists`, `goldat15`, `csat15`, `total cs`, and `champion`.

**Row filtering**
Next, only the games that were played in the 14th season (2024) were selected as the original dataset included games in the later patches of season 13. After this process, `patch` was dropped as it was no longer needed.

**Datatypes**
Below are the datatypes of the selected columns:

| Column Name           | Data Type |
|-----------------------|-----------|
| `gameid`              | object    |
| `league`              | object    |
| `gamelength`          | int64     |
| `position`            | object    |
| `result`              | int64     |
| `damagetochampions`   | int64     |
| `earnedgoldshare`     | float64   |
| `visionscore`         | int64     |
| `kills`               | int64     |
| `deaths`              | int64     |
| `assists`             | int64     |
| `goldat15`            | float64   |
| `csat15`              | float64   |
| `total cs`            | float64   |
| `champion`            | object    |

The datatypes are apppropriate.

**Further row filtering**
Lastly, in this dataframe, every 12 consecutive rows represent a single game sharing the identical `gameid`. 

Below are the first 12 rows of `df_2024`, representing a single game with the `gameid` of 'LOLTMNT99_132542'.

| gameid            | league | gamelength | position | result | damagetochampions | earnedgoldshare | visionscore | kills | deaths | assists | goldat15 | csat15 | total cs | champion       |
|--------------------|--------|------------|----------|--------|-------------------|-----------------|-------------|-------|--------|---------|----------|--------|----------|----------------|
| LOLTMNT99_132542  | TSC    | 1446       | top      | 1      | 11806             | 0.207072        | 17          | 4     | 1      | 4       | 5229.0   | 136.0  | 210.0    | Renekton       |
| LOLTMNT99_132542  | TSC    | 1446       | jng      | 1      | 12455             | 0.210727        | 40          | 5     | 1      | 11      | 5366.0   | 99.0   | 154.0    | Xin Zhao       |
| LOLTMNT99_132542  | TSC    | 1446       | mid      | 1      | 14082             | 0.174046        | 24          | 1     | 3      | 8       | 5015.0   | 133.0  | 208.0    | LeBlanc        |
| LOLTMNT99_132542  | TSC    | 1446       | bot      | 1      | 17295             | 0.271228        | 33          | 8     | 1      | 7       | 7296.0   | 141.0  | 234.0    | Varus          |
| LOLTMNT99_132542  | TSC    | 1446       | sup      | 1      | 5839              | 0.136927        | 72          | 2     | 1      | 17      | 4128.0   | 21.0   | 25.0     | Renata Glasc   |
| LOLTMNT99_132542  | TSC    | 1446       | top      | 0      | 8873              | 0.237100        | 18          | 1     | 3      | 1       | 5804.0   | 144.0  | 207.0    | Jax            |
| LOLTMNT99_132542  | TSC    | 1446       | jng      | 0      | 6537              | 0.199814        | 20          | 2     | 2      | 3       | 5130.0   | 105.0  | 154.0    | Lee Sin        |
| LOLTMNT99_132542  | TSC    | 1446       | mid      | 0      | 12973             | 0.239890        | 19          | 1     | 3      | 4       | 5424.0   | 137.0  | 190.0    | Neeko          |
| LOLTMNT99_132542  | TSC    | 1446       | bot      | 0      | 10730             | 0.205267        | 22          | 1     | 5      | 4       | 4485.0   | 101.0  | 170.0    | Kalista        |
| LOLTMNT99_132542  | TSC    | 1446       | sup      | 0      | 3624              | 0.117928        | 62          | 2     | 7      | 2       | 3898.0   | 20.0   | 31.0     | Nautilus       |
| LOLTMNT99_132542  | TSC    | 1446       | team     | 1      | 61477             | NaN             | 186         | 20    | 7      | 47      | 27034.0  | 530.0  | NaN      | NaN            |
| LOLTMNT99_132542  | TSC    | 1446       | team     | 0      | 42737             | NaN             | 141         | 7     | 20     | 14      | 24741.0  | 507.0  | NaN      | NaN            |

It can be seen that the first 10 rows present the data of individual players of both teams while the last two rows with the `position` value 'team' is of the overall team data. In this project, team cumulative data will not be necessary, and is therefore removed.

The cleaned dataframe is saved as `df_2024`.

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

**Bivariate analysis on vision score per position**

<iframe
  src="assets/position_vs_vision_bar.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This bar graph shows that support provides the highest vision score by a large margin. The jungle and bot positions also contribute moderately to vision, while mid and top have the least impact in this aspect of the game. This distribution shows that vision control is predominantly handled by supports.


**Bivariate analysis on gold earned at 15 minutes per position**

<iframe
  src="assets/position_vs_gold.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The box plot suggests that bot and mid laners tend to have the highest gold at 15 minutes with bot having more variance. They are followed by top and jungle, where jungle is seen to have no outliers in the lower end, likely from the fact that the early farming process of jungle has relatively low likelihood of interruption. Lastly, support consistently has the lowest gold with no outliers in the lower end, both of which can be explained by the fact that  the role often does not actively farm and obtains gold passively, especially in the early stages.

### Interesting Aggregates

An aggregate analysis was performed to understand the distribution of gold across different positions for winning and losing teams. Specifically, a pivot table was created to compare the average percentage of gold earned (earnedgoldshare) by each position between teams that won (result = 1) and teams that lost (result = 0). The mean was used as aggreagate function.

| result | top       | jng       | mid       | bot       | sup       |
|--------|-----------|-----------|-----------|-----------|-----------|
| 0      | 0.216337  | 0.181242  | 0.246962  | 0.255654  | 0.099805  |
| 1      | 0.213628  | 0.183764  | 0.240636  | 0.252545  | 0.109427  |

The aggregate shows that winning teams tend to jave allocated more gold to jungle and support roles compared to losing teams. While this may indicate that allocating greater gold to jungle and support may lead to better results, it may also be that being in a winning position in the game causes jungle and support to obtain more gold. Correlation not necessarily a causation. Regardless, I personally like to steal kills when playing suppport.

## Assessment of Missingness

In this section, different types of missingness in the dataset will be discussed.

### NMAR Analysis

### Missingness Dependency

In this subsection, the dependency of missingness of the column `goldat15` will be investigated

The first column tested will be `league`.

**Null Hypothesis (H<sub>0</sub>)**: The missingness of `goldat15` does not depend on the `league`.

**Alternate Hypothesis (H<sub>a</sub>)**: The missingness of `goldat15` does depend on the `league`.

**Test Statistic**: The Total Variation Distance (TVD) between the distributions of goldat15 missingness across different leagues.

**Significance Level**: 0.05

Below is the top 10 leagues contributing the most to the missingness of `goldat15`.

<iframe
  src="assets/MAR_obs.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Permutation test was ran 5000 times by shuffling the missingness of `goldat15` and was compared against the observed test statistic.

<iframe
  src="assets/MAR.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The p-value found is 0.0, and as 0.0 < 0.5, the null hypothesis is rejected. The missingness of `goldat15` likely depends on `league`.

The second column tested

## Hypothesis Testing
In this hypothesis test, I aim to determine whether allocating greater gold to the bot/ADC (Attack Damage Carry) compared to the mid laner at 15 minutes has a significant impact on the likelihood of winning the game. This investigation is vital for understanding optimal gold distribution strategies in League of Legends and their influence on game results.

**Null Hypothesis (H<sub>0</sub>)**: Allocating greater gold to the ADC than the mid laner at 15 minutes does not lead to a higher likelihood of winning the game compared to allocating greater gold to the mid laner.

**Alternative Hypothesis (H<sub>a</sub>):** Allocating greater gold to the ADC than the mid laner at 15 minutes does lead to a higher likelihood of winning the game compared to allocating greater gold to the mid laner.

**Test Statistic:** Signed difference in winrate (mean) between games where the ADC had greater gold at 15 minutes and games where the mid laner had greater gold at 15 minutes. Difference in mean is used as the aim is to compare a central tendency between two groups.

**Significance Level**: 0.05

**Observed data**

| bot_greater | result   |
|-------------|----------|
| False       | 0.488718 |
| True        | 0.512186 |

<iframe
  src="assets/hyp_demo_fig.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

**Hypothesis test result**
<iframe
  src="assets/hyp.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

A p-value of 0.0014 is obtained, rejecting the null hypothesis at 5% significance level. This suggests that a team that had more gold allocated to the bot laner/ADC than mid laner at 15 minutes had higher likelihood of winning the game. This implies that investing greater gold to bot lane may lead to a significant advantage in winning a game in professional level of League of Legends.

## Framing a Prediction Problem


## Baseline Model


## Final Model


## Fairness Analysis