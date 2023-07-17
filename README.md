# Cup IT 2023 
## Ranking Comments Using ML 
<div id="header" align="left">
  <img src="https://media.giphy.com/media/1o6rpNIRjOgR9eR1Wj/giphy.gif" width="100"/>
</div>

## Team Members:
- Anastasia Naumovskaya
- Roman Ababkov
- Ivan Nikolaev
- Maxim Staroverov
- Timur Gabitov

## Problem Statement
Propose a mechanism for sorting comments on posts based on their popularity using machine learning methods, so that the model can rank user comments as accurately as possible.

- Perform data verification and exploratory data analysis (EDA) and consider ready-made solutions for representing text.
- Train the model using the training and testing samples of the dataset to rank textual comments in order of their popularity (from most popular to least popular), and validate the model. The model selection should be justified based on the training results.
- Analyze the obtained results and formulate useful insights about what typically constitutes a popular comment, so that the VK team can use this information to improve user comments.
- Propose methods of interaction with commentators, as well as support mechanisms for different user groups, including those whose comments are unpopular. 

## Solution Structure

- **New_features_from_df**
> Extract new features based on comments and post texts, analyze the impact of generated features on the score.

> Comment features: len_with_spaces (comment length divided by spaces), links (indicator of containing links), emoji (indicator of containing special characters &#x), money (indicator of containing the $ sign), quotes (indicator of containing quotes), col_sentence (number of sentences), tokenized (tokenized words), col_words (number of words), punc_count (number of punctuation marks), avg_len_words (average word length), total_digits (total number of digits), total_letters (total number of letters)

> Text features: len_with_spaces (text length divided by spaces), links (indicator of containing links), emoji_pic (number of emojis contained in the text), money (indicator of containing the $ sign), quotes (indicator of containing quotes), col_sentence (number of sentences), col_words (number of words), punc_count (number of punctuation marks), avg_len_words (average word length), total_digits (total number of digits), total_letters (total number of letters)
- **EDA_features**
> General analysis of features from text and comments, extraction of insights
- **BERT**
> Selection of one batch of data (1000), removal of special characters, stop words, normalization. Training a pre-trained neural network to vectorize features. Classification using various methods.
- **CountVectorizer()**
> Vectorize data using CountVectorizer() while removing stop words, normalizing, and tokenizing. Use MultinomialNB for classification or apply TFIDF transformer and classify using MultinomialNB.
- **TFIDF**
> Remove special characters, stop words, normalization. Vectorize sentences using TFIDFVectorizer and evaluate score using various classifiers.
- **ranking_test_solution.jsonl**
> Filled score on the test dataset
- **Solution Presentation**

### General Conclusion

The dataset contains a large amount of data, which makes it challenging to process and scale the model further. The selected methods are based on their common usage in the industry, and their combination can lead to good results.
The best result was achieved with a combination of extracting features from comments + KNN, which was used to process the test dataset.
Using a pre-trained natural language processing model, Bert + KNN classifier, a high score could be achieved, but this model is not suitable for scaling.

Initiatives for implementing the comments ranking system on VKontakte were also proposed:
- Pre-rating in the search bar for comments not yet published
- Creation of a separate service for commentators

**NLP Hell Yeah!**
