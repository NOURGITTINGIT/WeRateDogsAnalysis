In this project, before conducting the EDA (Exploratory Data Analysis), we started by wrangling our Data: which included gathering, assessing and cleaning. The gathering phase: We needed to gather the Data from three different sources. 

## Gathering
 
Actually, we gathered three different pieces of Data. The first one comes from the file provided by Udacity. We downloaded manually the twitter_archive_enhanced.csv file then uploaded it in the Jupyter Notebook. The second file, the image_predictions file were downloaded programmatically using the Requests library. For the third additional data the data was gathered using the Twitter API.

## Assessing : 

The assessing phase: I approached this step using both visual and programmatic assessment. I started by displaying the first and last five rows of the first dataset using both head() and tail(), then used info() to see how many non nulls values there is in each column and the columns types. I also used the value_counts() function on the name and denominator columns to display all the typed names and denominators. I looked for duplicated rows using .duplicated() and used the .sample() to display random rows. 
As a final step, I used list() to see all the datasets columns and then see what columns are duplicated. At the end of this phase I was able to detect those issues :

Quality The Enhanced Twitter Archive :
• There are some retweets in the Twitter Archive
• timestamp column is a string and not a datetime type
• tweet id is an integer not a string
• Some dogs names are given 'a' as a name when it should be None
• Some rating denominator values are not 10 
• Source column is highly duplicated
• Missing values in the columns in_reply_to_status_id and in_reply_to_userid Image predictions : 
• Dogs bread names in p1,p2 and p3 columns : lowercase and contains '' 
• tweet_id should be a string not an integer Additional Data :
• id should be a string not an integer
Tidiness :
• The presence of the tweet_id,in_reply_to_status_id ,in_reply_to_user_id, retweeted_status_id and retweeted_status_user_id breaks the tidy rule : each variable forms a column.
• The presence of 4 breed columns ( dogg, floofer, pupper and puppo ) instead of one column breaks the tidiness rule : Each type of observational unit forms a table
• retweet_count and favorite_count should be in the first dataset

## Cleaning :

The cleaning phase : I started by making a copy of every dataset to not lose the original ones. 
I dropped the rows where the retweet status id is not null. 
I then tackled the tidiness issues using the Define, Code and Test method. 
I made a new column 'stage' and merge the correspondant values from the doggo,floofer,pupper and puppo columns.
I merged the retweet_count and the favorite_count to the Enhanced Twitter Archive table. We need to change the id column name to the same twwet_id name in the first dataset to be able to merge it. 
I corrected the datatypes (tweet id and timestamp.
I changed the names ‘a’ to None.
I gave the value 10 to all denominators.
I dropped duplicated columns. 
I standardized the breed names.

After that, I stored the two resulting datasets.

## EDA : 

After gathering, assesing, cleaning and storing. It was time to conduct the EDA. We began the Analysis by rereading the two datasets previously stored into two dataframs df1 for the twitter archive master and df2 for the image predictions.
We started by presenting the questions we are going to answer with the analysis which are :

What dog breeds are the easiest to predict ?
What dogs' stage is the most liked ?
What are the days with the highest users' engagement ?

For the first question, we extracted a smaller dataset using the .query() function to only limit the analysis to the dogs with the first prediction rate higher than 0.85.
There were only 509 dogs presenting a p1_conf>0.85. 
Among, those dogs we applied the function value_counts on the p1 column : Golden Retriever is the easiet breed to recognize. Pembroke, Labrador Retriever and Pug are also not very hard to recognize.



For the second question :

I used groupby on the stage column then I  created 5 dataframes with the correspondant dog stage and compare their retweets and favorite.
Then, I checked for the mean value of the retweet counts to see which dog stage has the highest retweet counts : The doggo stage seems to be the most liked among these dogs since it has the highest retweets rate, then comes the puppo stage, the floofer stage comes third, the doggo,pupper stages fourth and lastly the pupper stage is the least retweeted.

For the third question : I extracted the name of the days from the timestamp column, then made 7 boxplots corresponding to each day and the retweet counts :  Wednesday and Monday seem to be the days where people engaged more with the dogs pictures by retweeting them.



```python

```
