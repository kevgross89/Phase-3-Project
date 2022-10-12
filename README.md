# Phase-3-Project

![NFL Combine Picture](https://github.com/kevgross89/Phase-3-Project/blob/main/Images/Header%20Image.jpg)

Author: Kevin Gross

## Project Overview

This project analyzes data from the NFL Scouting Combine from 2009 to 2019 and also collegiate football stats from 2009 to 2013. Both of these datasets were pulled from [Kaggle](https://www.kaggle.com/).

The NFL Scouting Combine is a week-long showcase occurring every February at Lucas Oil Stadium in Indianapolis, where college football players perform physical and mental tests in front of National Football League coaches, general managers, and scouts. With increasing interest in the NFL Draft, the scouting combine has grown in scope and significance, allowing personnel directors to evaluate upcoming prospects in a standardized setting.

Athletes attend by invitation only. An athlete's performance during the combine can affect their draft status and salary, and ultimately their career. The draft has popularized the term "workout warrior", whereby an athlete's "draft stock" is increased based on superior measurable qualities such as size, speed, and strength, despite having an average or sub-par college career.

The data collected at the Combine is in the below categories. [LINK TO COMBINE DATA](https://www.kaggle.com/datasets/redlineracer/nfl-combine-performance-data-2009-2019)

* `Year`: Year of attendance at the NFL combine
* `Player`: Player name
* `Age`: Players age (years)
* `School`: College attended
* `Height`: Height (meters)
* `Weight`: Weight (kilograms)
* `Sprint_40yd`: 40 yard sprint time (seconds)
* `Vertical_Jump`: Vertical jump result (centimeters) 
* `Bench_Press_Reps`: Maximum bench press repetitions achieved while lifting 102.1 kg (225 lb) weight
* `Broad_Jump`: Broad jump result (centimeters)
* `Agility_3cone`: Three-cone agility test time (seconds)
* `Shuttle`: Lateral shuttle time (seconds)
* `Drafted..tm.rnd.yr.`: Team the athlete was drafted by, draft round, draft pick, and year
* `BMI`: Body mass index (kg/m2)
* `Player_Type`: Offensive or defensive player or special teams
* `Position_Type`: Broad classification of the athlete's playing position
* `Position`: Playing position
* `Drafted`: Was the player drafted during the NFL draft?

The second dataset takes game by game stats ranging from 2009 to 2013. These stats included 57 columns of data with items such as the below. [LINK TO NCAA FOOTBALL DATA](https://www.kaggle.com/datasets/mhixon/college-football-statistics)

* `Rush Att`: Amount of rushing attempts
* `Rush Yard`: Amount of rushing yards
* `Rush TD`: Amount of rushing touchdowns
* `Pass Att`: Amount of passing attempts
* `Pass Yard`: Amount of passing yards
* `Pass TD`: Amount of passing touchdowns
* `Pass Int`: Amount of interceptions thrown
* `Tackle Solo`: Amount of solo tackles
* `Sack`: Amount of sacks
* `Fumble Forced`: Amount of fumbles forced

## Buisness Problem

The NFL is a big money, high stakes business and every year the schedule kicks off with their marquee event, the **NFL Draft.** The NFL draft is where collegiate players get selected to one of the 32 teams in the National Football League. Over the course of 3 days, 259 players are selected based on a multitude of factors. The rigorous selection process utilizes millions of dollars and countless hours of analysis all to figure out who will bring the most amount of talent to a team. 

Why is this selection process so intense? According to an article from [Forbes](https://www.forbes.com/sites/davidching/2018/04/18/how-much-do-first-round-busts-cost-nfl-teams-nearly-9-4-million/?sh=1a88c04665ce), "roughly a third of the first-round picks fail to develop into long-term solutions for the teams that select them". Not only that, on average it costs a team $9.4 million per each first round draft pick who has yet to truly pan out. On top of that, the first round draft picks are supposed to be the *locks* meaning they should have a higher hit rate than the players selected in rounds 2 through 7.

Due to this high stakes business, **the stakeholders for this project are all 32 of the teams in the National Football League.** The analysis provided below can help guide NFL teams to make better decisions at the draft based purely on measureable stats.

This project utilizes two datasets. The first from the NFL Scouting Combine and the second from NCAA Football's game stats. Both of these were pulled from Kaggle. The goal of this project is for NFL teams to understand how data can help predict whether a player should or should not be drafted into the NFL, thus hopefully saving a team money down the road.

## Modeling

This project uses 4 types of models to help predict whether or not a player was drafted into the National Football League. Each of these models starts with a basic model with zero hypertuning, and then progresses into multiple iterations of each model using `GridSearchCV`.

### Logistic Regression - [Documentation Here](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html)

Logistic regression is a statistical analysis method to predict a binary outcome, such as yes or no, based on prior observations of a data set. A logistic regression model predicts a dependent data variable by analyzing the relationship between one or more existing independent variables.

### K-Nearest Neighbors - [Documentation Here](https://scikit-learn.org/stable/modules/generated/sklearn.neighbors.KNeighborsClassifier.html)

This algorithm — unlike linear models or tree-based models — does not emphasize learning the relationship between the features and the target. Instead, for a given test record, it finds the most similar records in the training set and returns an average of their target values.

### Decision Trees - [Documentation Here](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html)

Similar to linear models (and unlike kNN), this algorithm emphasizes learning the relationship between the features and the target. However, unlike a linear model that tries to find linear relationships between each of the features and the target, decision trees look for ways to split the data based on features to decrease the entropy of the target in each split.

### Random Forest - [Documentation Here](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)

A random forest is a meta estimator that fits a number of decision tree classifiers on various sub-samples of the dataset and uses averaging to improve the predictive accuracy and control over-fitting. 

## Evaluation

All of these models are evaluated using Testing Accuracy. Accuracy is useful because it allows us to measure the total number of predictions a model gets right, including both True Positives and True Negatives.

Accuracy = $\frac{Number of True Positives + True Negatives}{Total Observations}$

Our *dummy* model had an accuracy of 64.8%, meaning that if it predicted that every player that attended the combine was drafted to the NFL, it would be correct 64.8% of the time. 

Using just data from the NFL combine, our best model was able to have an accuracy of 67.8%, which is a 3% improvement over the dummy model. This model used Logistic Regression with tuned hyperparameters. 

**NFL Combine Models**

| Model Name      |   Accuracy Score |   Precision Score |   Recall Score |   F1 Score |
|:----------------|-----------------:|------------------:|---------------:|-----------:|
| Baseline LogReg |         0.674713 |          0.70088  |       0.858169 |   0.77159  |
| LogReg L1       |         0.678161 |          0.703976 |       0.858169 |   0.773463 |
| LogReg L2       |         0.674713 |          0.70088  |       0.858169 |   0.77159  |
| Baseline KNN    |         0.626437 |          0.665714 |       0.836625 |   0.741448 |
| KNN Model 2     |         0.651724 |          0.650831 |       0.983842 |   0.783417 |
| KNN Model 3     |         0.647126 |          0.662338 |       0.915619 |   0.768651 |
| KNN Model 4     |         0.622989 |          0.657931 |       0.856373 |   0.74415  |
| Baseline DTC    |         0.602299 |          0.69009  |       0.687612 |   0.688849 |
| DTC Model 2     |         0.63908  |          0.641115 |       0.991023 |   0.778561 |
| DTC Model 3     |         0.654023 |          0.652745 |       0.982047 |   0.784229 |
| DTC Model 4     |         0.654023 |          0.670667 |       0.903052 |   0.769702 |
| Baseline RF     |         0.67931  |          0.690934 |       0.903052 |   0.782879 |
| RF Model 2      |         0.650575 |          0.649704 |       0.985637 |   0.783167 |
| RF Model 3      |         0.658621 |          0.657005 |       0.976661 |   0.78556  |

Using data from the NFL combine and NCAA football games, we were able to boost our accuracy of the model to 71%, which is a 3.2% improvement. This model also used Logistic Regression with tuned hyperparameters.

**NCAA Football Stats with NFL Combine Models**

| Model Name      |   Accuracy Score |   Precision Score |   Recall Score |   F1 Score |
|:----------------|-----------------:|------------------:|---------------:|-----------:|
| Baseline LogReg |         0.709977 |          0.757669 |       0.843003 |   0.798061 |
| LogReg L1       |         0.709977 |          0.75     |       0.860068 |   0.801272 |
| LogReg L2       |         0.698376 |          0.753894 |       0.825939 |   0.788274 |
| Baseline KNN    |         0.649652 |          0.708824 |       0.822526 |   0.761453 |
| KNN Model 2     |         0.689095 |          0.700252 |       0.948805 |   0.805797 |
| Baseline DTC    |         0.665893 |          0.763251 |       0.737201 |   0.75     |
| DTC Model 2     |         0.663573 |          0.732704 |       0.795222 |   0.762684 |
| DTC Model 3     |         0.635731 |          0.709877 |       0.784983 |   0.745543 |
| Baseline RF     |         0.696056 |          0.710938 |       0.931741 |   0.806499 |
| RF Model 2      |         0.696056 |          0.697561 |       0.976109 |   0.813656 |

## Conclusion

In conclusion, it is very hard to predict whether a player will be drafted based purely on their combine and collegiate stats. This makes sense for a few intuitive reasons:

1. There is a lot more that goes into whether a player is drafted than purely their physical attributes. For example, a wide reciever can run extremely fast and be extremely agile, but if they can't catch the ball or run the right routes, they will not be drafted.
2. Every position in football is extremely different. Some positions require physical strength while others require more mental ability. Without having mental testing regulations on hand, it is hard to say how someone will perform.
3. The combine invites only the best of the best, meaning that all of these players were the best at their position in college. Sometimes the gap between people is extremely marginal.

With this data, NFL teams can avoid multi-million dollar mistakes by weeding out players from their draft board who should not be drafted. If people in the front office are very adamant about drafting a player who has poor statistics, the data team can show them how people have not been drafted in the past and can be either picked up in free agency or later in the draft.