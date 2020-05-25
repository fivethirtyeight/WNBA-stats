# WNBA-stats

This repo contains player advanced stats and Elo ratings for WNBA history.

## Player Stats ##

The file `wnba-player-stats.csv` contains season-level advanced stats for WNBA players by team for the 1997-2019 seasons, from [Basketball-Reference.com](https://www.basketball-reference.com/). It also contains my own `Composite Rating`, which blends PER and Win Shares per 40 into a single metric that mimics [RAPTOR player ratings](https://fivethirtyeight.com/features/introducing-raptor-our-new-metric-for-the-modern-nba/).


|     Category     |                           Description                           |
|------------------|-----------------------------------------------------------------|
| player_ID        | BB-Ref player ID                                                |
| Player           | Player name                                                     |
| year_ID          | Season                                                          |
| Age              | Age (as of Jul. 1)                                              |
| Tm               | Team played for                                                 |
| tm_gms           | Team's scheduled games                                          |
| Tm_Net_Rtg       | Team's net efficiency (offensive rating minus defensive rating) |
| Pos              | Player's position played                                        |
| G                | Games played                                                    |
| MP               | Minutes played                                                  |
| MP_pct           | Percentage of available minutes played                          |
| PER              | Player Efficiency Rating                                        |
| TS_pct           | True Shooting Percentage                                        |
| ThrPAr           | Three-point Attempt Rate (3PA/FGA)                              |
| FTr              | Free Throw Rate (FTA/FGA)                                       |
| ORB_pct          | Offensive rebound percentage                                    |
| TRB_pct          | Total rebound percentage                                        |
| AST_pct          | Assist percentage                                               |
| STL_pct          | Steal percentage                                                |
| BLK_pct          | Block percentage                                                |
| TOV_pct          | Turnover percentage                                             |
| USG_pct          | Usage percentage                                                |
| OWS              | Offensive Win Shares                                            |
| DWS              | Defensive Win Shares                                            |
| WS               | Total Win Shares                                                |
| WS40             | Win Shares per 40 minutes                                       |
| Composite_Rating | Estimated net points added per 100 possessions                  |
| Wins_Generated   | Wins implied by Composite Rating                                |

Composite Rating is determined by the following formula (based on NBA player stats):

`Rating = -5.237248 + 0.1741241*PER + 26.0059929*WS40`

Individual ratings are then adjusted so the team's weighted average Composite Rating (times 4.064, a scalar to account for score effects) equals the team's Net Rating. Wins Generated are derived by divvying up the team's Net Rating-implied wins according to each player's contribution to the team's Net Rating.

## Elo Ratings ##

The file `wnba-team-elo-ratings.csv` contains Elo Ratings for every team in WNBA history on a game-by-game basis. The ratings were developed by FiveThirtyEight's Jay Boice, similar to the [basic ratings for the NBA](https://projects.fivethirtyeight.com/complete-history-of-the-nba/). The ratings change after every game based on the winner's pregame win probability, with more unexpected wins resulting in more points shifting from the loser's rating to the winner's.


| Category  |             Decription              |
|-----------|-------------------------------------|
| season    | Year of game                        |
| date      | Date of game                        |
| team1     | First team listed's ID              |
| team2     | Second team listed's ID             |
| name1     | Team1's full name                   |
| name2     | Team2's full name                   |
| neutral   | Was game at a neutral site? (1=yes) |
| playoff   | Was game in playoffs? (1=yes)       |
| score1    | Team1's points in game              |
| score2    | Team2's points in game              |
| elo1_pre  | Team1's pregame Elo rating          |
| elo2_pre  | Team2's pregame Elo rating          |
| elo1_post | Team1's postgame Elo rating         |
| elo2_post | Team2's postgame Elo rating         |
| prob1     | Team1's pregame odds of winning     |
| is_home1  | Was Team1 the home team? (1=yes)    |


Some other pertinent information about WNBA Elo ratings:

* Home court advantage is 80 (NBA=100)
* K-factor is 32 (NBA=20)
* Teams are reverted by 1/2 between seasons (NBA=1/4)
* In playoffs, elo difference is multiplied by 1.25
* Margin of victory -- relative to expectation -- matters, same as NBA
* Expansion teams start at 1300

There were five teams that moved to different cities over the years; in those cases, ratings were carried over from the previous team:

* 2003: ORL -> CON
* 2003: UTA -> SAS
* 2010: DET -> TUL
* 2016: TUL -> DAL
* 2018: SAS -> LVA

