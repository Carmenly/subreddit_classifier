# Project 3 - Cryptocurrency Subreddit Classifier: Empowering Solana's Ecosystem


## **Problem Statement**

As a data scientist at the Solana Foundation, I have been tasked with analyzing Solana's standing in the cryptocurrency space particularly in regards to Reddit. As a platform, Reddit can be a valuable resource of information on popular opinion. The insights gleaned from these analyses will be invaluable in shaping the foundation's marketing strategies, community engagement efforts, and developer outreach initiatives, enabling the foundation to effectively navigate the cryptocurrency ecosystem and strengthen the position of Solana as a leading blockchain platform.

## **Data Dictionary**

| Feature | Type | Description |
| :--- | :--- | :--- |
| subreddit | Object | The source subreddit : bitcoin or solana |
| title_text | object| concatenated "title" (title of the post) and "self_text" (the text content of the post)|


## **Executive Summary**

The project's objectives are as follows:

* Collect and analyze Reddit comments to discern prevalent topics within the cryptocurrency community.

* Conduct sentiment analysis on the comments to gauge the overall sentiment towards Solana versus Bitcoin. This analysis will provide valuable insights into how the online community perceives each cryptocurrency, allowing the foundation to tailor communication efforts to effectively differentiate Solana and highlight its unique value proposition.

* Develop a Classification Model capable of accurately determining the subreddit origin (Bitcoin or Solana) of a given comment. This model will utilize machine learning techniques to classify comments accurately.

## *Data Collection*

To accomplish these goals, data was scraped from Reddit using the Python Reddit API Wrapper package (<https://praw.readthedocs.io/en/stable/>). A total of 1,902 posts were collected from r/solana and r/bitcoin, 914 posts for Solana and 988 for Bitcoin.

Data sources:
* <https://www.reddit.com/search/?q=r%2Fsolana&type=link&cId=ca238145-35f3-46cc-a570-d76e0253fdb7&iId=6fa398b8-c15f-4721-941b-fab4643f6cb3>
* <https://www.reddit.com/search/?q=r%2Fbitcoin&type=link&cId=65e4cdfb-7226-48b3-895d-f5dfe37ee901&iId=edbad7fc-1437-46df-bc31-4dbf009f6f0b>

The following features were retrieved during data collection:

created_utc\
title\
self_text\
subreddit


## *Data Cleaning*

* There were 250 and 90 null values in the "self_text" columns for bitcoin and solana DataFrames respectively. These were filled with an empty string
* Removed two duplicated rows from the bitcoin DataFrame
* Removed URLs, emojis, punctuation, special characters and extra white spaces. Used the Spacy library to tokenize the text, and perform lemmatization to reduce tokens to their root form.
* The two DataFrames were concatenated, and the "title" and "self_text" columns were merged into a single column "title_text". Subsequently, these merged columns, along with the "created_utc" column, were dropped.

Cleaned data was saved to a csv for modeling: "reddit_data.csv" 


## *EDA (Exploratory Data Analysis)*

* Exploration of Word Frequency: Examined word frequencies within each subreddit's posts to uncover patterns and topics that are prevalent within the respective communities. The most common words were very similar in both subreddits and did not reveal much information. 

* Comparison of Unique Vocabulary: Compared word frequencies and distributions between the two subreddits to discern which words were distinctly associated with one subreddit over the other. This allowed me to uncover vocabulary that is characteristic of each community, highlighting their unique discussions and interests.
For instance, conversation in the r/Bitcoin subreddit was mostly focused on Bitcoin's ETF, alongside some discussions regarding recent scams. The r/Solana community discussed things such as different trading platforms within the Solana ecosystem and memecoins. 

* Sentiment analysis: Utilized sentiment analysis techniques to evaluate the overall sentiment expressed within the discussions of both subreddits. While the community in both subreddits share similar sentiment, the sentiment from the Solana community is slightly less negative overall.


## *Modeling*

A Dummy Classifier model that predicts the most frequent class label in the training data for all instances in the test data was used as a baseline model. This approach enables us to assess the performance of more advanced machine learning models by providing a simple reference point. 

Four classification models were developed with Tfidf Vectorizer and optimized through grid search, exploring a range of hyperparameters to optimize their performance:

* K-Nearest Neighbors 
* Logistic Regression model 
* Naive Bayes 
* Random Forest 

| Model | Train score | Test score |
| :---  | :---   | :--- |
| Baseline | 0.52 | 0.51 |
| KNN   | 0.99 | 0.8 |
| Logistic Regression | 0.98 | 0.96 |
| Naive Bayes | 0.97 | 0.94 |
| Random Forest | 0.98 | 0.93 |

The KNN model was very overfit. While the other three models were also slightly overfit, the Logistic Regression displays stronger performance. 

The Logistric Regression model predicted 21 comments incorrectly: 13 False Positives and 6 False Negatives. 

## **Recommendations**

* Promote talks about ETFs. By discussing ETFs within the Solana community, we can bridge the gap between traditional financial markets and the Solana blockchain, potentially attracting investors who are more comfortable with conventional investment instruments.
* Partnerships with companies within the cryptocurrency space. The community often mentions Phantom (wallet) and the Jupiter exchange platform, by working with these platforms directly we can potentially extend Solana's reach.
* Steer the conversation away from topics such as memecoins. While certainly a part of the Solana ecosystem, it's important to emphasize Solana's real world utility and potential for meaningful applications in blockchain technology and decentralized finance. 


