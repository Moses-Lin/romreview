# Mobile Game Review Classification

### Continuation of this project
- Initial Project: https://github.com/Moses-Lin/mobile_game_reviews

# Project Goal

The goal of this project is to develop a multi-class classification model that can correctly predict the rating of a review based off of the content of the review. In doing so, developers could possibly use such a model when proactively asking users for feedback in-game in order to gauge how their game is doing without taking a possible hit to their ratings, should users leave negative feedback in the app store. After reviews are classified, they may be analyzed more specifically to address problem areas or to focus on development or further development of desireable features.

I have chosen this specific game, Ragnarok Mobile: Eternal Love, as it is a game that I have played since launch and have been playing to this day. As a result I have an idea of what I want to be looking for, and in a sense have an answer key as to what results I should generally be getting when doing exploratory data analysis.

In addition, it is suitable for a continuation fo my initial mobile games review project, as the game itself has multiple regions and different number of reviews per region. This gives me a view of what changes in modeling and EDA when certain factors are changed such as culture, playerbase size, and timing of updates.

# Dataset
Data was gathered from the Google Play store on [1/7/2020] at 10:26 PM EST for ROM Global, ROM SEA, and ROM EU
Data was gathered from the Apple Store on [1/7/2020] at 10:26 PM EST for ROM Global

