I have every variable / the means to create every variable from the https://www.researchgate.net/publication/338728435_Forecasting_college_football_game_outcomes_using_modern_modeling_techniques paper. Also, I'm choosing to model the second most important variable (home / away) with dimensions like flight arrival time or distance, change in evelation / temp / conditions, stadium buckets to discern high noise, high intensity stadiums.

Converted json data to a pandas dataframe then converted to sql. I could have used NoSQL but I don't want to waste my time learning the syntax.

Looking around at other scholarly articles:
https://www.sciencedirect.com/science/article/pii/S2772662223001364

7 years of data makes more sense than 5, getting two more years is a good idea.

I am using talent as a proxy for recruitment and transfer portal data - but, I'm not sure. 

I don't have a way to model injuries yet


Steps left on data gathering:
Get weather data from another API that allows for lat and lon specification of stadium

Get arrival flight time instead of distance (jet streams can add an hour plus to a flight)

 --- look into flight trackers to see if arrival time before game is significant
 
Maybe include stadium name or stadium buckets for noise and psychological effects

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

General ideas:

Talk to friend about automating periodic update scripts regularly through the terminal

conduct ex-post vs ex-ante analysis to test weather forecasts and other forecasts

Find optimal number of seasons to include in model ?

Use PCA with Lasso, reduce variables with stepwise selection, use decision tree importance vs randon number generator to find important variables

Develop hedging strategy

Validate tables in database

Find a way to discern between sharp and public movement

Find a way to discern between high-confidence and low-confidence predictions

post dashboard to personal website or new website (if new website, use ADO for username and password authentication, paywall some features)

# College Football Prediction Model

College Football database currently contains **18 tables**

These tables are named Games24, Games23, Games22, Games21, Games20, AdvancedSeasonGameStat24, AdvancedSeasonGameStat23, AdvancedSeasonGameStat22, AdvancedSeasonGameStat21, AdvancedSeasonGameStat20, fbsTeams, bets24, bets23, bets22, bets21, bets20, and coachHist

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Games
id column is game_id in other tables
Columns: index|id|home_team|away_team|away_points|home_points

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### AdvancedSeasonGameStat
AdvancedSeasonGameStat24 has to be updated regularly. It's last update was on Saturday night so it is missing games that ended late Saturday.
Columns: index|game_id|team_id|team_name|home_away|conference|points|rushingTDs|puntReturnYards|puntReturnTDs|puntReturns|passingTDs|kickReturnYards|kickReturnTDs|kickReturns|kickingPoints|interceptionYards|interceptionTDs|passesIntercepted|fumblesRecovered|totalFumbles|tacklesForLoss|defensiveTDs|tackles|sacks|qbHurries|passesDeflected|possessionTime|interceptions|fumblesLost|turnovers|totalPenaltiesYards|yardsPerRushAttempt|rushingAttempts|rushingYards|yardsPerPass|completionAttempts|netPassingYards|totalYards|fourthDownEff|thirdDownEff|firstDowns

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### fbsTeams
id column is team_id in other tables
Columns: index|id|school|conference|division|elevation|capacity|latitude|longitude|grass|dome

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### bets

Columns:
bets24 has to be updated regularly. 
index|game_id|season|season_type|week|start_date|away_team|away_conference|away_score|home_team|home_conference|home_score|provider0|formatted_spread0|spread0|over_under0|provider1|formatted_spread1|spread1|over_under1|provider2|formatted_spread2|spread2|over_under2

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### coachHist

Columns: 
index|INTEGER|0||0
1|first_name|TEXT|0||0
2|hire_date|TEXT|0||0
3|season_type|TEXT|0||0
4|year|REAL|0||0
5|games|REAL|0||0
6|losses|REAL|0||0
7|postseason_rank|REAL|0||0
8|preseason_rank|REAL|0||0
9|school|TEXT|0||0
10|sp_defense|REAL|0||0
11|sp_offense|REAL|0||0
12|sp_overall|REAL|0||0
13|games0|REAL|0||0
14|losses0|REAL|0||0
15|postseason_rank0|REAL|0||0
16|preseason_rank0|REAL|0||0
17|school0|TEXT|0||0
18|sp_defense0|REAL|0||0
19|sp_offense0|REAL|0||0
20|sp_overall0|REAL|0||0
21|games1|REAL|0||0
22|losses1|REAL|0||0
23|postseason_rank1|REAL|0||0
24|preseason_rank1|REAL|0||0
25|school1|TEXT|0||0
26|sp_defense1|REAL|0||0
27|sp_offense1|REAL|0||0
28|sp_overall1|REAL|0||0

----------------------------------------------------------------------------------------------------------------------------

### talent20s

2020,2021,2022,2023,2024 talent team composite scores
may not be granual enough, have to look into how athletes are scored, hoping this cans serve as a proxy for transfer and recruiting, it may have limitations though depending on player usage

Columns
index|team|talent|year

----------------------------------------------------------------------------------------------------------------------------
