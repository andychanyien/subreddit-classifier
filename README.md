# DSI17_Project3_Reddit

## Problem Statement

Some people wish they were born with super powers, allowing them to do many amazing things typical human beings could not do. On the other hand, there are also some super powers which could bring some inconvenience too. For example, the ability to turn things into gold by touching an object (like the Midas touch) may seem like an awesome super power. However, it also turns food into gold; you will not be unable to eat anything at all. In such cases, people would call it a "shitty super power". The subreddit dedicated for such discussion is r/shittysuperpowers. The super powers discussion are usually hilarious power which affects daily lives and daily activities.

The more extreme version and positive version can be found here r/godtiersuperpower. According to the description, it is "r/shittysuperpowers, but they're actually god tier". In this subreddit, they discuss hilarious powers but gives strong powers that are comparable to God. Hence, both subreddit have hilarious powers but the difference lies with the outcome of those super powers.

In which subreddit would your super power be classified under? The aim of this notebook is to build a classifier model based on reddit users' sentiments. The classifier would be able to determine whether a super power is "god-tier" [1] or "shitty" [0] through analysing the text within the post. Since the training dataset would be from reddit users, if the model has high accuracy and predictability, it should be able to determine what reddit users think about your super power. The classfier models which will be explored are Logistic Regression, Multinomial NB and RandomForest, vectorised either by Count or by TFIDF.

**Measurement of Success**

The prediction of the model will be scored and it's accuracy will be determined. The higher the accuracy, the more accurate the model is at predicting whether a super power is considered god-tier or shitty, based on Redditors' sentiment/opinions. 

Another measurement of success will be feeding the model two super powers and determine if the predictions are likely to be true.

**Primary Stakeholders**

The model could be useful content creators, such as novel writers or comic creators, to determine whether their new super hero with a new super power would be favourable among the community or not. In the world of content creators, these are valuable information which allows them to sense whether their idea would be favourable or not within the community. Furthermore, when vying for consumers' attention, creators with a headstart have a higher chance extending their lead in the market.

**Secondary Stakeholders**

Another useful application would be using it as a tool for reddit's website backend. The subreddit moderators could use such tools to automatically classify posts which may not belong to a certain subreddit group.


## Executive Summary

Reddit is a go-to place for communities to engage in discussions and express themselves in across various topics in different subreddits. Wouldn't it be nice to know how the community feels about certain issues without looking through thousands of posts? Wouldn't we then be able to know what grabs their attention?

Based on two subreddits, r/godtiersuperpowers and r/shittysuperpowers, a model was developed to determine whether a post belongs to which subreddit. The model was trained based on redditors' sentiments and opinions in both subreddits. Through such a model, we could understand whether a super power would be considered "God-tier" or "Shitty".

During the EDA, the words used in each subreddit was analysed based on frequency (using Count Vectorisation) and its salience (using TFIDF Vectorisation). Firstly, the 20 most frequent words were compared between the two subreddits to see what kind of words appear the most in each subreddit. The more certain words appear over the other subreddit, the stronger it is as a determinant in the classifier model. Secondly, the TFIDF Vectorisor showed the most significant (or unique) word in each posts, relative to the all the text. The more unique the word, the stronger it is as a determinant in the classifier model. Finally, salient words in each subreddit were also compared against each other to determine the words unique to each subreddit and whether there were common words.

**Findings**:

- The median word count for r/godtiersuperpowers and r/shittysuperpowers are 56 words and 46 words respectively, with many outliers writing beyond 500 words.

- Both subreddits have quite a lot in common
    - Among the 20 most frequent words, there were 10 common words.
    - There about 700 words unique to each subreddit, with 166 common words.

- The common words tend to describe god-tier powers more, making it likely for model to predict false negatives.

- Context is still very important, words without context are insufficient to qualify a super power.


**Model Evaluation and Selection**

Using Count Vectorisation and TFIDF Vectorisation to preprocess the dataset, and applying it to Logisitic Regression, Multinomial Naive Bayes and RandomForest, a total of 6 models were developed. The models were also optimised by tuning their hyperparameters using GridSearchCV and RandomSearchCV. Out of the 6 models, the top 2 performing models were scored based on Accuracy and AUC score. In the end, RandomForest with Count Vectorisation performed the best, with the least overfitting, high accuracy and higher AUC score. 

**Results**

One can understand whether a super power would be god-tier or shitty based on the model. It has an accuracy of about 65% with an AUC score of 0.649. Content creators and reddit moderators would be able to leverage on such algorithm but its limitation should be overcome in order for it to be practical and useful.

## Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**name**|object|god_tier_df, shitty_df, combined_df|unique ID for each poster|
|**selftext**|object|god_tier_df, shitty_df, combined_df|The text where users can write more than one sentence or more than the title|
|**title**|object|god_tier_df, shitty_df, combined_df|The title of the post|
|**subreddit**|object|god_tier_df, shitty_df, combined_df|The subreddit the post belongs to|
|**combined_text**|object|god_tier_df, shitty_df, combined_df|The combination of selftext and title|


## Conclusions and Recommendations

I have managed to build a classifier model based on redditors' sentiments and opinions which could determine whether a post belong to r/godtiersuperpowers or r/shittysuperpowers. The model has a 65% accuracy in correctly determining whether a post belongs to whichever subreddit.

Another way to interpret the accuracy is that the model is able to determine whether reddit users would think a super power is "god-tier" or "shitty", with 65% chance of being right.

Overall, the model is quite good at classifying more than half the time but it is still lacking in order for it to be more useful. 


**Limitations**

The model is far from perfect and has a lot of shortcomings and limitations. Based on EDA, preprocessing and modelling, here are three limitations which could be addressed.

1. The model is limited to the vocabularies it is trained with. It will be difficult for the model to predict from complex strings. The model uses key vocabularies from each post to train and determine the results, using vocabularies outside of the model may not work very well.


2. The topics of both subreddits are highly subjective. Even human beings have difficulty in determining what is absolute good or bad. A super power which might seem bad could be good in another's eyes. Hence, it can be very difficult to achieve high accuracy in these two subreddits.


3. It cannot process Non-ASCII Characters. The model is not able to fully analyse non-ASCII characters, such as emojis and foreign characters. They are removed but they are also data observations too. For example, emojis like 🙃 could tell us someone is being sarcastic. Unfortunately, the tools to clean and analyse non-ASCII characters are not available yet. Manually imputing is an option but it would take too long to go through everything.

**Recommendations**

1. Scrape more data and train the model with more words! As the machine learns more vocabularies, it would predict better.


2. To reduce the subjectivity and improve objectivity, perhaps more feature engineering is required. Perhaps words can be further classified into categories first. For example, they can be classified into verbs and adjectives. The current model classifies based on a mixture of verbs, adjectives and nouns.


3. Explore libraries or other tools which can analyse emojis, such as [DeepMoji](https://deepmoji.mit.edu/). This will become inevitable as more people express themselves this way, especially in cooler subreddits.

**Stakeholders**

From the EDA and model, content creators definitely could understand the kind of abilities which interest our redditors, and understand what sets both subreddits apart through analysing the words used. They can also get a sense of what redditors would think by running super powers through the model. 

For moderators, it is possible that such a model could be automated and integrated into the backend which allows for automated sorting of reddit posts. It could also be expanded to flag inappropriate content, such as racists remarks or words which violate community standards. 

However, for it to be truly feasible and applicable, the model needs to overcome the above limitations and improve its accuracy.