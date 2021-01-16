# &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   News Article Classification

### Table of Content:
-	[About the project](#about-the-project) 
-	[Understanding the data](#understanding-the-data)
-	[Deduplication and handling null values](#deduplication-and-handling-null-values)
-	[Cleaning the text:](#cleaning-the-text) 
- [Make Balanced Dataset](#make-balanced-dataset)
-	[Tfidf Vectorization](#tfidf-vectorization)
-	[Time for training and testing](#time-for-training-and-testing)
- [Conclusion and About Author](#conclusion-and-about-author) 

# About the project:
In this article, we will see the text classification model using NLP and machine learning. For this project, I Collected the Dataset from Kaggle named [News Category Dataset](https://www.kaggle.com/rmisra/news-category-dataset).
This dataset is in JSON format with a 200853 sample and 6 features. The news articles are classified under 41 categories. let's see the implementation and analysis.

# Understanding the data
he data was in JSON format after reading, I dropped some unnecessary features like date,image_url, and continued with the feature only I need.
Let’s analyze the category column.
![Screenshot (409)](https://user-images.githubusercontent.com/51699297/104182031-d34d7200-5435-11eb-8d8d-aca29b34bc94.png)

- As shown in the figure, there are 41 categories, some of them like Education, College and others are having a very small number of  samples. The model accuracy may be decreased due to the imbalance in the categories. So, we have to take care about the imbalance and have to downsample this dataset to some certain threshold value. We can see how this should be done in later on this article.,<br/>

- We can analyze  the authors and their articles. Here you can see the number of articles under the top 25 authors. The author named  <b>”Lee Moran”</b>  released 2,000+ articles.<br/>

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
This means there are no null values. Is our data contains no null values?? It’s so rare, In our case the null values are filled with empty strings(‘’) .<br/>


![Screenshot (402)](https://user-images.githubusercontent.com/51699297/104180572-5b7e4800-5433-11eb-858c-396a81e4fd0d.png)


With these lines of code, I am removing all the null values and continue further.<br/>

After all I combined all the 2 feature(headline,short_description)  into one features(text). Now, our dataset looks like below and we are ready for cleaning and vectorization.<br/>

# Cleaning the text:

Cleaning the text involves removing the unnecessary whitespaces, convert the capital letters to smaller ones, and remove symbols. With the below line of code, I am cleaning the text and splitting it for training and testing. <br/>

![Screenshot (403)](https://user-images.githubusercontent.com/51699297/104180597-633dec80-5433-11eb-9ed0-eef3aaa3ff2e.png)

# Make Balanced Dataset:
- Our model needs a  balanced dataset, which means all categories must have the same number of samples, then only we can get better performance. For this, I have dropped the “Education, Style, College, Environment ,etc “ categories which all have a very small number of samples, and selected 3000 samples from the remaining 15 categories, now our dataset has 45000 samples under 15 categories. 
- Now, our dataset’s category distribution is looks like below,

![Screenshot (418)](https://user-images.githubusercontent.com/51699297/104292151-7956b600-54e2-11eb-85dc-7543e38aed26.png)

- With this dataset, we are continuing the Vectorization and Training, finally we are going to Evaluate our 5 different model’s training and testing performance. 

# Tfidf Vectorization:
- TF-IDF is an abbreviation for Term Frequency Inverse Document Frequency. This is very common algorithm to transform the text into a meaningful representation of numbers, which is used to fit a machine algorithm for prediction.
- It is a measure of the originality of a word by comparing the number of times the word appears in the document with the number of documents the word appears in.
- One can also use the TfidfTransformer, which will give you the same result but, it will take a few more extra steps than Tfidfvectorizer.
- This model will find the importance of each word in the given documents. The word which appears more time will get a lesser score. The vocabulary which has a lesser score will get less importance. Likewise, the word which appears fewer times will get a higher score and high importance.
 - [Reference1](https://medium.com/@cmukesh8688/tf-idf-vectorizer-scikit-learn-dbc0244a911a),[Reference2](https://kavita-ganesan.com/tfidftransformer-tfidfvectorizer-usage-differences/#.X_xudegzbIU),[Know about the IDF](https://kavita-ganesan.com/what-is-inverse-document-frequency/#.X_xuzugzbIU)
<br/><br/>
Using this Tfidfvectorizer, I vectorized the document and made it ready for the training.

# Time for training and testing:
I have trained my data with 5 different models lets see the report of those models.<br/>

![Screenshot (417)](https://user-images.githubusercontent.com/51699297/104292221-9095a380-54e2-11eb-9d59-7128f868c44d.png)

# Conclusion and About Author:
 Finally amoung all the model I have tried , The <b> Logistic Regression</b> gives me the high performance.
 
 - You can also view the code here----------------------------------------------> [Kaggle Notebook](https://www.kaggle.com/ninjaac/text-classification-newss), [GitHub Code](https://github.com/pavi-ninjaac/Specrom_Analysis/blob/main/Internship_works/week2/text-classification-newss.ipynb) 
 - You can collect all the images used in this article here-----------------------> [Image Folder](https://github.com/pavi-ninjaac/Specrom_Analysis/tree/main/Internship_works/week2/article_images)
 - You can get the pretrained logistric Regression model as a sva file here ---> [Pretrained Model](https://github.com/pavi-ninjaac/Specrom_Analysis/blob/main/Internship_works/week2/logistricRegression_text_classi.sav)
 
### About the Author:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  I am <b><i>Pavithra Devi M</i></b>, a Computer Science Engineering student. Being a Computer Science student, I always love to learn new techniques every day. Put my dreams and aims apart,” I always want to be the best person where I am in”. One day I stumbled upon one application that can say your health condition with your DNA Sequences. Without knowing anything about ML & DL stuffs that day, I really wondered and got interest in Machine Learning and AI. I have Started understanding Maths and Machine Learning Algorithms. Got some experience through different internship and live projects in this field.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Currently pursuing mine under graduation from University College of Engineering BIT Campus, Anna University at Tamil Nadu, India. And as a Data Science Intern at Specrom Analytics learning lots of NLP stuffs through different projects and data. Now I am participating in lots of Competitions, the open-source community works to enhance my skills and to get more knowledge that can not be learned through books and projects. That makes me more confident and clear. My current ambition is to be a part of a world-level project which will change this whole world.<br>
- Gmail : pavipd495@gmail.com
- GitHub : @pavi-ninjaac
- Contact number : 7904014309
- LinkedIn : @Pavithra Devi M
 



