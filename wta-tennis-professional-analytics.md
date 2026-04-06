# WTA Tennis Professional Analytics 2020-2024

## Introduction

This project analyzes Women’s Tennis Association (WTA) match data spanning five seasons (2020–2024) with the goal of deriving actionable insights both for understanding the broader competitive landscape and for informing player development decisions. The central analytical objective is twofold: (1) characterize what distinguishes winners from losers at a population level, and (2) identify patterns that define improving players with a particular focus on Qinwen Zheng as a case study in rapid ranking ascent. A secondary applied objective frames part of the analysis from a coaching perspective: understanding how many tournaments elite players compete in per year, how titles are distributed, and whether specific serve metrics are statistically associated with rank improvement over time.

## Dataset

All data is available on GitHub and was created by Jeff Sackmann. The dataset contains 11,966 matches across 533 unique tournaments, covering 626 distinct players competing on hard, clay, and grass surfaces at varying levels of competition, from Grand Slams down to International-level events. After removing records with missing values in key match fields, the working dataset consists of 11,706 matches. The data include player identities (winner and loser), contextual variables (surface, tournament, round), and detailed performance statistics such as aces, double faults, serve percentages, and break point outcomes.

## Research Questions

Coming into this dataset, I had no explicit research question in mind, and throughout the exploring process, the research questions were developed as the following:

- Do winners differ from losers in physical characteristics such as age and height, and if so, how large are these effects?
- How have the top 10 players of 2024 evolved in rankings over the full 2020–2024 period?
- What patterns in tournament performance characterize Qinwen Zheng's rapid ranking improvement?
- Among players who improved their ranking in the past 5 years, how do tournament load and results vary by rank tier?
- How does the proportion of matches against higher-ranked versus lower-ranked opponents vary by rank tier, and what are the win rates in each scenario?
- Are serve metrics (first serve percentage, first serve win percentage) statistically associated with rank improvement across all players?

## Data Cleaning

Data preparation proceeded in two stages. First, rows missing any of the minimum required fields — surface, tournament level, round, winner name, loser name, winner rank, and loser rank — were removed, reducing the dataset from 11,966 to 11,706 matches. Second, numeric columns (rank, ranking points, age, height, draw size) were coerced to float with errors treated as missing rather than raising exceptions. Tournament date strings stored as integers in `YYYYMMDD` format were converted to datetime objects for time-series analysis. A round-order mapping was applied to convert categorical round labels (`R128` through `F`) into ordinal values for identifying each player's furthest result per tournament.

## Findings

### Age

Across all 11,706 matches, winners were slightly younger than losers (mean age: 26.05 vs. 26.33 years). A paired t-test indicated that this difference was statistically significant (`t = -5.11`, `p < 0.0001`), suggesting that younger players had a marginal advantage. However, the magnitude of the difference was small (~0.28 years), and the distribution of age differences is approximately centered near zero with substantial spread.

 <img width="294" height="230" alt="image" src="https://github.com/user-attachments/assets/a6fcc5aa-a6cd-4e18-8579-2e1912c8c480" />

### Height

Winners were also slightly taller than losers (mean height: 174.76 cm vs. 174.16 cm). This difference was statistically significant (`t = 6.49`, `p < 0.0001`), indicating that taller players had a marginal advantage. However, the magnitude of the difference was very small (~0.6 cm). The finding suggests a marginal structural advantage for taller players, possibly linked to serve effectiveness, but height does not determine competitive outcomes at the match level.

### Top 10 Players

<img width="468" height="267" alt="image" src="https://github.com/user-attachments/assets/9600334c-5cb9-46ab-9f82-45b996cad541" />

The 2024 top 10 were identified by selecting the 10 players with the lowest best observed rank during the 2024 season. Plotting monthly median rankings from 2020 to 2024 reveals varied trajectories. Swiatek and Sabalenka maintained consistently elite rankings throughout the period, while players like Gauff, Rybakina, and Zheng showed clear upward trends.

