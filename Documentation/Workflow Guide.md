
# Step-By-Step Workflow Guide:

We have to analyze to find the best players to be in our cricket team.

1. We start with doing webscrapping on [ESPNCricinfo](https://www.espncricinfo.com/) site using [bright data](https://brightdata.com/) , a web data collector website. we use these four js code on bright datac collector to get four JSON files, named as follows:

    A. [t20_wc_batting_summary.js](https://github.com/prashantsingh8962/Webscraping_Cricket_Analysis/blob/main/Web_Scrapping_Code/t20_wc_batting_summary.js)<br>
    B. [t20_wc_bowling_summary.js](https://github.com/prashantsingh8962/Webscraping_Cricket_Analysis/blob/main/Web_Scrapping_Code/t20_wc_bowling_summary.js)<br>
    C. [t20_wc_match_results.js](https://github.com/prashantsingh8962/Webscraping_Cricket_Analysis/blob/main/Web_Scrapping_Code/t20_wc_match_results.js)<br>
    D. [t20_wc_player_info.js](https://github.com/prashantsingh8962/Webscraping_Cricket_Analysis/blob/main/Web_Scrapping_Code/t20_wc_player_info.js)<br>


2. The four extracted JSON files are as named below:

   A. [t20_wc_batting_summary.json](https://github.com/prashantsingh8962/Webscraping_Cricket_Analysis/blob/main/Json%20Code/t20_wc_batting_summary.json)<br>
   B. [t20_wc_bowling_summary.json](https://github.com/prashantsingh8962/Webscraping_Cricket_Analysis/blob/main/Json%20Code/t20_wc_bowling_summary.json)<br>
   C. [t20_wc_match_results.json](https://github.com/prashantsingh8962/Webscraping_Cricket_Analysis/blob/main/Json%20Code/t20_wc_match_results.json)<br>
   D. [t20_wc_player_info.json](https://github.com/prashantsingh8962/Webscraping_Cricket_Analysis/blob/main/Json%20Code/t20_wc_player_info.json)<br>

 
3. After web scrapping, we did some data preprocessing in Pandas-python. And convert JSON to CSV files.

    [Python Code](https://github.com/prashantsingh8962/Webscraping_Cricket_Analysis/blob/main/Python%20Code/t20_data_preprocessing.ipynb)

4. We fetched data in Power BI and started building dashboards
