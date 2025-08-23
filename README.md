# US Ryder Cup Team Selection 2025 - Case Study

This project aims to determine the best candidates to be selected for the US Ryder Cup Team for 2025 by analyzing golfer data for the year.

## Data Source

This data was scraped from ESPN's website using Python. Specifically, data was collected on the top PGA tour players' performance in golf tournaments from the beginning of the 2020 season, in September, to August 2025. The data used for final selection is from the 2025 season.
This data includes fields such as total Earnings, Fedex Cup Points, and individual statistics.

## Methodology

Several techniques were used to identify top candidates, including:
* Data Cleaning: I cleaned the data to remove missing or inaccurate data points and ensure consistency. 
* Exploratory Data Analysis: I conducted data analysis to understand the distribution of the data and identify any outliers or anomalies.
* Feature Engineering: I created new features, such as win percentage per event, to better capture golfer performance.
* Weighted scoring: I developed a scaled scoring model that normalizes key performance metrics and statistical data, allowing for the calculation of numerical scores to rank players consistently across all categories.

## Results

The Ryder Cup team is comprised of twelve golfers total. Six golfers automatically qualify on total Fedex points. 
The other six golfers are picked by the Ryder Cup captain.

As of August 23, 2025:

Auto Qualify:

| Name | Points | 
| --------------- | --------------- |
| Scottie Scheffler | 7,456 | 
| J.J. Spaun | 3,493 | 
| Ben Griffin| 2,798 | 
| Russell Henley | 2,795 | 
| Maverick McNealy | 2,547 | 
| Harris English | 2,512 | 


Top 10 Selections:

| Rank | Name            | Earnings  | Events | Rnds | Cuts | Top10 | Wins | Score | DDIS  | DACC | GIR  | PUTTS | Points/Event | Top10% | Wins% |
| ---- | --------------- | --------- | ------ | ---- | ---- | ----- | ---- | ----- | ----- | ---- | ---- | ----- | ------------ | ------ | ----- |
| 1    | Justin Thomas   | 9,761,829 | 19     | 72   | 18   | 7     | 1    | 69.8  | 304.9 | 53.7 | 65.4 | 1.683 | 130.37       | 36.8%  | 5.3%  |
| 2    | Keegan Bradley  | 7,581,145 | 20     | 76   | 19   | 5     | 1    | 70.1  | 306.2 | 61.4 | 65.9 | 1.746 | 99.60        | 25.0%  | 5.0%  |
| 3    | Collin Morikawa | 7,302,227 | 18     | 64   | 16   | 4     | 0    | 70.1  | 296.5 | 70.7 | 68.8 | 1.747 | 91.94        | 22.2%  | 0.0%  |
| 4    | Patrick Cantlay | 5,052,606 | 18     | 66   | 16   | 4     | 0    | 70.0  | 305.4 | 59.3 | 69.9 | 1.739 | 92.28        | 22.2%  | 0.0%  |
| 5    | Sam Burns       | 5,564,815 | 23     | 86   | 21   | 5     | 0    | 69.7  | 307.2 | 60.6 | 66.4 | 1.715 | 81.35        | 21.7%  | 0.0%  |
| 6    | Cameron Young   | 5,991,646 | 23     | 79   | 17   | 6     | 1    | 70.3  | 313.5 | 53.8 | 63.5 | 1.711 | 94.96        | 26.1%  | 4.3%  |
| 7    | Kurt Kitayama   | 3,360,156 | 22     | 66   | 14   | 4     | 1    | 69.3  | 318.1 | 56.1 | 67.4 | 1.725 | 59.00        | 18.2%  | 4.5%  |
| 8    | Chris Gotterup  | 4,101,304 | 26     | 83   | 17   | 3     | 1    | 69.4  | 316.7 | 54.2 | 70.3 | 1.761 | 54.38        | 11.5%  | 3.8%  |
| 9    | Brian Harman    | 4,977,660 | 22     | 83   | 20   | 4     | 1    | 70.4  | 295.0 | 63.2 | 65.3 | 1.763 | 78.86        | 18.2%  | 4.5%  |
| 10   | Akshay Bhatia   | 4,154,687 | 23     | 77   | 18   | 4     | 0    | 70.0  | 298.1 | 61.8 | 67.6 | 1.724 | 61.26        | 17.4%  | 0.0%  |

# Scoring Methodology

## 1. 📊 Statistical Score

This score is based on a player's in-game statistics. Each stat was normalized using MinMaxScaler, then weighted according to its predictive importance.

### Metrics Used:

- Score (inverted, lower is better)  
- GIR (Greens in Regulation)  
- DDIS (Driving Distance)  
- DACC (Driving Accuracy)  
- BIRDS (Birdies)  
- PUTTS (inverted)  

### Weighting:

- Score – 30%  
- GIR – 30%  
- DDIS – 15%  
- DACC – 15%  
- BIRDS – 5%  
- PUTTS – 5%  

---

## 2. 🏆 Performance Score

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


| Player Name     | Statistical Score | Performance Score | Total Score |
| --------------- | ----------------- | ----------------- | ----------- |
| Justin Thomas   | 5.97              | 9.45              | 7.71        |
| Keegan Bradley  | 6.00              | 6.63              | 6.31        |
| Collin Morikawa | 7.09              | 5.14              | 6.11        |
| Patrick Cantlay | 6.96              | 5.01              | 5.99        |
| Sam Burns       | 6.88              | 4.88              | 5.88        |
| Cameron Young   | 4.84              | 6.50              | 5.67        |
| Kurt Kitayama   | 7.58              | 3.16              | 5.37        |
| Chris Gotterup  | 7.99              | 2.67              | 5.33        |
| Brian Harman    | 5.09              | 4.79              | 4.94        |
| Akshay Bhatia   | 6.43              | 3.02              | 4.72        |


## Conclusion
Based on the analysis, the recommendation is that US Ryder Cup Captain, Keegan Bradley, selects the following players. Justin Thomas is a key outlier and is the highest confidence pick. Keegan Bradley should also elect himself (as a player and captain). Strong contenders include Collin Morikawa and Patrick Cantlay, both of which have Ryder Cup experience. Both Morikawa and Cantlay posted strong total scores without a single win in the 2025 season. The model elects Sam Burns and Cameron Young for the fifth and sixth positions. However, these positions are more contentional. Cameron Young has not the lowest stats in the group, but has been playing notably strong to finish the season. 

