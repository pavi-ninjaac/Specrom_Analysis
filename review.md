# &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   News Article Classification
### Table of Content:
-	[About the project](#about-the-project) 
-	[Understanding the data](#understanding-the-data)
-	[Deduplication and handling null values](#deduplication-and-handling-null-values)
-	[Cleaning the text:](#cleaning-the-text) 
- [Make Balanced Dataset](#make-balanced-dataset)
-	[Tfidf Vectorization](#tfidf-vectorization)
-	[Time for training and testing](#time-for-training-and-testing)
- [Conclusion](#conclusion) 

# About the project:
This is a text classification project, here I calssified the news article under different categories. For this project I Collected the Dataset from Kaggle named [News Category Dataset](https://www.kaggle.com/rmisra/news-category-dataset)
This dataset is in jason format with 200853 sample and 6 features. The news articles are classified under 41 categories. let's see the implementation and analysis.

# Understanding the data
The data was in json format after reading, I dropped some unnecessary features like date,image_url and continued with the feature only I need.<br/>
Let’s analyses the category column.<br/>

![Screenshot (409)](https://user-images.githubusercontent.com/51699297/104182031-d34d7200-5435-11eb-8d8d-aca29b34bc94.png)

As shown in figure, there are 41 categories, some of them like Education, College etc are having very small samples and Similar in nature. The model accuracy may decreased due to the imbalance in category. So, I merged up some of the category and named it. you can see the new categories and its name below. Noe there are only 19 categories,<br/>

![Screenshot (408)](https://user-images.githubusercontent.com/51699297/104182037-d7798f80-5435-11eb-8aa5-e49e1dd1f751.png)

We can analyse the authors and their articles. Here you can see the number of articles under the top 25 authors. The author named  <b>”Lee Moran”</b>  released 2,000+ articles.<br/>

![Screenshot (407)](https://user-images.githubusercontent.com/51699297/104182043-d8aabc80-5435-11eb-8a56-2dce6d13a67b.png)

# Deduplication and handling null values:
The next important step is to remove the duplicates,<br/>
```
data.drop_duplicates(subset=['headline', 'short_description'],inplace=True,keep='last') 
```
With this line of code I removed the duplicates by ‘headline and short_description’ was removed. It’s time for remove the null values.<br/>
```
data.isnull().sum() #output is Zero
```
This means there is no null values. Is our data contains no null values?? It’s so rare, In our case the null values are filled with empty strings(‘’) .<br/>


![Screenshot (402)](https://user-images.githubusercontent.com/51699297/104180572-5b7e4800-5433-11eb-858c-396a81e4fd0d.png)


With this lines of code I am removing all the null values and continue further.<br/>

After all I combined all the 2 feature(headline,short_description)  into one features(text). Now , our dataset looks like below and we are ready for cleaning and vectorization.<br/>

# Cleaning the text:
Cleaning the text involves removing the unnecessary whitespaces, convert the  capital letters to smaller one and remove symbols . with the below line of code I am cleaning the text and splitting it for training and testing. <br/>

![Screenshot (403)](https://user-images.githubusercontent.com/51699297/104180597-633dec80-5433-11eb-9ed0-eef3aaa3ff2e.png)

# Make Balanced Dataset:
- Our model much be balanced , that means all categories must have almost same number of samples then only we can get better performance. For this, I have dropped the “Education ,Style ,College ,Environment “ categories which all have very same number of samples, and selected 3000 samples from remaining 15 categories , now our dataset  has 45000 samples under 15 categories. 
- Now, our dataset’s category distribution is looks like below,



- With this dataset we are continuing the Vectorization and Training and then finally we are going to Evaluate our 5 different model’s training and testing performance. 

# Tfidf Vectorization:
- TF-IDF is an abbreviation for Term Frequency Inverse Document Frequency. This is very common algorithm to transform text into a meaningful representation of numbers which is used to fit machine algorithm for prediction.
- It is a measure of originality of a word by comparing the number of times the word appears in the document with the number of documents the word appears in.
- One can also use the TfidfTransformer which will give you the same result,but will take few more extra steps than Tfidfvectorizer.
- This model will find the importance of each word in the given documents. The word which appears more time will get lesser score , lesser score will leads to less importance , like wise the word which appears less times will get higher score and high importance.
 - [Reference1](https://medium.com/@cmukesh8688/tf-idf-vectorizer-scikit-learn-dbc0244a911a),[Reference2](https://kavita-ganesan.com/tfidftransformer-tfidfvectorizer-usage-differences/#.X_xudegzbIU),[Know about the IDF](https://kavita-ganesan.com/what-is-inverse-document-frequency/#.X_xuzugzbIU)
<br/><br/>
Using this Tfidfvectorizer, i vectorized the document and made ready for the training.

# Time for training and testing:
I have trained my data with 5 different models lets see the report of that models.<br/>

![Screenshot (411)](https://user-images.githubusercontent.com/51699297/104228830-66f06400-5471-11eb-8ff0-1231191c026f.png)

# Conclusion:
 Finally amoung all the model I have tried , The <b> Logistic Regression</b> gives me the high performance.
