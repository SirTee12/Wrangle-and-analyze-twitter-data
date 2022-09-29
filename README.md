# Wrangle-and-analyze-twitter-data
The aim of the project is to demonstrate data wrangling and cleaning skills. Three dataset were used.
+ The first dataset (twitter_archive_enhanced.csv) was already provided. The second
dataset (image_predictions.tsv) was extracted from a url using **requests** library and
stored using the **os** library. The third dataset was extracted from twitter using the
tweepy API library with the help of twitter's consumer tokens and access tokens. The
twitter information gotten was written into text file (tweet_json.txt) the and the
reqiured information for the analysis (tweet id, retweet count, favorite count) were
extracted from the json file directly. This information was appended to a list and
converted to a dataframe which then saved as a csv file using pandas to_csv() as
json_tweets.csv
+ All three datasets were read into the notebook using pandas **read_csv()**.

## Accessing
### Visual assessment:
+ Copies of each dataset were made and then they were assessed visually by printing
first few rows using the pandas **head() and sample()** method.

### Quality and Tidiness isuues discovered:
+ Column in_reply_to_status_id, in_reply_to_user_id, retweeted_status_id
retweeted_status_user_id and retweeted_status_timestamp contains null values
+ Column headers doggo, fluffer, pupper and puppo are values not headers
+ incorrect dog like a and None
+ p1, p2, p3 in the image prediction dataset having underscore.
+ Presence of duplicate rows
+ Missing records due to missing tweet ids

### Programmatic Assessment
This was done using the **decribe(), duplicated(), info()** and also searching for specific
info about the datasets using the comparison operators

### Quality and Tidiness issues discovered
+ Erroneous data types
+ Outliers in the rating_numerator e.g minimum value of 0 and maximum of 1776. There are
+ Other apart from these.
+ Rating denominator value of None and less than 10
+ Only one table should exist

## Cleaning
+ Missing records due to missing tweet ids: the datasets (twittwer_enhanced_df and
json_tweet_df) were merged together on the tweet_id using the **merge()** method to
create uniformity
+ Column headers doggo, fluffer, pupper and puppo are values not headers: a function
was written to extract the count of each dog stage which was appended to a list. The
function was applied to the twitter_archive _df (contains the merged data) and a
column for the dog_stage was created
+ Erroneous data types: All wrong data types (timestamp, dog_stage, tweet_id) were
converted to the right ones using **astype()**
+ Outliers in the rating_numerator e.g minimum value of 0 and maximum of 1776. There
are other apart from these: Rows with a rating numerator of 0 in the
twitter_enhanced_df were dropped using **drop()**. Higher values of rating numerator
are vaid so they are left as they are.
+ Rating denominator value of None and less than 10: the values were replaced by 10
using **replace()**
+ Only one table should exist: the image_predictions_df was merged with
twitter_enhanced_df on the tweet_id.
+ Only true prediction with their confidence level are needed: a function was written to
extract only the true predictions with their respective confidence levels to form new
columns called prediction and confidence in the twitter_archive_df.
+ p1, p2, p3 in the image prediction dataset having underscore: the underscore was
replaced with empty string using **str.replace()**.
+ Incorrect dog like a and None: Dogs names with None were left as they are but incorrect dog names like
a, quite etc and **str.contains()** together with a regex pattern wasused to print them all out 
before using **str.replace()** with the same regex pattern toreplace those names with
None.
+ Presence of duplicate rows: the rows with retweet information were isolated by subsetting 
the twitter_archive_df for row with non_empty values for the specifi ccolumn of interest. 
The index for these isolated dataframe was extracted using indexattribute and stored as a list 
using **list()**. A for loop was used to iterate through the listand index in the list present in 
the twitter_archive_df was dropped

## Analysis and Visualization
Due to the aim of the project, no indepth analysis was performed. The analysis performed was
to get general view, distribution and area of focus of the data.
