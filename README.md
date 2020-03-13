#### Author:
Adriana Vesa
- [LinkedIn Profile](https://www.linkedin.com/in/adriana-v-67aa3a165/)
- [GitHub Profile](https://github.com/adrianavesa)
- Email address - advesa@gmail.com
- Based in New York

#### [Jupyter Notebook](./notebook_clean.ipynb)


### Problem statement
Posts published on the social media impact decisions made by people all over the world in all kind of situations, including health care and health care related topics. Type 1 diabetes is a chronic disease that can start in early childhood and adolescence - and it requires lifelong daily management, including testing, adjusting medication doses, and diet management through various means. When it comes to type 1 diabetes, the options available for diabetics to improve their condition are extremely varied - from medication to testing equipment, to insulin delivering systems, and continuous glucose monitors. A lot of the care is administered by parents - since the disease can commence very early in life - and parents rely on online communities for advice and psychological support (Balkhi, Reid, McNamara, Geffken - "The diabetes online community: the importance of forum use in parents of children with type 1 diabetes" - https://onlinelibrary.wiley.com/doi/abs/10.1111/pedi.12110). We believe it is important to understand the sources of stress and the topics that present interest to people affected by type 1 diabetes, as diabetic distress can impact the condition itself and it is studied as such (Polonsky, Fisher, Earles, Dudl, Lees, Mullan, and Jackson, - "Assessing Psychosocial Distress in Diabetes Development of the Diabetes Distress Scale") - and we will therefore acquire data from the reddit type 1 diabetes thread for the past 100 days - starting with february 18th - and analyze these posts in order to find out the main topics of interest for type 1 diabetics. We will use unsupervised machine learning to explore these posts. Unsupervised machine learning is a class of techniques used to find pattern in data. Tha data given to an unsupervised algorithm will not be labeled - which means we will have only an input variable X - and no corresponding varriable. We will use K-means in order to explore the clustering of our data - and we will explore the silhouette score in order to obtain the best clustering choices.

### Provided Data

For this project we have four provided datasets scrapped using Pushshift's API  from 1 reddit subthreads.

---

###  Data Dictionary

For diabetes_t1_2.csv:

|Feature|Type|Description|
|---|---|---|
|**title**|*object*|post title|
|**selftext**|*object*|post text|
|**subreddit**|*object*|subreddit thread|
|**created_utc**|*int*|time|
|**author**|*object*|author|
|**num_comments**|*int*|number of comments|
|**score**|*int*|score|
|**is_self**|*bool*|is this the original post or a repost|
|**timestamp**|*object*|time|



---

### Executive Summary


We have obtained a set of data that contains posts from the the type 1 Diabetes subreddit thread for 100 days from 2019 - starting back from February 18th 2020. after dropping all the empty rows in our data, we are left with a total of 4283 posts. Our target is to analyze these posts using Natural Language Processing Unsupervised Machine learning and the K-Means clustering and see if any meaningful clustering will emerge, that will help us identify the topics of interest that emerge in the type 1 diabetic online community.

 K-means is a method of vector quantization, that is popular for cluster analysis in data mining which aims to partition n observations into k clusters in which each observation belongs to the cluster with the nearest mean, serving as a prototype of the cluster.

After we import our data, we tokenize it in order to clean the text and get it ready to be vectorized. We ran both CountVectorizer and TFIDF vectorizers on our text, and realized that TFIDF will make a better candidate for preprocessing our data in order to be clustered with the k-means model.

We have then decided to use TFIDF with a maximum number of 10000 features (that is tokenized words in our case). Once we have ran TFIDF on our posts, and obtained our sparse matrix, we proceeded to use it in order to calculate the silhouette score for a number of k (clusters) between 5 and 50. We aimed to find the highest silhouette score in order to find the best clustering. However, as soon as we ran our search and plotted our inertia and silhouette scores, we noticed that the silhouette score is very small - starts at 0.004, and at k=50 it starts to hover at 0.01, and that means for us that we wont be able to use it very efficiently in order to choose our cluster number. Still, we use the first observed "elbow" in our silhouette graph - at k=6 - and we decide on a clustering on 6 centroids.

We then proceed to analyze each cluster, and the words that have the highest TFIDF sum in the specific cluster, and their general frequency in the cluster. That way we will see what topics emerge from our analysis.



### Drawbacks, Conclusions, and Further Steps:


One of the drawbacks of this study is the limited number of posts. Possibly with more than 100 days - and more than 4200 posts - we would have had more information about the topics of interest for type 1 diabetics. At the same time, another limitation is the very close clustering - with the small silhouette score. A clustering on about 30 clusters would have made a small difference as the silhouette score would have been 0.01 and not 0.06 - but clustering on 30 clusters with only 4200 posts felt like it will become too granular.
Another drawback was the presence of the removed posts - which for further studies will have to be handled on a case by case basis - and removed posts will have to be verified individually before they can be dropped from the dataframe.

We conclude that the topics of interest for diabetics fall into several categories:
The largest group has to do with broadly with health insurance - and the blood tests that are considered essential for monitoring how well a diabetic's condition is managed.
A very large one - composed actually of three clusters we found, is the technology a type 1 diabetic can use in order to manage their condition - continuous glucose monitors of various kinds, and the pumps that can be used to administer the insulin without daily injections - and all the connected issues.
And the third large group has to do with managing the low blood sugar episodes, the high blood sugar episodes, disruption of sleep and the general diet followed.

After this brief study - we can see that the sources of stress as reflected by topics of discussion on the reddit forum seem to fall  under a couple of categories - health insurance and lack thereof, managing the technology used for monitoring the blood sugar and administering insulin, managing episodes of low or high blood sugar, and how they impact the diabetic's nights.

At the same time - we can safely draw the conclusion that the existence of online forums where type 1 diabetics exchange opinions offers comfort and help to thousand of people suffering from this condition. This is a daily struggle - and the people that understand it the best are people suffering from the same condition. From advice about technology, to a mere cry for help or compassion, social media can help diabetics feel less isolated, and get emotional support in a direct way from peers.

Further steps.
We would like to explore this subject further by acquiring more data and obtaining a stronger capacity processor, in order to find out if the clustering would look different on more than 4200 posts. The most important find that we would like to explore further is the fact that night disruption in type 1 diabetics is not explored as much as we would have thought. Exploring this topic would potentially lead to solutions that could improve a diabetic's quality of life.
