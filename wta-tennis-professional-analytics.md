# WTA Tennis Professional Analytics (2020–2024)

## Overview
This project analyzes Women's Tennis Association (WTA) match data from 2020 to 2024 to understand what separates winners from losers, what patterns characterize ranking improvement, and how match-level performance can inform player development decisions.

The project combines descriptive analytics, player trajectory analysis, case-study exploration, and regression modeling to examine both the competitive landscape of professional women's tennis and the development path of improving players.

## Objectives
This analysis was designed around three main goals:

- Identify population-level differences between match winners and losers
- Examine how top players, especially Qinwen Zheng, improved over time
- Explore whether serve-related performance metrics are associated with ranking improvement

## Dataset
The data come from Jeff Sackmann's public WTA match datasets and include:

- **11,966 matches** across **533 tournaments**
- **626 players**
- Seasons: **2020–2024**
- Surfaces: **hard, clay, and grass**
- Variables including player identity, rankings, tournament context, and match statistics

After removing rows with missing values in key variables, the working dataset included **11,706 matches**.

## Research Questions
This project explored the following questions:

1. Do winners differ from losers in age and height?
2. How did the 2024 Top 10 players evolve in the rankings from 2020 to 2024?
3. What performance patterns characterize Qinwen Zheng's rapid rise?
4. Among players who improved their rankings, how do tournament load and results vary by rank tier?
5. How often do players at different rank tiers face higher-ranked opponents, and how often do they win?
6. Are serve metrics statistically associated with ranking improvement?

## Data Preparation
The main cleaning steps included:

- Removing observations with missing values in critical variables such as surface, tournament level, round, player names, and rankings
- Converting numeric columns such as rank, ranking points, age, height, and draw size to numeric format
- Converting tournament dates from `YYYYMMDD` format into datetime objects
- Mapping round labels (for example, `R128` to `F`) into ordinal order for tournament progression analysis

## Methods
This project used several analytical approaches:

- **Descriptive statistics** to compare winners and losers
- **Paired t-tests** for age and height comparisons
- **Ranking trajectory analysis** using monthly median rankings from 2020 to 2024
- **Player classification** based on ranking trend over time
- **Tournament-load summaries** by rank tier
- **Case study analysis** of Qinwen Zheng's results and serve metrics
- **OLS regression** to test whether serve metrics predict rank change between tournaments

## Key Findings

### 1. Winners were slightly younger and taller
Across 11,706 matches:

- Winners were slightly younger than losers (26.05 vs. 26.33 years)
 <img width="294" height="230" alt="image" src="https://github.com/user-attachments/assets/fa34636b-1541-488d-9f86-539926af38db" />

- Winners were slightly taller than losers (174.76 cm vs. 174.16 cm)

Both differences were statistically significant, but the effect sizes were small, suggesting that age and height provide only modest advantages at the match level.

### 2. Ranking trajectories differed substantially among top players
The 2024 Top 10 players showed very different development patterns:
<img width="468" height="267" alt="image" src="https://github.com/user-attachments/assets/9f8f26ca-7670-41a1-937f-9a0619398f15" />


- Iga Swiatek and Aryna Sabalenka remained consistently elite
- Coco Gauff, Elena Rybakina, and Qinwen Zheng showed strong upward trajectories

This highlighted that top-level status can emerge through different developmental paths.

### 3. Titles and finals do not fully explain rankings
Although players such as Swiatek and Sabalenka led in titles and finals appearances, not every player with many finals or titles finished in the 2024 Top 10. This suggests ranking outcomes reflect broader consistency across the season, not only peak tournament results.

### 4. Tournament load varies meaningfully by rank tier
Among players with improving rankings:

- **Top 10** players averaged about **18 tournaments per year**, **4 finals**, and **2.5 titles**
- **Rank 10–30** players played the most events, averaging **19 tournaments per year**
- **Rank 30–100** players averaged about **17 tournaments per year**
- **Rank 100–200** players had much lower WTA-level exposure, averaging about **6 tournaments per year**

