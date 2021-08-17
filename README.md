# SF_NBA
## _Simulate and Forecast NBA Games Quickly and Efficiently_

SF_NBA is a Python library for simulating NBA games between custom teams and for forecasting NBA player stats in future games. SF_NBA uses high-performing machine learning models trained on Basketball-Reference data from nearly every player who has played in a basketball game since 1970. See paper for details and citations. 

- Decide whether to forecast or simulate
- Call the respective class
- Pick your favorite NBA player(s)
- Run the Python code in your preferred code-editor. 
- Get results in seconds!


## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install SF_NBA.

```bash
pip install sf_nba
```

## NBAGamesSimulator
Here's a brief documentation of using NBAGamesSimulator to simulate a custom NBA match. Simulate a 48 minute NBA game in just 4 lines of code!

### Example Usage
```python
from sf_nba.NBAGamesSimulator import NBAGamesSimulator

# input player data
bot = NBAGamesSimulator('Alex Caruso', 32, 2020, 'Kentavious Caldwell-Pope', 36, 2020, 'Kawhi Leonard', 35, 2012, 'Kyle Kuzma', 35, 2018, 'Damian Jones', 35, 2020, 'Ben Simmons', 8, 2021,'PG', 'DeMar DeRozan', 10, 2015, 'SG', 'Danny Green', 13, 2021, 'SF', 'Karl Malone', 13, 2004, 'PF', 'Bob Lanier', 13, 1973, 'C', 'Muggsy Bogues', 8, 1989, 'PG', 'Michael Jordan', 2, 1997, 'SG', 'Stephen Curry', 32, 2017, 'James Harden', 36, 2020, 'LeBron James', 35, 2017, 'Larry Nance Jr.', 35, 2016, 'Zaid Abdul-Aziz', 35, 1971, 'Chris Paul', 8, 2020,'PG', 'Kobe Bryant', 10, 2015, 'SG', 'Joe Harris', 13, 2020, 'SF', 'Dwight Howard', 13, 2005, 'PF', 'Kevin Love', 13, 2018, 'C', 'Kyrie Irving', 8, 2021, 'PG', 'Michael Jordan', 2, 1998, 'SG')

#simulate nba game
bot.simulate()

#display simulation results
bot.results()
```

### .simulate()
| Parameter Name        | Type           | Description  |
| ------------- |:-------------:| -----:|
| reg  | str, default = 'reg' | Regression model trained on each player dataframe. Options include: 'lreg' = Ordinary least squares Linear Regression, 'lasso' = Lasso Regression, 'ridge' = Ridge Regression. |
| hyp_tuning | bool, default = False      |  If reg = 'ridge' or 'lasso', tunes the alpha hyperparameter using RandomizedSearchCV |
| verbose | int, default = 0      |   Whether or not to show the hyperparameter tuning process. verbose = 0 shows nothing. The higher the verbose,the more messages shown.|
| n_iter | int, default = 100      | Number of parameter settings that are sampled for RandomizedSearchCV.  |
| cv | int, default = 3      |    Determines fold of cross-validation. |
| random_state | int, default = 42      |    Ensures random unified splitting. |
| n_jobs | int, default = -1      |    Number of jobs to run in parallel. |

### .results()
| Parameter Name        | Type           | Description  |
| ------------- |:-------------:| -----:|
| table      | str, default = 'None' | Displays simulation results. Options include: 'None' = team 1 score vs team 2 score, 'team_1_dataframe' = Box Score for Team 1, 'team_2_dataframe' = Box Score for Team 2 |

## NextXGamesForecast
Here's a brief documentation of using NextXGamesForecast. NextXGamesForecast uses a univariate Bidirectional LSTM for time-series forecasting. Forecast any statistic(Points, Rebounds, Assist, etc.) for any player for any number of future games in just 4 lines of code!

### Example Usage
```python
from sf_nba.NextXGamesForecast import NextXGamesForecast

#Select Player and Stat to Forecast. In this case Michael Jordan is selected and Points per Game is tracked.
forecast = NextXGamesForecast('Michael Jordan')

#Forecast PPG for Michael Jordan for 10 games 
forecast.simulate(10, verbose = 1, test_loss = True, loss_curve= True)

#Display results
forecast.results()
```
### Parameters
| Parameter Name        | Type           | Description  |
| ------------- |:-------------:| -----:|
| player_name      | str | Player Name |
| stat      | str, default = 'PTS'      |   Stat to forecast. Options include: 'PTS', 'AST', 'TRB', 'ORB', 'DRB', 'FG', 'FGA', 'FG%', 'FT', 'FTA', 'FT%', '3P', '3PA', '3P%', 'STL', 'BLK', 'PF', and 'TOV'. |

### .simulate()
| Parameter Name        | Type           | Description  |
| ------------- |:-------------:| -----:|
| next_n_games      | int | Number of games to forecast. |
| epochs     | int, default = 100      |   Number of epochs for training the LSTM |
| verbose     | int, default = 0      |   Whether or not to show the hyperparameter tuning process. verbose = 0 shows nothing. The higher the verbose,the more messages shown. |
| test_loss     | bool, default = False      |   Whether or not to return loss on test data. |
| loss_curve     | bool, default = False      |   Whether or not to display graph of training loss versus the number of epochs. |

### .results()
| Parameter Name        | Type           | Description  |
| ------------- |:-------------:| -----:|
| table      | str, default = 'dataframe' | Either dataframe or plotly visualization. Options include either table = 'dataframe' or table = 'plotly'|
| viz_type      | str, default = 'standard'      |  Type of plotly visualization. Options include table = 'standard', 'future', or 'validate'. 'Standard' shows the past game data and future predictions. 'Future' shows only future predictions. 'Validate' shows past game data, the LSTM's predictions on the past game data, and future predictions.|



## License
MIT
