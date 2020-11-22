# Mobile Game Review Classification
Module 5 Final Project by Moses Lin

# Continuation of this project
- Initial Project: https://github.com/Moses-Lin/mobile_game_reviews

# Project Goal
The goal of this project is to develop a multi-class classification model that can correctly predict the rating of a review based off of the content of the review. In doing so, developers could possibly use such a model when proactively asking users for feedback in-game in order to gauge how their game is doing without taking a possible hit to their ratings, should users leave negative feedback in the app store. After reviews are classified, they may be analyzed more specifically to address problem areas or to focus on development or further development of desireable features.

I have chosen this specific game, Ragnarok Mobile: Eternal Love, as it is a game that I have played since launch and continuing to this day. As a result I have an idea of what I want to be looking for, and in a sense have an answer key as to what results I should generally be getting.

# Dataset
Data was gathered from the Google Play store on [11/10/2020] at 1:47 PM EST.

A Google Play Scraper (https://github.com/JoMingyu/google-play-scraper) was then used to obtain up to 6432 English reviews from the US.

# Repository Contents
- Scraping (scraping.ipynb): The process used to obtain the datasets in preparation for cleaning and EDA.
- Exploratory Data Analysis (EDA.ipynb): Analysis of the reviews using NLP methods, and visualization to demonstrate insights.
- Modeling (Modeling.ipynb): Various models were examined and the best model was identified.

# EDA
Looking at the top 20 words across reviews did not provide much insight.

CONT

# Modeling
A baseline model was created using a dummy classifier. The Accuracy and F1 score is about 29%, which is an strange value as it should normally be 20% with random guessing. However, this is our baseline for comparison.

### Performance Metric
Accuracy was selected as the main metric as True Positive and True Negatives are most important in determining a valid representation of a mobile game's performance. In addition, the dataset is balanced after downsampling, so accuracy will be favored in this scenario.

F1 score was also considered as the cost of a False Negative and False Positive is the same: The developer gets an incorrect rating that is not reflective of their mobile game's performance.

### Models
Four different models were fit to the dataset after TF-IDF Vectorization: Naive Bayes, Decision Tree, Random Forest, and Support Vector Machine.
- Naive Bayes (Accuracy: 65.4% | F1 Score: 57.7%)
- Decision Tree (Accuracy: 56.3% | F1 Score: 53.9%)     
- Random Forest (Accuracy: 64.8% | F1 Score: 56.0%)
- Support Vector Machine (Accuracy: 66.8% | F1 Score: 57.6%)

Gridsearch Models:
- Naive Bayes (N/A)
- Decision Tree (Accuracy: 60.0% | F1 Score: 53.3%)     
- Random Forest (Accuracy: 65.6% | F1 Score: 56.5%)
- Support Vector Machine (Accuracy: 67.3% | F1 Score: 59.6%)

# Findings

### About the Model
The best model was Support Vector Machine with an Accuracy of 67.3% and F1 score of 59.6%. This is a significant improvement in accuracy and F1 compared to the initial project which used data on a wide variety of mobile games.


### About EDA
Interestingly, it is still somewhat difficult to pinpoint very specific problems that I personally know about this game from playing it since launch. Some of the n-grams simply displayed problems that are relatively common to this genre of games in general. Furthermore, there were a lot less reviews than expected. This makes it rather difficult to filter things out and look for specific problems during periods of time such as launch/major updates/minor updates.


### Limitations:
- I am running these models on a MacBook Air with 1.1 Ghz Dual-Core Intel Core i3. Perhaps a stronger computer could be used or a cloud service like Amazon Web Services could be used to run models that I normally cannot.
- There is a lot of specific mobile game jargon that may not be picked up or simply removed during the pre-processing step. 
- A majority of reviews for this game was not picked up by the scraper.
- This game does not have that many reviews.
- Rating is not necessarily a good indicator of app performance. As previously mentioned, many games bait users into giving good reviews by offering in-game rewards for doing so. In addition, games that are well received by an audience may not have a sustainable model and can "die" much earlier than expected. Revenue would be a much better indicator, but such information is not publicly available most of the time.

### Future-Work
- Review mobile MMOs that are similar in rating to this game. This perhaps will give insight as to which words may be simply common phrases that can be ignored.
- Review mobile MMOs with more ratings but similar microtransaction systems. This will perhaps increase the accuracy and F1 score of this modeling