A Google Play Scraper (https://github.com/JoMingyu/google-play-scraper) was utilized.
An Apple Store Scraper (https://github.com/cowboy-bebug/app-store-scraper) was utilized.

A total of:
- 6533 Reviews were obtained for ROM Global (Google Play)
- 1318 Reviews were obtained for ROM Global (Apple Store)
- 72231 Reviews were obtained for ROM SEA (Google Play)
- 577 Reviews were obtained for ROM EU (Google Play)

ROM EU had too few reviews to work with, so the files were not pickled for use later. 

The only reviews selected from the Apple store came from US, Canada, and Australia as these are the major English-speaking countries that play the Global Server.


# Repository Contents

- Scraping (scraping.ipynb): The process used to obtain the datasets in preparation for cleaning and EDA.
- Exploratory Data Analysis (EDA.ipynb): Analysis of the reviews using NLP methods, and visualization to demonstrate insights.
- Modeling (Modeling.ipynb): Various models were examined and the best model was identified.

# EDA

Distribution of ratings across both ROM Global and ROM SEA are relatively the same, with the most reviews being 5 stars, and 2nd most reviews being in the 1 star category. 2 to 4 star ratings comprise the least of all ratings. Interestingly, 1 star ratings comprise of a greater percentage of reviews in ROM SEA. This is possibly indication that SEA culture is much more critical of games than their Global counterparts. However, it is known that SEA was considered a "guinea pig" for new updates in the past before they were applied in Global. This is indicative of how review spikes are much more prevalent in SEA than Global when major updates land. SEA was subject to much more game breaking bugs than Global upon release of major updates.

Looking at the meta features of reviews in ROM Global and ROM SEA show that Rating 2 reviews generally have the more substance to them, as they contain the most characters, punctuation, and capitalizations. Rating 5 on the other hand generally have very low count of most meta features, much lower than any other ratings by a long shot. The one exception would be mean number of words for both ROM Global and SEA reviews. This could be another indication that a majority of words used in Rating 5 are rather short, possibly indicating less thought being put into word choice.

When looking at the top 20 words/ngrams across ROM Global, there are not many well-defined features distinguishing these reviews from reviews of any other games. However, when looking at ROM SEA words/ngrams, there are several indications of jargon used specifically for that game such as woe/woc which is a game mode in the game. There are also several slang terms used such as calling Ragnarok Mobile: Eternal Love by the moniker of "Lagnarok Eternal Bug" or "Bugnarok Eternal Lag". Such jargon/slang is absent in the global top 20 words/ngrams and is most likely due to the lack of reviews. This is because these terms are also commonly referenced in the Global community as well, but perhaps is blanketed by more common phrases. Perhaps this is also an indication that Global players are less likely to put notable reviews than that of SEA players.


# Modeling

A baseline model was created using a dummy classifier. The Accuracy and F1 score is about 29%, which is an strange value as it should normally be 20% with random guessing. However, this is our baseline for comparison.

### Performance Metric
Accuracy was selected as the main metric as True Positive and True Negatives are most important in determining a valid representation of a mobile game's performance. In addition, the dataset is balanced after downsampling, so accuracy will be favored in this scenario.

F1 score was also considered as the cost of a False Negative and False Positive is the same: The developer gets an incorrect rating that is not reflective of their mobile game's performance.

### Models
Four different models were fit to the dataset after TF-IDF Vectorization: Naive Bayes, Decision Tree, Random Forest, and Support Vector Machine.

#### Global Models:

- Dummy Classifier: 33.19% Accuracy, 32.79% F1 Score
- Naive Bayes: 66.87% Accuracy, 58.90% F1 Score
- Decision Tree: 58.28% Accuracy, 56.51% F1 Score
- Random Forest: 66.75% Accuracy, 58.00% F1 Score
- Support Vector Machine: 68.42% Accuracy, 59.50% F1 Score

##### GridSearch Global

- DT: 59.15% Accuracy, 52.87% F1 Score
- RF: 67.49% Accuracy, 58.38% F1 Score
- SVT: 68.72% Accuracy, 61.93% F1 Score

#### Global Models with Apple Store Reviews Added (1/7/2021 added)
- Dummy Classifier: 29.50% Accuracy, 29.52% F1 Score
- Naive Bayes: 66.73% Accuracy, 58.87% F1 Score
- Decision Tree: 56.34% Accuracy, 54.59% F1 Score
- Random Forest: 65.97% Accuracy, 57.34% F1 Score
- Support Vector Machine: 68.62% Accuracy, 59.65% F1 Score

#### GridSearch Global (with apple reviews)
- DT: 58.58% Accuracy, 52.96% F1 Score
- RF: 67.04% Accuracy, 57.93% F1 Score
- SVT: 68.57% Accuracy, 61.60% F1 Score

#### SEA Models:

- Dummy Classifier: 36.67% Accuracy, 36.84% F1 Score
- Naive Bayes: 72.62% Accuracy, 69.06% F1 Score
- Decision Tree 69.87% Accuracy, 68.03% F1 Score
- Random Forest: 75.54% Accuracy, 69.82% F1 Score
- Support Vector Machine: 77.24% Accuracy, 71.00% F1 Score

##### GridSearch SEA

- DT: 72.09% Accuracy, 67.33% F1 Score
- RF: N/A (75.44% Accuracy, 70.05% F1 Score)
- SVT: N/A (76.84% Accuracy, 70.83% F1 Score)

# Findings

### About the Models

The best model for ROM Global was Support Vector Machine with Gridsearch with 68.73% Accuracy, 61.93% F1 Score. The best model for ROM SEA was Support Vector Machine without Gridsearch with 77.24% Accuracy, 71.00% F1 Score.

It seems that adding in reviews from the Apple store dropped the performance of the models by a bit, possibly suggesting some difference in how people review the games per platform.

Unfortunately, I was unable to utilize Gridsearch for ROM SEA reviews for Random Forest and Support Vector Machine as they simply took too long to run, or would freeze up the kernel. However, with a more powerful computer, it is very possible to run such models with an increased review size.

### Conclusion

Perhaps for games with similar characteristics to ROM, it is possible to apply the classification model created here in order to determine a general "rating" for a specific period of time such as during major updates. In addition, we can determine that from those classifications, developers may sort such tickets in order of importance as it seems that ratings 1 or 5 yield very little beneficial information.


### Limitations:

- I am running these models on a MacBook Air with 1.1 Ghz Dual-Core Intel Core i3. Perhaps a stronger computer could be used or a cloud service like Amazon Web Services could be used to run models that I normally cannot.

- Servers for certain games like ROM did not start concurrently, and as a result it's hard to really compare both servers. In a sense, you could consider these completely different games, especially if the publisher is different for different regions (TERA Online for example has En Masse Entertainment for the North American Version and Gameforge for the European Version).

- A majority of people may simply not review the game on the app store, and would rather send support tickets to voice their complaints. As a result, it is possible that the reviews used are less critical than they would seem.
 
- A majority of reviews for this game was not picked up by the scraper.

- Rating is not necessarily a good indicator of app performance. As previously mentioned, many games bait users into giving good reviews by offering in-game rewards for doing so. In addition, games that are well received by an audience may not have a sustainable model and can "die" much earlier than expected. Revenue would be a much better indicator, but such information is not publicly available most of the time.

### Future-Work

- Review mobile MMOs that are similar in rating to this game. This perhaps will give insight as to which words may be simply common phrases that can be ignored.

- Review mobile MMOs with more ratings but similar microtransaction systems. This will perhaps increase the accuracy and F1 score of this modeling

- Review other genre of mobile games, preferably those with multiple servers for comparison.

