Project 3: Bodyweight Fitness and Powerlifting Subreddit Analysis

### Problem Statement

CRUNCH Fitness, an international fitness center and gym with more than 225 locations, wants data to help build an online fitness store and streaming service. Crunch needs to know how to market to different segments of the fitness market, specifically Bodyweight Fitness and Powerlifting.


#### Executive Summary

The purpose of this project was to use subreddit text in order to gain insights on the subreddit communities. Using the Bodyweight Fitness and Powerlifting subreddits, I applied Natural Language Processing and several decision tree models to explore the data and make predictions. The results were intended to help fitness industry companies make more targeted decisions in online content, online stores, and physical locations. 

---

### Project Files

README.md
Project3_Bodyweight Fitness and Powerlifting Analysis.pdf
Code Directory
- Data_Collection
- Data_Cleaning
- EDA
- Modeling_the_Reddit_Data


---

### Data Collection and Cleaning

The first step in this project was collecting reddit data from reddit.com. Pushshift.io reddit API facilitated the data collection by collecting 100 posts per request and restricting the search to a specific subreddit. Additionally, pushshift has a "before" parameter that allowed me to specify the date and time of the desired posts. I collected 20,000 posts total - 10,000 from Bodyweight Fitness subreddit and 10,000 from Powerlifting subreddit. I collected these posts with a loop that allowed me to gather 100 posts at a time, which is the limit of pushshift.io. I was able to use the oldest utc date/time of each 100 post batch in order to gather the next 100 older posts. Per best practices, I slowed the loop to run every three seconds so as to not overwhelm the reddit website. 
<br>
To clean the data for EDA and modeling, I first selected three relevant columns - title, selftext, and subreddit. About 2,800 rows in the selftext column had null values. Instead of deleting these rows, I replaced the null values with empty strings. This allowed me to combine the title and selftext values into one column labeled all_text. I also replaced strings that said “[removed]” and “[deleted]” with empty strings. In this way I was about to retain thousands of rows in the dataset. 
<br>
By utilizing Natural Language Toolkit (nltk) and regular expressions I further cleaned the data. These steps included making all letters lowercase, removing numbers, removing the subreddit names, applying stop words to remove nonsense words, and restricting the vectorizers to “min_df=3” to remove the noise. I used the tf-idf vectorizer and count vectorizer to create two CSV files. I also saved the cleaned data before the vectorizer step to a CSV file. 

---

### EDA
Analysis of Word Occurences: 
<br>
The bodyweight fitness reddit reveals several themes:
- Website usage: Three of the top 15 words are "http", "www", and "com". Through further investigation I determined that these are websites and links that are references to workout videos, exercise guides, and progress photos. This suggests that this community is open to researching and collecting pieces for their fitness program. 
- Time oriented: Words that reference time include "routine", "progress", and "day". 
- Fitness Terms: "Weight" is the second ranked word; however, this is not referencing kilograms or pounds like the powerlifting reddit. The top 50 words focus on bodyweight exercises such as "pushup", "pull", "dip" and "squat. Additionally, terms like "fit" and "exercise" point to a more rounded program rather than specific muscle groups. 

The powerlifting reddit points to a different type of workout program:
- Weights: The top words are "kg" and "lb". The reddit is dominated by discussion and programming focused around the amount of weight for exercises. 
- Exercises: Complimenting the focus on kilograms and pounds are the other most frequent words that highlight the powerlifters most important exercises. These include "squat", "bench", "deadlift", and "powerlift". Other frequent words put the exercises in context. The focus is on the "lift", "bar" (barbell) and "pr" (person record). Additionally words like "gym" and "program" are found in this subreddit.


### Modeling

I built three models to evaluate the Reddit posts including the following: Decision Tree, Random Forest, and Boosted Random Forest. The goal of each model was to beat the baseline score, which was 50%. The Decision Tree was the worst model. It had a score of 99% indicating it was overfit to the training data and would not generalize well to new datasets. The Decision Tree had the lowest accuracy, sensitivity and recall scores out of the three models. The Random Forest was also overfit with a score of 99%. Its accuracy was 91%, precision was 93% and specificity was 93%. The Boosted Random Forest was the best all-around model. The training set score was 93% and the testing set score was 92%, indicating that the model was not overfit.  Its accuracy was 92%, precision was 90% and specificity was 93%. For each model, I used a grid search to help tune the parameters. Unfortunately the processing power of my computer limited the number parameters I could test. 


### Recommendations

My advice to fitness companies was targeted to the subreddits. The bodyweight fitness community had a broad footprint across the web. They tended to post websites to their submissions that included workout programs, streaming workouts, and progress photos. The data suggests an opportunity to target this community with online services and online stores. The powerlifting community focused more on a physical gym presence and heavy duty equipment. Fitness companies would need to consider how to cater to this community in person or get the equipment into the homes of these people. Both communities had an emphasis on programming fitness.  

---