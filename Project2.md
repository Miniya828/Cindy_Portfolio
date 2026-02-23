---
title: Project 2
---

# WTA Top 100 vs WNBA: How Different Are Athlete Body-Size Profiles
***Using publicly available height and weight data, I compared body-size profiles between WTA Top 100 tennis players and WNBA players. Across multiple analyses, WNBA athletes are taller, heavier, and have higher BMI on average than WTA Top-100 athletes. Even within a shared height range (167.6–185.0 cm), WTA players weigh about ~17 lb less than WNBA players of the same height.***

## Data and approach
This project compares anthropometric profiles between WNBA players and WTA Top 100 tennis players using height (cm), weight (lb), and BMI (kg/m²). Data sources are scrapped from WNBA official website, WTA official website, and ESPN. Because the two sports differ in typical height ranges, I used two complementary strategies: (1) global comparisons using all available observations (BMI tests; MANOVA on height–weight) and (2) comparisons restricted to the overlapping height interval for the two sports to avoid extrapolation when asking “at the same height, do athletes weigh differently?”

## 1. Do WNBA and WTA athletes differ in BMI?
BMI values were available for 66 WTA players and 132 WNBA players. ***WNBA players had a higher mean BMI (mean = 23.04) than WTA Top 100 players (mean = 20.27)***. A Welch two-sample t-test indicated a statistically significant difference in means (t = 6.64, df = 93.78, p = 2×10⁻⁹), with a 95% confidence interval for the mean difference (WNBA − WTA) of [1.94, 3.59] BMI units. A Wilcoxon rank-sum test provided consistent evidence that the BMI distributions differ between groups (p = 3.39×10⁻¹⁵). These results support a clear difference in body-size profiles across sports, while noting that BMI is descriptive and does not directly measure body composition or fitness.
<img width="500" height="650" alt="BMI comprison" src="https://github.com/user-attachments/assets/e94aef08-5cc1-42ea-b829-61ea9002f582" />

## 2. At the same height, do WNBA players weigh more than WTA players?
To compare weights at the same height without extrapolating beyond where the two sports overlap, I restricted the dataset to the shared height interval of 167.64–185.00 cm. This produced an overlap sample of 53 WNBA and 57 WTA athletes. In a linear regression model predicting weight from height and sport (Weight ~ Height + Sport), height was strongly associated with weight (estimate = 2.20 lb per cm, p = 4.60×10⁻¹¹). Importantly, the sport indicator was also significant: relative to WNBA (reference), the WTA coefficient was (−16.86 lb, p = 1.39×10⁻⁹). This indicates that, ***within the shared height range, WTA Top 100 players weigh approximately 17 lb less than WNBA players of the same height on average***.
<img width="500" height="500" alt="Height-weight profiles" src="https://github.com/user-attachments/assets/a77e7cdf-16b6-4601-af29-1165a484c9e8" />

<img width="500" height="500" alt="Height-weight by sport" src="https://github.com/user-attachments/assets/c00189ef-8580-4e87-80c5-d6d0f108b293" />

## 3. What is the expected weight for one to become a WTA Top 100 / WNBA player?
Using the overlap-trained interaction model, I created a simple prediction function to estimate an expected weight given a player’s height and sport, along with a 95% prediction interval (a plausible range for an individual athlete). For example, at 180 cm, the model predicts an expected weight of 167.8 lb for WNBA players (95% PI = 141.0, 194.6) and 147.4 lb for WTA players (95% PI = 120.7, 174.1). These predicted values are descriptive reference estimates derived from the observed data; they could be interpreted as typical weights for the condition. 
| Sport | Height (cm) | Expected Weight (lb) | Lower (PI) | Upper (PI) |
|------|-------------:|---------------------:|-----------:|-----------:|
| WNBA | 170 | 141.09 | 114.11 | 168.08 |
| WNBA | 175 | 154.44 | 127.91 | 180.97 |
| WNBA | 180 | 167.79 | 140.96 | 194.62 |
| WNBA | 185 | 181.14 | 153.26 | 209.02 |
| WTA  | 170 | 128.89 | 101.98 | 155.80 |
| WTA  | 175 | 138.14 | 111.62 | 164.65 |
| WTA  | 180 | 147.39 | 120.69 | 174.09 |
| WTA  | 185 | 156.64 | 129.19 | 184.08 |

## Summary
Across multiple methods—BMI comparisons, multivariate height–weight testing, and height-controlled regression in the overlap range—WNBA athletes consistently show larger body-size measures than WTA Top 100 athletes. BMI in particular cannot distinguish lean mass from fat mass, and basketball roles/positions likely contribute to variation in weight at a given height. The bottom line is that there is no guarantee that a certain height and weight can or cannot make it to the WTA TOP 100 or WNBA. Being an elite athlete takes a lot more than just manage yout body-size, it would be helpful to see if you are on the right track. :)