This suggests tournament planning depends heavily on a player's current competitive tier.

| Rank Group | Avg Tournaments/Year | Median Tournaments/Year | Avg Finals/Year | Avg Titles/Year | Player-Years | Players |
|---|---:|---:|---:|---:|---:|---:|
| Top 10 | 17.76 | 18.0 | 4.04 | 2.48 | 25 | 11 |
| 10–30 | 19.02 | 20.0 | 1.71 | 0.83 | 48 | 28 |
| 30–100 | 16.97 | 18.0 | 0.64 | 0.32 | 228 | 94 |
| 100–200 | 6.33 | 6.0 | 0.11 | 0.04 | 238 | 121 |
| >200 | 2.48 | 2.0 | — | — | — | — |


### 5. Matchup difficulty changes by rank tier
The opponent profile also varied across ranking levels:

- Top 10 players faced higher-ranked opponents in only a small share of matches
- Players ranked 10–30 and 30–100 faced stronger opponents more often
- Players ranked 100–200 played higher-ranked opponents most of the time but still maintained competitive win rates

This has practical implications for balancing ranking opportunities, competitive challenge, and player confidence.

### 6. First-serve effectiveness was associated with ranking improvement
An OLS regression model tested whether serve performance predicted rank change between tournaments. Among six serve-related predictors, two were statistically significant:

- **First serve percentage**
- **First serve win percentage**

Both were negatively associated with rank change, meaning stronger first-serve performance was linked to ranking improvement.

Other variables, including second-serve win percentage, ace rate, double-fault rate, and break-point save percentage, were not statistically significant in this model.

## Qinwen Zheng Case Study
Qinwen Zheng was used as a focused case study because her ranking trajectory showed one of the clearest upward trends in the dataset.
<img width="350" height="180" alt="image" src="https://github.com/user-attachments/assets/9b72f05b-ec0f-4404-bc2f-648252f63186" />

The analysis found that:

- She reached **10 finals** and won **5 titles** during the study period
- Her strongest concentration of finals came in 2024
- Her serve metrics appeared to improve meaningfully from late 2021 into 2022
- Her serve development aligned more closely with ranking gains from 2023 onward

This suggests first-serve effectiveness may have been an important contributor to her competitive rise.

| Predictor | Coefficient | p-value | 95% CI Low | 95% CI High |
|---|---:|---:|---:|---:|
| Intercept | 23.639 | 0.001* | 9.543 | 37.735 |
| First serve % | -16.822 | 0.029* | -31.929 | -1.716 |
| First serve win % | -15.408 | 0.027* | -29.070 | -1.746 |
| Second serve win % | -4.724 | 0.431 | -16.480 | 7.031 |
| Ace rate | -2.498 | 0.899 | -40.997 | 36.001 |
| Double fault rate | -16.810 | 0.361 | -52.857 | 19.232 |
| Break point save % | -4.719 | 0.152 | -11.177 | 1.738 |

## Limitations
This analysis has several limitations:

- The dataset focuses on WTA-level events and does not fully capture ITF participation
- The available match statistics are limited and do not include richer performance variables such as serve speed, direction, or spin
- The OLS model treats player-tournament observations as independent and does not account for repeated measures within players

A logical next step would be to use mixed-effects models to better account for the longitudinal structure of player performance.

## Tools Used
- Python
- pandas
- NumPy
- statsmodels
- matplotlib / seaborn
- Jupyter Notebook

## Why This Project Matters
This project demonstrates how sports analytics can be used not only to describe performance but also to support coaching decisions, player development planning, and competitive strategy. It reflects my broader interest in applying data analytics to tennis performance and decision-making.

## Future Improvements
Potential next steps include:

- Adding ITF-level tournament data
- Building mixed-effects models for longitudinal player development
- Incorporating more advanced serve and rally metrics
- Creating an interactive dashboard for player comparison and performance tracking

---

**Author:** Cindy Hu  
**Focus Area:** Sports Analytics | Tennis Performance | Player Development

