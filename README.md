# Cricket Team Player Analysis

This project involves analyzing cricket player performance data to identify the best players for team selection. The workflow consists of web scraping, data preprocessing, and visualization.

## Table of Contents

1. [Workflow Overview](#workflow-overview)
2. [Web Scraping](#web-scraping)
3. [Data Preprocessing](#data-preprocessing)
4. [Power BI Dashboard](#power-bi-dashboard)
5. [Measures and Calculated Columns](#measures-and-calculated-columns)


## Workflow Overview

The analysis follows these steps:

1. **Web Scraping**: Collect data from ESPN Cricinfo using Bright Data.
2. **Data Preprocessing**: Clean and convert data into usable formats.
3. **Visualization**: Create dashboards in Power BI for insights.

## Web Scraping

We extracted data from the [ESPNCricinfo](https://www.espncricinfo.com/) website using the following JavaScript files via [Bright Data](https://brightdata.com/):

- **Batting Summary**: [t20_wc_batting_summary.js](https://github.com/prashantsingh8962/Webscraping_Cricket_Analysis/blob/main/Web_Scrapping_Code/t20_wc_batting_summary.js)
- **Bowling Summary**: [t20_wc_bowling_summary.js](https://github.com/prashantsingh8962/Webscraping_Cricket_Analysis/blob/main/Web_Scrapping_Code/t20_wc_bowling_summary.js)
- **Match Results**: [t20_wc_match_results.js](https://github.com/prashantsingh8962/Webscraping_Cricket_Analysis/blob/main/Web_Scrapping_Code/t20_wc_match_results.js)
- **Player Info**: [t20_wc_player_info.js](https://github.com/prashantsingh8962/Webscraping_Cricket_Analysis/blob/main/Web_Scrapping_Code/t20_wc_player_info.js)

The resulting JSON files are:

- [Batting Summary JSON](https://github.com/prashantsingh8962/Webscraping_Cricket_Analysis/blob/main/Json%20Code/t20_wc_batting_summary.json)
- [Bowling Summary JSON](https://github.com/prashantsingh8962/Webscraping_Cricket_Analysis/blob/main/Json%20Code/t20_wc_bowling_summary.json)
- [Match Results JSON](https://github.com/prashantsingh8962/Webscraping_Cricket_Analysis/blob/main/Json%20Code/t20_wc_match_results.json)
- [Player Info JSON](https://github.com/prashantsingh8962/Webscraping_Cricket_Analysis/blob/main/Json%20Code/t20_wc_player_info.json)

## Data Preprocessing

Data preprocessing was conducted using Pandas in Python. The extracted JSON files were cleaned and converted into CSV format.

- [Data Preprocessing Code](https://github.com/prashantsingh8962/Webscraping_Cricket_Analysis/blob/main/Python%20Code/t20_data_preprocessing.ipynb)

## Power BI Dashboard

We utilized Power BI to create dashboards for visualizing player performance metrics based on the preprocessed data.

### Measures Created

| Sno | Measures                     | Description                                           | DAX Formula                                                                 | Table                     |
|-----|------------------------------|------------------------------------------------------|-----------------------------------------------------------------------------|---------------------------|
| 1   | Total Runs                   | Total runs scored by the batsman                     | `Total Runs = SUM(fact_batting_summary[runs])`                           | fact_batting_summary      |
| 2   | Total Innings Batted         | Total innings a batsman got to bat                   | `Total Innings Batted = COUNT(fact_batting_summary[match_id])`            | fact_batting_summary      |
| 3   | Total Innings Dismissed      | Number of innings batsman got out                    | `SUM(fact_batting_summary[out])`                                          | fact_batting_summary      |
| ... | ...                          | ...                                                  | ...                                                                         | ...                       |

### Calculated Columns Created

| Sno | Calculated Column Name       | Description                                            | DAX Formula                                                             | Table         |
|-----|------------------------------|-------------------------------------------------------|-------------------------------------------------------------------------|---------------|
| 1   | Boundary Runs                | Total runs scored by hitting fours and sixes         | `boundary runs = fact_batting_summary[fours]*4 + fact_batting_summary[sixes]*6` | fact_batting_summary |
| 2   | Custom Batting Order         | Assign batting order to potential final 11           | `SWITCH(TRUE(), ...)`                                                  | dim_player    |


Feel free to contribute to this project or explore the code and data files! For any questions, please open an issue on GitHub.
