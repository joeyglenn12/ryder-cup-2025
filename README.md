# US Ryder Cup Team Selection 2025 - Case Study

This project aims to determine the best candidates to be selected for the US Ryder Cup Team for 2025 by analyzing golfer data for the year.

## Data Source

This data was scraped from ESPN's website using Python. Specifically, data was collected on the top PGA tour players' performance in golf tournaments from the beginning of the 2020 season, in September, to August 2025. The data used for final selection is from the 2025 season.
This data includes fields such as total Earnings, Fedex Cup Points, and individual statistics.

## Methodology

Several techniques were used to identify top candidates, including:
* Data Cleaning: Cleaned the data to remove missing or inaccurate data points and ensure consistency. 
* Exploratory Data Analysis: Conducted data analysis to understand the distribution of the data and identify any outliers or anomalies.
* Feature Engineering: Created new features, such as win percentage per event, to better capture golfer performance.
* Weighted Scoring: Developed a scaled scoring model that normalizes key performance metrics and statistical data, allowing for the calculation of numerical scores to rank players consistently across all categories.

## Results

The Ryder Cup team is comprised of twelve golfers total. Six golfers automatically qualify on total Fedex points. 
The other six golfers are picked by the Ryder Cup captain, Keegan Bradley.

As of August 25, 2025:

Auto Qualify:

| Name | Points | 
| --------------- | --------------- |
| Scottie Scheffler | 37,180 | 
| J.J. Spaun | 14,851 | 
| Xander Schauffele | 13,733 | 
| Russell Henley | 12,276 | 
| Harris English | 10,880 | 
| Bryson DeChambeau | 10,774 | 
Source: https://www.rydercup.com/rankings

Top 10 Selections based on 2025 performance (not Ryder Cup points):

| Rank | Name              | Earnings  | Events | Rnds | Cuts | Top10 | Wins | Score | DDIS  | DACC | GIR  | PUTTS | Points/Event | Top10% | Wins% |
|------|-------------------|-----------|--------|------|------|-------|------|--------|--------|------|------|--------|----------------|--------|--------|
| 1    | Justin Thomas     | 10,883,495| 20     | 76   | 18   | 8     | 1    | 69.6   | 305.2  | 54.0 | 65.5 | 1.679  | 123.85         | 40.0%  | 5.0%   |
| 2    | Ben Griffin       | 9,990,352 | 28     | 96   | 21   | 10    | 2    | 69.4   | 305.5  | 59.1 | 68.5 | 1.745  | 99.93          | 35.7%  | 7.1%   |
| 3    | Maverick McNealy  | 8,207,075 | 24     | 88   | 20   | 7     | 0    | 69.9   | 306.4  | 58.9 | 67.4 | 1.750  | 106.13         | 29.2%  | 0.0%   |
| 4    | Keegan Bradley    | 8,702,812 | 21     | 80   | 19   | 6     | 1    | 69.9   | 306.4  | 61.4 | 66.0 | 1.742  | 94.86          | 28.6%  | 4.8%   |
| 5    | Cameron Young     | 8,608,313 | 24     | 83   | 17   | 7     | 1    | 70.1   | 313.6  | 54.5 | 63.7 | 1.705  | 91.00          | 29.2%  | 4.2%   |
| 6    | Patrick Cantlay   | 9,405,106 | 19     | 70   | 16   | 5     | 0    | 69.8   | 306.1  | 59.9 | 70.0 | 1.730  | 87.42          | 26.3%  | 0.0%   |
| 7    | Collin Morikawa   | 7,754,727 | 19     | 68   | 16   | 4     | 0    | 70.0   | 296.8  | 71.0 | 68.9 | 1.745  | 87.11          | 21.1%  | 0.0%   |
| 8    | Sam Burns         | 6,686,482 | 24     | 90   | 21   | 6     | 0    | 69.6   | 307.4  | 60.7 | 66.0 | 1.711  | 77.96          | 25.0%  | 0.0%   |
| 9    | Chris Gotterup    | 4,816,304 | 27     | 87   | 17   | 4     | 1    | 69.3   | 316.9  | 54.9 | 70.4 | 1.757  | 52.37          | 14.8%  | 3.7%   |
| 10   | Kurt Kitayama     | 3,360,156 | 22     | 66   | 14   | 4     | 1    | 69.3   | 318.1  | 56.1 | 67.4 | 1.725  | 59.00          | 18.2%  | 4.5%   |


# Scoring Methodology

## 1. 📊 2025 Statistical Rating

This rating is based on a player's statistics for the 2025 season. Each stat was normalized using MinMaxScaler, then weighted according to its importance.

### Metrics Used:

- Score (inverted, lower is better)  
- GIR (Greens in Regulation)  
- DDIS (Driving Distance)  
- DACC (Driving Accuracy)  
- BIRDS (Birdies)  
- PUTTS (inverted, lower is better)  

### Weighting:

- Score – 30%  
- GIR – 30%  
- DDIS – 15%  
- DACC – 15%  
- BIRDS – 5%  
- PUTTS – 5%  

---

## 2. 🏆 2025 Performance Rating

This score reflects how a player performs in tournaments. Metrics were scaled and weighted accordingly:

### Metrics Used:

- Points per Event  
- Top 10 Finishes  
- Wins (with additional bonus)  
- Earnings  
- Cuts Made  

### Weighting:

- Points per Event – 40%  
- Top 10s – 20%  
- Wins – 30% + bonus  
- Earnings – 5%  
- Cuts – 5%  

---

## 3. 🧮 Total Score

A final `total_score` is calculated as a weighted average of the two previous scores:
total_score = 0.5 * statistical_score + 0.5 * performance_score


| Player Name        | Statistical Score | Performance Score | Total Score |
|--------------------|-------------------|--------------------|-------------|
| Ben Griffin        | 7.50              | 8.33               | 7.92        |
| Justin Thomas      | 6.27              | 9.00               | 7.63        |
| Maverick McNealy   | 6.24              | 6.95               | 6.59        |
| Keegan Bradley     | 6.26              | 6.43               | 6.34        |
| Patrick Cantlay    | 7.35              | 5.11               | 6.23        |
| Collin Morikawa    | 7.25              | 4.77               | 6.01        |
| Sam Burns          | 6.87              | 4.70               | 5.79        |
| Cameron Young      | 5.19              | 6.30               | 5.74        |
| Chris Gotterup     | 8.19              | 2.70               | 5.44        |
| Kurt Kitayama      | 7.51              | 2.96               | 5.23        |


## Conclusion
Based on the analysis, the recommendation is that US Ryder Cup Captain, Keegan Bradley, selects the following players:
1. Ben Griffin - Leads the table in statistical score with two wins this season (Zurich and Scwhab).
2. Justin Thomas - Won RBC Heritage and placed in the top 10 eight times.
3. Maverick McNealy - No wins but signficant performances. Second at The Genesis and third at Valero, RBC, and the BMW Championship.
4. Keegan Bradley - Win at the Traveler's. Keegan Bradley should attend the cup (as a player AND captain). 
5. Patrick Cantlay - No wins this year, but all around strong player with Ryder Cup experience.
6. Collin Morikawa - The most accurate player off the tee and the third highest GIR % in the group. Ryder cup experience is a plus. 
