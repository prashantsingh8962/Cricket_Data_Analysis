
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

## we created these measures:

       Sno	Measures	                                            Description / Purpose	                  DAX FORMULA	TABLE
       1	Total Runs	Total number of runs scored by the batsman	Total Runs = SUM(fact_batting_summary[runs])	fact_batting_summary
   
       2	Total Innings Batted	Total number of innings a batsman got a chance to bat	Total Innings Batted = COUNT(fact_batting_summary[match_id])	fact_batting_summary
   
       3	Total Innings Dismissed	To find the number of innings batsman got out	SUM(fact_batting_summary[out])	fact_batting_summary
   
       4	Batting Average	Average runs scored in an innings	Batting Avg = DIVIDE([Total Runs],[Total Innings Dismissed],0)	fact_batting_summary
				
       5	Total balls Faced	Total number of balls faced by the batsman	total balls faced = SUM(fact_batting_summary[balls])	fact_batting_summary
   
       6	Strike Rate	No of runs scored per 100 balls 	Strike rate = DIVIDE([Total Runs],[total balls faced],0)*100	fact_batting_summary
				
       7	Batting Position	Batting position of a player	Batting Position = ROUNDUP(AVERAGE(fact_batting_summary[batting_pos]),0)	fact_batting_summary
   
       8	Boundary %	Percentage of boundaries scored by the Batsman	Boundary % =  DIVIDE(SUM(fact_batting_summary[Boundary runs]),[Total Runs],0)	fact_batting_summary
   
       9	Avg. balls Faced	Average balls faced by the batter in an innings	AVERAGE(fact_batting_summary[balls])	fact_batting_summary
				
       10	Wickets	Total number of wickets taken by a bowler	wickets = SUM(fact_bowling_summary[wickets])	fact_bowling_summary
   
       11	balls Bowled	Total number of balls bowled by the bowler	balls Bowled = SUM(fact_bowling_summary[balls])	fact_bowling_summary
   
       12	Runs Conceded	Total runs conceded by the bowler	Runs Conceded = SUM(fact_bowling_summary[runs])	fact_bowling_summary
   
       13	Bowling Economy	Average number of runs conceded in an over	Economy = DIVIDE( [Runs Conceded], ([balls Bowled]/6),0)	fact_bowling_summary
   
       14	Bowling Strike Rate	Number of balls bowled per wicket	Bowling Strike Rate = DIVIDE([balls Bowled], [wickets],0)	fact_bowling_summary
   
       15	Bowling Average	No. of runs allowed per wicket  	Bowling Average = DIVIDE([Runs Conceded],[wickets],0)	fact_bowling_summary
				
       16	Total Innings Bowled	Total number of innings bowled by a bowler	Total Innings Bowled = DISTINCTCOUNT(fact_bowling_summary[match_id])	fact_bowling_summary

       17	Dot Ball %	Percentage of dot balls bowled by a bowler	Dot ball % = DIVIDE(SUM(fact_bowling_summary[zeros]), SUM(fact_bowling_summary[balls]),0)	fact_bowling_summary
				
       18	Player Selection	To understand if a player is selected or not	Player Selection = if(ISFILTERED(dim_player[name]),"1","0")
   
       19	Display Text	To display a text of no player is selected	"Display Text = if([Player Selection] = ""1"", "" "" ,""Select Player(s) by clicking 
             the player’s name to see their individual or combined strength."")"
   
       20	Color Callout Value	To display a value only when a player is selected	Color Callout Value = if([Player Selection]="0", "#D0CF1D","#1D1D2E")	
				
				
				
## we created these Calculated Columns:				

     Sno.	Calculated Column Name	Description / Purpose	DAX formula	Table
    1	boundary runs	to find the total number of runs scored by hitting fours and sixes	boundary runs = fact_batting_summary[fours]*4 + fact_batting_summary[sixes]*6	fact_batting_summary
    
    2	Boundary runs bowling	to find the total number of runs conceded by bowlers in boundaries	Boundary runs = fact_bowling_summary[fours]*4 +fact_bowling_summary[Sixes]*6	fact_bowling_summary
    
    3	Custom Batting Order	To assign the batting order to potential final 11	"SWITCH(
    TRUE(),
      dim_player[name] = ""Jos Buttler"",1,
     dim_player[name] = ""Rilee Rossouw"",2,
    dim_player[name] = ""Alex Hales"",2,
    dim_player[name]  = ""Virat Kohli"",3,
    dim_player[name] = ""Suryakumar Yadav"" ,4,
    dim_player[name] = ""Glenn Phillips"" ,5,
    dim_player[name] = ""Marcus Stoinis"" ,6,
    dim_player[name] = ""Glenn Maxwell"" ,6,
    dim_player[name] = ""Sikandar Raza"" ,7,
    dim_player[name] = ""Rashid Khan"" ,8,
    dim_player[name] = ""Shadab Khan"" ,8,
    dim_player[name] = ""Sam Curran"" ,9,
    dim_player[name] = ""Shaheen Shah Afridi"" ,10,
    dim_player[name] = ""Anrich Nortje"" ,11
    )"	dim_player