Among all players in the dataset, the top 10 by total titles are led by Iga Swiatek (22 titles from 25 finals appearances), followed by Aryna Sabalenka (12 titles from 22 finals). However, not all top 10 ranked players had the most number of finals and titles. Barbora Krejcikova, Daria Kasatkina, and Anett Kontaveit earned top-10 places in finals and titles, while they did not make the top 10 by 2024, indicating that the number of championships and finals reached does not fully determine a player's ranking.

## Professional Analysis

From the perspective of a professional player’s coach, if I were to start planning with a professional player, there are several questions I would need to know:

1. How many matches does she need to play in a year?
2. What percentage of her matches should be against higher-ranked opponents, and what percentage against lower-ranked ones?

The reasoning behind this question is that players need to gain confidence from victories. Of course, competing in bigger tournaments offers greater opportunities to improve rankings, and challenging higher-ranked players provides valuable learning experiences. However, a player’s confidence is often more closely tied to the results of their performance. We need to ensure the player secures enough wins while also having sufficient opportunities to take on more challenging matches.

In this analysis, we only look at players with improved ranking over the study period, in order to learn from their tournament decisions and performance patterns. Players were classified as improving if their yearly median WTA ranking showed a negative linear trend (numerically decreasing rank = improving) across at least three years of data. This criterion identified 169 improving players. The table below summarizes average tournament appearances, finals, and titles per year for improving players, grouped by rank tier. Players ranked below approximately 100 who participate primarily in ITF-level events are underrepresented in this dataset, which limits the reliability of the analysis for those tiers.

| Rank Group | Avg Tournaments/Year | Median Tournaments/Year | Avg Finals/Year | Avg Titles/Year | Player-Years | Players |
|---|---:|---:|---:|---:|---:|---:|
| Top 10 | 17.76 | 18.0 | 4.04 | 2.48 | 25 | 11 |
| 10–30 | 19.02 | 20.0 | 1.71 | 0.83 | 48 | 28 |
| 30–100 | 16.97 | 18.0 | 0.64 | 0.32 | 228 | 94 |
| 100–200 | 6.33 | 6.0 | 0.11 | 0.04 | 238 | 121 |
| >200 | 2.48 | 2.0 | — | — | — | — |

Players ranked in the top 10 average approximately 18 tournaments per year with over 4 finals appearances and 2.5 titles. Those in the 10–30 range play the most tournaments, averaging 19 per year, but win fewer titles, reflecting the competitive density at that tier. Players in the 30–100 range appear at about 17 events per year and average less than one final per year. Depending on the ranking of the player that I will be working with, we can plan the number of WTA-level tournaments for the year.

Top 10 players face higher-ranked opponents in only about 8% of their matches, and they win roughly 74% against lower-ranked opponents. Players in the 10–30 range win 44% against higher-ranked players, and players in the 30–100 range play 51% against higher-ranked opponents and win 38%. Interestingly, players in the 100–200 tier play higher-ranked opponents 76% of the time, but they also win 38%. We can see that players outside of the top 100 do not play as many WTA-level tournaments, with fewer than 6 per year. While we do not know how much they play at the ITF level, they do not have a significantly lower win percentage, and the percentage of an upset is not dramatically lower than that of top-100 players. Therefore, when working with a player between 100–200, we need to do more thorough research on the proportion of WTA-level and ITF-level tournament planning based on current performance and many other factors.

## Case Study: Qinwen Zheng

<img width="468" height="204" alt="image" src="https://github.com/user-attachments/assets/75205240-395e-4ad7-88d9-3b4274074ffa" />

From the ranking trajectories we generated earlier, Qinwen Zheng illustrates a clear developmental trend. I wanted to know what she did well to improve her ranking so quickly. Pulling her results for the past 5 years, she reached 10 finals and won 5 titles out of those 10. She made the most finals in 2024, and the question arises: what explains that huge jump from 2021 to 2023? I know that serve has been a huge weapon for her, so I tried to see if her serve performance improved over time and whether that was the greatest contribution to her ranking improvement.

