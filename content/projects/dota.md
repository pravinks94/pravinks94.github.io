---
title: "Dota Win Prediction"
draft: false
url: content/projects/dota.md
github_url: "https://github.com/pravinks94/dota"
image: "https://i.pinimg.com/736x/44/3d/64/443d64c13b59a0c25ee6d1f4d0530579.jpg"
tags: [classification,clustering,rest]
date: 2024-08-04T00:00:00+01:00
descrption: Finding whether the player win prediction based on the adaption of the hero and skill level.
---

# Dota Win Prediction

A model to help understand the win probability of the game based on in-game metrics, skill level, and assistance from the hero pool. The model is also used to find the heroes which the player is comfortable with from the 120+ hero pool. Analysis is done to help users understand their weak points based on the hero pool through Exploratory Data Analysis (EDA).


![Hero Adaption Model](/themes/adritian-free-hugo-theme/assets/images/projects/dota/adoption_model.jpg)
Everyone is good at certain heroes, and everyone is bad at others. We will be classifying the heroes which a Dota player excels at, and those they struggle with.

![Game Outcome Model](/themes/adritian-free-hugo-theme/assets/images/projects/dota/game_outcome.jpg)


## Table of Contents

1. Gathering Data
2. Preprocessing Hero Data and Merging External Sources
3. Performing Clustering Analysis with the Hero Data
4. Interpretation of Clustering Outputs
5. Preprocessing Match Data
6. Deriving Win Flag
7. Merging Clustering Data to the Match Data
8. Finding Win Probability using Classification Algorithms
9. Conclusion

## 1. Gathering Data

With the help of the OpenDota API, we extracted Hero Statistics data and Matches data. Using `curl`, we retrieved the data in document form (JSON format). 

Hero data consists of:
- Total number of games played for each hero
- Game win percentage with the hero
- Game win percentage against the hero

Matches data consists of in-game metrics such as:
- Duration of each match
- The hero picked during the match
- KDA (Kills, Deaths, Assists)
- Whether the player played with their team or solo
- The role of the hero

The hero dataset also includes information about the hero, such as its primary role, and spell data (with a focus on hero roles since some heroes can be played as both carry or support).

## 2. Preprocessing Hero Data and Merging External Sources

We have the hero performance for each player, such as the number of matches played under the hero, win percentage, win percentage when the hero was picked by teammates, and win probability when picked by opponents.

Although we have hero statistics, we do not always know if the player played a support or carry role. That’s where the hero dataset comes in. Through a GitHub pull request, we found the primary, secondary, and tertiary roles of each hero.

We merged this data into a final dataset, which we later used for clustering.

## 3. Performing Clustering Analysis with the Hero Data

We applied K-means clustering and Tree-based clustering. Since we wanted to easily distinguish between the most comfortable and least comfortable heroes, we implemented K-means with a value of k=5 for clustering. 

We also measured the Euclidean distance and found that 5 is the optimal number of clusters for this model.

## 4. Interpretation of Clustering Outputs

After performing K-means clustering, we interpreted the clusters based on win probability. The K-means algorithm effectively identified and distinguished the most comfortable heroes from the least comfortable ones.

## 5. Preprocessing Match Data

We preprocessed the match data by removing columns that contained over 50% outliers. For instance, although the patch version is a valuable feature, including it would require additional metadata about the patch details, such as which heroes were buffed or nerfed. This metadata was not available.

## 6. Deriving Win Flag

Since we only had the side on which the match was played, we could not initially determine if the game was won or lost. To address this, we tweaked the REST API link to include the win condition.

We then combined the win and loss datasets into a single matches dataset.

## 7. Merging Clustering Data to the Match Data

We merged the Hero Skill Adaptation model with the game outcome dataset to create a final dataset. This dataset contains:
- In-game metrics
- The hero played in the match
- The comfort level of the hero (as determined by the clustering labels)

This allowed us to proceed with running classification models on the dataset.

## 8. Finding Win Probability Using Classification Algorithms

We split the data into 80% for training and 20% for validation.

We ran several classification models and found that all models performed well, with no overfitting or underfitting issues. 

In the end, we selected Naive Bayes as the final model to predict the win outcome.

## 9. Conclusion and Next Steps

The trained model can help players understand what is the expected KDA needed to achieve a win, and provide insight into which hero to pick based on the player's comfort level.

Currently, the model only considers individual players' pick status and corresponding in-game metrics. Since Dota is not just about individual metrics but also about hero counters and overall team performance, incorporating these factors in the future could make the algorithm more efficient at identifying the right heroes and their comfort levels for better results.
