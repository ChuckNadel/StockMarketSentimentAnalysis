# Stock Market Sentiment Analysis

### The Business Problem

We've been tasked by Point72 to conduct a sentiment analysis on a forum of retail investors, in order for them to implement them on top of their existing systematic trading algorithms

### The Dataset

For our data, we scraped r/Investing Daily Discussion Posts and Comments to gauge investor sentiment on a given trading day. We also will use yahoo finance data on the S&P 500 for our classification analysis

### Methods

​First, we had to conduct sentiment analysis on the reddit comments. To do so, I used the VADER Sentiment Analysis Library. Although this might not be optimal r/investing specifically, it is the best option for sentiment analysis on social media, and is familiar with the lingo and other things used on a website like reddit. After implementing VADER, we were able to get a compound sentiment score for each comment.

After that, we aggregated each comment based on the day, and averaged all of the comments' scores to get our aggregated score. This was then merged with the S+P500 stock market data of those days, along with whether or not the market was up or down on that day.

Finally, we implemented and optimized 5 different classification models (Decision Tree, Naive Bayes, KNN, Gradient Boost, and ADA Boost) to classify whether or not the market would go up or down on a given day, based on the average compound sentiment score of that day.


### The Results

Optimzed for accuracy, our best model turned out to be the Gradient Boost Model, with an accuracy on 66%, as shown by the following confusion matrix.
<p align="center">
  <img src = images/GradientBoostConfusionMatrix.png width="750" height="500">
</p>

Although this is relatively low, it is better than our completely naive baseline. However, due to our small sample size, I decided to stack all 5 of the models used, in order to improve its performance on unseen data. Since sklearn's stacking classifier did not work with my data, I aggregated all of the predictions from each of the models, and would classify each date based on what the majority of classifiers predicted for that day. That model performed a bit worse, only being 57% accurate, but it should perform much better on unseen data. Here is that confusion matrix.
<p align="center">
  <img src = images/StackedModelConfusionMatrix.png width="750" height="500">
</p>

### Next Steps

​Increase Sample Size- 250 days of data is not nearly enough

Apply to specific tickers, other websites such as twitter, stockaholics, and others

Implement on top of more formal training algorithms.