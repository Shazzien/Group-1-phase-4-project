# Phase 4 Project

* Group: *Group 1*<br>
* Student names: *Faith Kanyuki, Marybennah Kuloba, Sharon Thiga, Sharon Maina*<br>
* Student pace: *Part Time*<br>
* Instructor name: *Christine Kirimi*<br>

# Measuring Public Perception of Apple and Google Products on Twitter
## 1. Project Overview
The aim of this project is to build a Natural Language Processing (NLP) model to classify tweets mentioning Apple or Google into positive, negative, or neutral sentiments. This will help understand public perception, monitor brand reputation, and inform marketing and product strategies.<br>
This project will enable businesses to:

* Adjust their campaigns based on trends in sentiment
* Prioritize responses when negative sentiment spikes.
* Identify common issues or requests from user feedback.
* Detect negative trends early to mitigate PR risks.

## 2. Business Problem
Our analysis will give insights on the following questions:

* How do people feel about Apple vs Google products on social media?
* Which words or phrases are most influential in expressing sentiment?
* Do specific events or product launches trigger changes in sentiment?

## 3. Data Understanding
For this analysis, we used the [crowdflower dataset](https://data.world/crowdflower/brands-and-product-emotions) which contains over 9,000 tweets about Apple and Google products. The dataset has tweets from real users in the form of unstructured text. Each tweet is labelled as expressing either positive emotion, negative emotion or no emotion, making it suitable for supervised Machine Learning.

## 4. Data Cleaning and Preparation
1. **Dropping unwanted columns**: Retained only the columns that contain the tweets and the sentiment label.
2. **Handling Missing Values**: Dropped rows with missing sentiment labels and replaced missin values in the tweet column with appropriate placeholders.
3. **Renaming Columns**: Columns were renamed to make them more intuitive.
4. **Removing Unwanted Sentiment Categories**: Retained only the tweets that are labelled as having either positive, negative or neutral sentiment.
5. **Cleaning Text Data**: Converted text to lowercase. Removed URLs, mentions, hashtags, punctuation marks, numbers, whitespace. Removed stopwords.
6. **Tokenization and Lemmatization**: Converted each tweet to a list of tokens afterwhich lemmatization was applied.
7. **Word Vectorization**: Utilized the TF-IDF Vectorizer to assign weights to each word based on the rarerity of the word in the corpus.

### 4.1 Exploratory Data Analysis
#### Distribution of Tweet Sentiments
<br>
<p align="left">
  <img src="tweet_sentiment_distribution.png" width="600" height="400">
</p>

 - majority of the tweets are neutral or positive, with negative reactions being minimal. 
 - This can guide marketing and customer engagement strategies to maintain positive sentiment while monitoring negative feedback for potential improvements.

#### Tweet Length by Sentiment
<br>
<p align="left">
  <img src="tweet_length_distribution.png" width="600" height="400">
</p>

- Positive tweets have mostly between 50 - 100 characters, suggesting that users expressing positive emotions are likely to share detailed feedback or experiences.
- Negative tweets cluster around 20 - 80 characters, indicating brief and direct texts reflecting frustration or immediate reactions.
- Neutral tweets have a broader range. They are likely to be informational or descriptive texts that stick to the facts rather than conveying emotion.

## 5. Modeling
### 5.1 Logistic Regression Classifier
A multiclass logistic regression classifier was built to classify tweets as either positive, negative or neutral based on the vectorized text, tweet length and word count. The data was split into a training and test set where 80% of the data was set aside for training the model. A gridsearch was used for hyperparameter tuning to achieve the best performing model.
#### Parameters for Best Performing Logistic Regression Classifier
- **C**: 5
- **penalty**: l2

#### Model Performance on Test Data
<br>
<p align="left">
  <img src="cnf_matrix_log_reg.png" width="600" height="400">
</p>

The Logistic Regression Classifier achieved a test accuracy of 65%.
| Class | Precision | Recall | F1-Score |
|-------|-----------|--------|----------|
|`positive`| 0.57 | 0.60 | 0.59 |
|`negative`| 0.33 | 0.51 | 0.40 |
|`neutral`| 0.76 | 0.70 | 0.73 |

### 5.2 Random Forest Classifier
A random forest classifier was built to analyse the same features and classify the tweets into one f the three classes. In this case, the sentiment labels were converted to numbers using a label encoder since a random forest model can only work with numerical data.<br>
negative -> 0 <br>
neutral -> 1 <br>
positive -> 2 <br>
#### Parameters for the Random Forest Classifier
- **n_estimators**: 200
- **class_weight**: balanced

#### Model Performance on Test Data
<br>
<p align="left">
  <img src="cnf_matrix_rf.png" width="600" height="400">
</p>

The Random Forest Classifier achieved a test accuracy of 67%.
| Class | Precision | Recall | F1-Score |
|-------|-----------|--------|----------|
|`positive`| 0.62 | 0.42 | 0.50 |
|`negative`| 0.58 | 0.19 | 0.29 |
|`neutral`| 0.69 | 0.86 | 0.77 |

### 5.3 Support Vector Machine (SVM) Classifier
Similarly, the sentiment labels were also converted to numbers since the SVM classifier can only work with numerical data.

#### Model Performance on Test Data
<br>
<p align="left">
  <img src="cnf_matrix_svm.png" width="600" height="400">
</p>

The Random Forest Classifier achieved a test accuracy of 64%.
| Class | Precision | Recall | F1-Score |
|-------|-----------|--------|----------|
|`positive`| 0.57 | 0.60 | 0.59 |
|`negative`| 0.31 | 0.54 | 0.40 |
|`neutral`| 0.76 | 0.68 | 0.72 |

### 5.4 XGBoost Classifier
For this model, the sentiment labels were also converted to numbers.
#### Parameters for the XGBoost Classifier
- **n_estimators**: 200
- **max_depth**: 6
- **learning_rate**: 0.1

#### Model Performance on Test Data
<br>
<p align="left">
  <img src="cnf_matrix_xgboost.png" width="600" height="400">
</p>

The Random Forest Classifier achieved a test accuracy of 67%.
| Class | Precision | Recall | F1-Score |
|-------|-----------|--------|----------|
|`positive`| 0.63 | 0.37 | 0.47 |
|`negative`| 0.58 | 0.10 | 0.17 |
|`neutral`| 0.68 | 0.89 | 0.77 |

## 6. Model Evaluation and Interpretation
