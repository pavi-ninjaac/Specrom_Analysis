# &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   News Article Classification
### Table of Content:
-	[About the project](#about-the-project) 
-	[Understanding the data](#understanding-the-data)
-	[Deduplication and handling null values](#deduplication-and-handling-null-values)
-	[Cleaning the text:](#cleaning-the-text) 
-	[Team members](#team-members)
# About the project:
This is a text classification project, here I calssified the news article under different categories. For this project I Collected the Dataset from Kaggle named [News Category Dataset](https://www.kaggle.com/rmisra/news-category-dataset)
This dataset is in jason format with 200853 sample and 6 features. The news articles are classified under 41 categories. let's see the implementation and analysis.

# Understanding the data
The data was in json format after reading, I dropped some unnecessary features like date,image_url and continued with the feature only I need.<br/>
Let’s analyses the category column.<br/>
pie chart

As shown in figure, there are 41 categories, some of them like Education, College etc are having very small samples and Similar in nature. The model accuracy may decreased due to the imbalance in category. So, I merged up some of the category and named it. you can see the new categories and its name below. Noe there are only 19 categories,<br/>

barchart
We can analyse the authors and their articles. Here you can see the number of articles under the top 25 authors. The author named  <b>”Lee Moran”</b>  released 35,000+ articles.<br/>
Author_bar

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

After all I combined all the 3 feature(author,headline,short_description)  into one features(text). Now , our dataset looks like below and we are ready for cleaning and vectorization.<br/>

# Cleaning the text:
Cleaning the text involves removing the unnecessary whitespaces, convert the  capital letters to smaller one and remove symbols . with the below line of code I am cleaning the text and splitting it for training and testing. <br/>

![Screenshot (403)](https://user-images.githubusercontent.com/51699297/104180597-633dec80-5433-11eb-9ed0-eef3aaa3ff2e.png)
