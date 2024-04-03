---
layout: post
title:  "Picking an FPL Team"
date:   2024-02-10 17:35:51 +0000
categories: jekyll update
---

One of the most challenging aspects of testing the performance of my models is calculating the best combination of players for any given gameweek. 
This is a result of the many parameters which, whilst restricting the search space, make optimising this process particuarly difficult. 

In a given gameweek there are approximately 640 footballers, split across 20 teams and 4 positions. The aim is to find the combination of 15 players (including 4 substitutes)
who will score the most number of points. However, the following restrictions exist:
- Positional requirements:
  * 2 Goalkeepers
  * 5 Defenders
  * 5 Midfielders 
  * 3 Forwards
- No more than 3 players from any team
- Total cost less than 1000

The aim is to optimise for the highest number of predicted points whilst fitting into these constraints. It is, of course, practically impossible to examine every possibilty.
As such, I followed the following process, the implementation of which be found [here]('https://github.com/bencecsiba/FPL-Predictor/blob/main/Models/Test/test_by_season_cache.pyy'):
1. Restricting the players searched to 6 goalkeepers, 10 defenders, 10 midfielders and 7 forwards.
2.  Picking the following players in turn:
    - 2 goalkeepers
    - 5 defenders
    - 5 Midfielders
    - 3 Forwards
3. Storing the predicted number of points scored by such a team if it is the largest found thus far and the total cost is below 1000. 
4. Steps 2 and 3 are iterated through every combination. 

This search space is still too large, so at every step, the following was also done:
- Only proceeding with a combination in a certain position if either the cost was lower and/or the predicted number of points was higher than that of the corresponding set of the current best team.
- Once the total cost and total predicted points were calculated for a given set, storing these values in a cache to avoid repitition.
- Only proceeding if the maximum number of players from any one club had not exceeded 3 for the players picked thus far. 

Some other points to note:
- The order of positions searched was deliberate: they were sorted by the variance in points scored, from smallest to largest, i.e. finding the best combination of forwards is more important than goalkeepers for the final score
- A limit of 20 minutes to find such a team was imposed; in the rare case it took longer than 20 mins, the best team at that time was kept. 
