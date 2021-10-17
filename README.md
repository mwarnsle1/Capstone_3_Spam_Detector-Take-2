# Project 3 Spam Content Filter - Identifying Unwanted Comments for Company Security
A model that identifies and filters spam content in online forums

# Overview

With a world that is becoming increasingly digital and social-media focused, the need to manage and maintain the integrity of online platforms during online engagement has become a necessity.

What are spam comments? The more time spent online, they are bound to come across spam comments. They take many forms, such as being automated by spambots, generic messages as a cover for including links. They mainly pose a risk to online platforms because:

they interfere with the user experience, increasing the difficulty for legitimate visitors to engage
decrease the overall legitimacy of the site
contain redirecting and potentially malicious links, for phishing or malware
Cyber-security is the practice of protecting systems and entities from outside forces designed to infiltrate, change, and gleam sensitive information from them. Today, companies have begun to practically invest in software, professionals and in larger agencies, entire departments familiar with addressing, preventing, and managing these crises situations. Such software can include:

- a created list of "blacklisted" keywords
- hyperlink moderation
- anti-spam plugins(active database of spam)



# PROPOSAL

A prospective online platform company is in the market for new software that identifies spam. How can you help them create an effective filter?


# The Data

The data for this project was obtained from The University of California, Irvine's public dataset archive, and consists of five csv files. Each file contains sets of comments(341_590 bytes, 1956 in all) extracted from the five most popular YouTube music videos(); for the collection period of 07/2013-04/2015. They files originally came separate but were able to be combined into one large csv using GIT GUI. Following are the links to the dataset:

- https://archive-beta.ics.uci.edu/ml/datasets/youtube+spam+collection
- https://archive.ics.uci.edu/ml/machine-learning-databases/00380/
- github: https://github.com/mwarnsle1/Capstone_3_Spam_Detector-Take-2/blob/f518cdf5ae84c0c59e03dbea57f536ef1d20b883/new_combinevid_files.csv


# Methods

As mentioned in the previous section, for my research, a public dataset was obtained from UCI's archives, originally consisting of five individual files that were then combined into one csv file of comments. This was for both ease of accessibility and analysis. The combined datasets catalogued the categorized emails received by users. Before the model creation, I initially applied a number of exploratory analyses; such as removing any null values and exploring the interactions between datetime and other variables.

I then applied some preliminary visualizations and descriptive statistics to check the initial distribution of the variables; by themselves and in relation to each other. Afterwards, I proceeded to apply a progressive variation of models to observe their effect and accuracy on the dataset and clustering abilities on unlabeled data. I applied K-Means and DBSCAN clustering methods to the chosen numeric features - "Years", "Months", "Wday", "Text_Length" - in order to display the categorization of clustering and ability to filter Spam content. I also adjusted the parameters, and applied hierarchical clustering to the dataset. After observing the results, I applied two other clustering methods; TF-IDF/K-Means to the data, with word clustering included, and Text clustering with NLP. For these two unsupervised learning models, I used an earlier dataframe with less features - Date, Content, Text_length.

I applied a number of natural language processing techniques to the dataset; specifically, word embedding using Word2Vec and word vectorization. Their effectiveness were used to build a better predictive model, filtering Spam. For the NLP Text Clustering, I trained and tested the model, preprocessed the data by removing stopwords, applied TFIDF Vectorization and KMeans clustering to find the optimal number of clusters using the Elbow Method(the point of inflection on the plotted curve), and plotted the outcome. The results are discussed in the next section.


# Results

The exploratory analysis showed a number of trends with the variables that were created. May was by far the most active month, with almost 600 comments, and November being the second most-active month(and also having the most popular date - November 7, 2014). Comments tended to be evenly dispersed throughout the week, though activity went slightly up on the weekends.

The cluster modeling with K-Means and DBSCAN continued to show three variables grouped into two large clusters; both in the scatter plots and PCA plots. Also, the Silhouette score, RI, and ARI for the K-Means model were:

```
Silhouette - 0.4521
RI - 0.5179
ARI - 0.5503
```
However, after the features were applied to the TD-IDF + KMeans cluster model, better results were able to be obtained, as well as some word clustering that could be used in conjuntion with the "Blacklisting" method (keywords spam filtering method).

Following up on this logic was a WordCloud created alongside a word frequency list generator, which could also be used for Blacklisting. A predictive model was then able to be created using natural language processing(NLP) techniques. Using word embedding, scatter plotting was used to visualize dots annotated with the words from the text. These visualized the proximity Spam-like comments had to each other compared to non-Spam comments. From the second NLP model, a predictive model was created using word vectorization; where each categorization was used to detect and filter Spam content. A confusion matrix was created to easily compare and display, showing that:

```
[[67  4]
 [ 2 99]]
 ```
 
- Actually/predicted to be Ham: 99
- Actually/predicted to be Spam: 67
- Predicted Spam/mistaken for Ham: 4
- Predicted Ham/mistaken for Spam: 2

The Text Cluster NLP Model with TFIDF and KMeans ran successfully also, though this is admittedly a newer method that was simply exciting to be implementing. At this, though the amount of groups expected was known, it seemed the number of optimal clusters were found to be closer to 20. Of note, it also took noticeably more resources to run.


# Discussion & Recommendation

A closer look at the data indicates that techniques for applying the most effective Spam Detection and Filters can be obtained by applying TD-IDF/KMeans clustering with word clustering of unlabeled data, WordCloud with word frequency, and NLP word vectorization models. While DBSCAN algorithm works well to find clusters of any shape and works better than hierarchical clustering, they perform better on more robust datasets.

Drawbacks of the dataset was having a higher number of non-spam("Ham") emails; which may have negatively affected the predictive modeling. This imbalance was overcome for the NLP models; however. Future iterations would still implement measures to balance out the dataset by under-sampling the "Ham" variable, and implement more accuracy measures such as K-Folds cross-validation. Additionally, future iterations would take more advantage of the datetime variables, with further expertise and research.