Using the two performance metrics we have in the dataset, average first serves made and first-serve points won per tournament, alongside her ranking trend revealed a notable spike in first serves made at the end of 2021 and into early 2022. However, in this period, she was still losing in early rounds. This spike likely reflects longer sets in closer-fought early-round matches. The serve trend and ranking trend converge more tightly from 2023 onward, coinciding with her first title runs.

## Serve Metrics and Rank Improvement Regression

Only looking at Qinwen’s results does not give me the answer of whether serve performance is statistically associated with ranking changes. To find out this association among the entire study population, an OLS regression was estimated across all players with available serve data. For each player-tournament observation, serve metrics were averaged across matches within that tournament, and the outcome variable (rank change) was defined as the difference between a player's rank at the next tournament and their rank at the current tournament.

The model included six predictors: first serve percentage (number of first serves in / total serve points), first serve win percentage (points won with first serve in / number of first serves in), second serve win percentage, ace rate, double fault rate, and break point save percentage.

| Predictor | Coefficient | p-value | 95% CI Low | 95% CI High |
|---|---:|---:|---:|---:|
| Intercept | 23.639 | 0.001* | 9.543 | 37.735 |
| First serve % | -16.822 | 0.029* | -31.929 | -1.716 |
| First serve win % | -15.408 | 0.027* | -29.070 | -1.746 |
| Second serve win % | -4.724 | 0.431 | -16.480 | 7.031 |
| Ace rate | -2.498 | 0.899 | -40.997 | 36.001 |
| Double fault rate | -16.810 | 0.361 | -52.857 | 19.232 |
| Break point save % | -4.719 | 0.152 | -11.177 | 1.738 |

Among the six predictors, first serve percentage (`β = -16.82`, `p = 0.029`) and first serve win percentage (`β = -15.41`, `p = 0.027`) were both statistically significant and negatively signed, meaning that players with a higher proportion of first serves in, and a higher proportion of first-serve points won, tend to improve their ranking between tournaments. Second serve win percentage, ace rate, double fault rate, and break point save percentage were not significant predictors. This result provides directional evidence that first-serve effectiveness is meaningfully associated with ranking trajectories, consistent with the serve development hypothesis motivating the Qinwen Zheng case study.

## Limitations and Conclusion

Several limitations apply to the current analysis. First, the dataset only consists of WTA Tour-level tournaments and not ITF-level events. Players may be playing more ITF-level tournaments besides the WTA Tour, which we are not considering. Second, the in-match statistics are not advanced performance indicators, such as first-serve speed, direction, or spin. Furthermore, the OLS regression treats all player-tournament observations as independent, ignoring the longitudinal structure within players. A mixed model with player random effects would be a more appropriate next step.

Overall, this analysis of WTA match data from 2020 to 2024 reveals several consistent patterns across different levels of the competitive landscape. At the population level, winners tend to be marginally younger and taller than their opponents, though the effect sizes are small enough that neither characteristic meaningfully predicts individual match outcomes. The rank-tier analysis of improving players highlights a structural reality of professional tennis: below rank 100, WTA-level match exposure drops sharply, and the path upward requires navigating a schedule that combines higher-ranked opponents and lower-level tournaments. The ranking trajectories for the top 10 players highlight a clear spike in Qinwen Zheng’s development, with a concentration of finals runs beginning in 2023 and culminating in a Grand Slam final and Olympic title in 2024. The serve regression adds a quantitative dimension to this story. While serve metrics alone explain only a small fraction of tournament-to-tournament rank changes, first serve percentage and first serve win percentage emerge as the two statistically significant predictors, suggesting that first-serve effectiveness is a meaningful contributor to sustained ranking improvement. Taken together, these findings offer a foundation for further player development analysis and future mixed-effects modeling of longitudinal performance.

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

