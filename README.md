# FakeJobPosting
A NLP model trained for detect fake job posting online

**Motivation and Background**

The increase in job demand along with the development of the internet has caused the emergence
of LinkedIn, a company whose website permits people to put their resume on the website and
seek job opportunities via online HR of different companies. As the rapid growth of online forms
of job application, people are getting used to browsing job opportunities and applying for jobs.
However, since more people take the online job application seriously under a competitive job
market, the online job fraud also appears throughout the internet.

Data Mining techniques play an important role in analysing and finding scams across the internet

due to the mega amount of data that was generated everyday. It can be applied in discovering

patterns for such inappropriate behaviors. The continuously increasing user amount indicates that

finding a better and more efficient way to detect if there is a fraud job information listing is

strongly needed. Through its application, the users are able to find positions they want with

lower risk to be scammed, which also creates a more efficient and safe job-matching online

platform. [6]

**Data Description**

Our dataset contains about 18k of online job postings across different areas such as marketing,

sales, and engineering etc. This dataset has 18 columns which describe the job features. Each of

the jobs has its unique job\_id and title. Location represents the geographical location of the job

ad. Company\_profile is a brief of the company and requirements are the listed requirements of

the job opening. Description is the most important column for our mining process, which is the

detail of the job ad. Most of the columns are in text form so our data mining model faces an

important challenge of processing the natural language. The column fraudulent is our target

feature for classification. For all of the job postings, 800 of them are job scams. [1]

**Related Work**

In an article called ‘Data Entry Job Scams’ by Alison Dolye, he listed several types of job

fraudulence. According to the article, most of these fake jobs are asking for money, such as a

‘training program’, others sound ‘too good to be true’. (Doyle, 2019) More research and signed

contracts are needed for such companies. This article inspired us about what kind of patterns

shall we focus on through the project and reassure the importance of developing that. [2]

In further researching, we didn’t find any specific program done by others, so we have to base on

the dataset we collected. By comparing the top list of fake job types, it helps us to define which

columns we might need and which information is non-related to what we are going to do. More




<a name="br3"></a>specific approach is listed below. However, job scamming is just a small part of online scams.

With the rising of social media platforms, different types of scam appeared across the internet. A

lot of data scientists use different approaches to solve such problems. They also provide us a lot

of insights when we are discovering our topic.

**Methodology**

**Data Preprocessing**

The whole project starts from data processing, which allows us to extract the data we want and

delete the missing or non-related columns from the dataset. This part is important since the

choosing of data defined the performance of our models. First, we discard some of the columns

that are not deeply correlated with data mining processes such as job\_id, title, location. Second,

there are a lot of null and missing values in this dataset, so we decided to delete these columns

with almost half of the value missing such as "department"(64.58% null), "salary\_range"(83.96%

null), "benefits" (40.32% null), "required\_education (45.33% null)" etc. The remaining dataset

consists of "telecommuting", "has\_company\_logo", "has\_questions", "description", "fraudulent".

The column "description" has the detailed description of the job posting which would be the

most helpful column for the prediction.



<a name="br4"></a>From the plot above, the original dataset has a serious imbalance problem. We extract all the

fraudulent job postings and concatenate them with 1000 random sampled real job postings, so

that the data now consists of 865 fake job postings and 1000 real job postings.

**Natural Language Processing**

For a text classification model, the NLP is the most important part. By NLP, we can let the

computer understand human’s natural language. [2] We need to preprocess the text of the

‘description’ column, which is also the most important column since most of the fake

information is detected through this column. we firstly use the nltk model to tokenize all the text

in description.

The second step is vital, which is to featurize the tokenized text. We compared several NLP

words to the feature model such as TF-IDF, Bag of Words (BoW), and word2vec. We found out

that the Skip-gram model in word2vec is the best solution in our case. For TF-IDF and BoW

models, the dimension of the features after extracting all the features in the text is directly

correlated with the number of non-repeating words across all the tokenized words in the text. It

represents the count of the word in the data. For example, if the data has 20000 non-repeating

words, the dimension of the features for BoW would be 20000. If we apply this trained model by

the data into a specific text, we will get a sparse vector which most of the dimensions are zero,

because the text may just include a little amount of words in the data. This will waste the space

and increase the complexity of the algorithm because the sparsity of the data.[3] In addition,

TF-IDF and BoW models do not take the semantic meanings into account. As a result, both of

these models exist problems like sparse vectors and the number of dimensions are too high,

which may have to sort again before application.[4] Word2vec uses Skip-gram or CBOW model

to represent the words numerically. The Skip-gram model uses a word in the text to predict the

context while the CBOW model uses the context to predict the word. We can set the size of the

word embedding so the feature vector is dense. And the word2vec model could understand the

semantic of the model and extract the order feature between words. After we featurize all the

tokenized words, we calculate the mean of each of the word embeddings to represent the density

of this particular feature.




<a name="br5"></a>**Classification Analysis**

After we featurize all the text, we can apply the text classification algorithms. After the data

preprocessing step, we only left a relatively small dataset. So we choose to apply k-fold cross

validation to ensure that each of the job postings has a chance to be in the train or test set. Then

we choose three classification algorithms to build the model, which are logistic regression, SVM

machine, and neural network classifier. We choose to use logistic regression since the essence of

logistic regression is a linear regression with the sigmoid function which will also show the

direction of association, which is suitable for text classification models. Also, since the

dimension of our featurized vector is 300 which is relatively large, the SVM machine is also a

good choice.

**Experiment**

Logistic Regression:

||<p>Run time: 2.19</p><p>second</p>||mean Standard dev min max|
| :- | :- | :- | :- |
Accuracy 81.39% 2.39% 77.96% 86.1%

Precision 81.49% 2.34% 78.44% 86.18%

Recall 81.39% 2.39% 77.96% 86.1%

F1 81.34% 2.43% 77.67% 86.05%




<a name="br6"></a>SVM:

||<p>Run time: 10.35</p><p>second</p>||mean Standard dev min max|
| :- | :- | :- | :- |
Accuracy 79.67% 3.07% 75.81% 85.03%

Precision 79.84% 2.94% 76.57% 86.18%

Recall 79.67% 3.07% 75.81% 85.03%

F1 79.60% 3.13% 75.35% 85.00%

FNN:

||<p>Run time: 25.88</p><p>second</p>||mean Standard dev min max|
| :- | :- | :- | :- |
Accuracy 87.24% 2.12% 81.82% 89.25%

Precision 87.34% 2.00% 82.43% 89.28%

Recall 87.24% 2.12% 81.82% 89.25%

F1 87.23% 2.13% 81.83% 89.25%

Among these three classification models, FNN provides the best result while taking most of the

time. Logistic regression provides a relatively good accuracy and precision while taking the least

of time. SVM doesn’t work that well since most of its measures are around 79 percent and the

runtime performance is around 10 seconds. After all, all these three models provide a not bad

result which is acceptable.

**Conclusion**

The work we’ve done is not perfect. Although we are unable to detect every specific fake job,

this project did achieve most of our thoughts and has a bright future. First thing we can improve

is the data collection. We collected the data from an easy way instead of mining current real

information from job platforms since it will be hard to operate. So we had to delete a lot of

missing or useless data to apply analysis models. Also, since the number of fake jobs are far less

than real jobs, to improve the performance, we have to select only part of the real jobs.
