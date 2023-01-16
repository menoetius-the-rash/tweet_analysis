# Tweet Analysis on Ukraine Russia tweets using NLP techniques
Analysis of Ukraine Russia tweets from April 20 to May 2022
Jupyter notebook was used for this.
Using Pyspark and Cassandra, the tweets were stored, pre-processed, analysed and evaluated.

## Method & Implementation

![image](https://user-images.githubusercontent.com/62455043/212716817-02242b88-b77f-4e48-ae5a-bd6da6b265c3.png)

- Raw data was collected from [Kaggle](https://www.kaggle.com/datasets/bwandowando/ukraine-russian-crisis-twitter-dataset-1-2-m-rows)
- Raw data was then stored in a Cassandra DB
- Pyspark to queary the data into a dataframe
- Create pipelines in Pyspark to clean and perform Sentiment analysis on the data
- Store results in the Cassandra
- Process results to perform topic modelling

### Sentiment Analysis with Naive Bayes labelling implementation
User-defined functions (UDF) were created in order to get the polarity scores of the tweet. Another UDF was created to evaluates these scores to assign them positive, neutral or negative sentiment.

- Create training and test data
- Use HashingVectorizer rather than CountVectorizer as it is more efficient and takes less space in our session
- Create vectors for train and test data
- Get the scores with naïve bayes
- Begin the prediction of the data
- Review the scores returned using the metrics library from sklearn

### Topic Modelling with LDA

- Tokenize the data
- Create a vector of the data
- Inverse Data Frequency (IDF) of the vector of data
- Perform LDA on the data provided
- Get the vocabulary list of the data and the topics from the model generated
- Finally map this and print out the dataframe of the topics

## Results

![image](https://user-images.githubusercontent.com/62455043/212725905-b81530cf-27e4-47ea-871e-67d292a4c3f2.png)

There were more positive tweets identified against neutral and negative sentiment. These returned a 74% accuracy when evaluating and was improved to 79% accuracy when stop-words were removed.

![image](https://user-images.githubusercontent.com/62455043/212725926-412c9323-3e1c-4b76-a389-dfa3ac0647c3.png)

Shown on the diagram is the number of tweets per hour in a 24-hour format. It can be seen below that the data on hour 14, is the most active number of tweets. Also, between hours 14-19 inclusive are the busiest times where there is higher traffic of tweets.

![image](https://user-images.githubusercontent.com/62455043/212728874-0ed8e5bc-fe61-4f23-96a6-2882671db6fb.png)

This is a word cloud of tweets that was cleaned and processed. It can be seen that Ukraine and Russia stand out. War, people, Tigray, government stand out as well.

![image](https://user-images.githubusercontent.com/62455043/212729003-9d319ba6-e2ac-4ca4-b911-c984a61e2b91.png)

As can be seen with ten topics created with LDA, topics are overrun by stop-words. This is not ideal as it does not help with the analysis. Due to time constraints and hardware limitations, this is being left here. For improvement, the next time this is ran, stop words will have to be removed to get a meaningful result. This will be improved in the coming weeks.

## Future Work & Considerations
- Add confusion matrix to the results for evaluation
- Improve topic modelling by removing stop words to achieve a meaningful result
- Consider re-implementing Pyspark to work with using the GPU to speed up processing
