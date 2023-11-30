# Uncovering-Coordinated-Twitter-Campaigns

## Introduction
Social media platforms have become an integral part of our daily lives, and Twitter is no exception. With millions of tweets being posted every day, analyzing Twitter trends can provide valuable insights into the opinions and interests of people around the world. This project is an in-depth analysis of 10 different Twitter trends, with a particular focus on trends in political campaigns during the Indian General Election in February 2019. During this period, two prominent Twitter trends emerged: one in support of Prime Minister Narendra Modi with the hashtag #Welcomemodi, and the other against him with the hashtag #Gobackmodi. These hashtags highlight the polarized political landscape and demonstrate how social media platforms like Twitter serve as battlegrounds for political discourse and campaigning.

To analyze these trends, PySpark was utilized for efficient data processing and analytics on the collected tweets. PySpark, a powerful big data processing framework, enabled the handling of large datasets and the extraction of meaningful insights. The data processing involved cleaning the tweets and removing irrelevant information to understand the overall dynamics of the trends related to each hashtag. Key findings and results were derived from this analysis. The hashtags #Welcomemodi and #Gobackmodi exhibited a mix of activities, indicating the contentious nature of political discussions on social media. The analysis also revealed patterns in tweet activity, such as peaks during specific times of the day or in response to particular events.

This project aims to help the intended audience and the broader community better understand the significance and implications of Twitter trends. By analyzing these trends, we can gain insights into public opinion, identify influential voices in social media discussions, and understand the dynamics of online engagement. Moreover, the project seeks to develop tools, such as a dashboard, that can monitor trends in real-time and distinguish between genuine trends and artificially inflated ones. Such tools are crucial in an era where social media manipulation is a growing concern.

## Data Collection
The data collection process for this project involved using the Twitter API to retrieve tweets for each of the 10 selected trends. The Twitter API provides a powerful and flexible way to access Twitter's vast amount of data. By leveraging this API, we were able to collect tweets that matched specific search criteria designed to capture the most relevant information for our analysis. To ensure a comprehensive dataset, specific search queries were constructed. These queries included relevant hashtags, keywords, and precise timeframes to target the periods of peak activity for each trend. For instance, for the political trends during the Indian General Election in February 2019, we focused on hashtags such as #Welcomemodi and #Gobackmodi to capture the discourse surrounding Prime Minister Narendra Modi.

Each tweet was represented as a JSON object that contained various fields such as user information, date and time of the tweet, tweet content, and engagement metrics such as retweets and likes.

### Dataset Description
* tweet.card: The Twitter card type of the tweet.
* tweet.cashtags: The cashtags used in the tweet.
* tweet.content: The text content of the tweet.
* tweet.conversationId: The ID of the conversation thread that the tweet is a part of.
* tweet.coordinates: The geolocation coordinates associated with the tweet, if any.
* tweet.date: The date and time when the tweet was created.
* tweet.hashtags: The hashtags used in the tweet.
* tweet.id: The unique ID of the tweet.
* tweet.inReplyToTweetId: The ID of the tweet that this tweet is in reply to, if any.
* tweet.inReplyToUser: The username of the user that this tweet is in reply to, if any.
* tweet.json: The raw JSON data of the tweet.
* tweet.lang: The language of the tweet.
* tweet.likeCount: The number of likes that the tweet has received.
* tweet.links: The URLs included in the tweet.
* tweet.mentionedUsers: The usernames of the users mentioned in the tweet.
* tweet.place: The name of the place associated with the tweet, if any.
* tweet.quoteCount: The number of times that the tweet has been quoted.
* tweet.quotedTweet: The ID of the tweet that this tweet has quoted, if any.
* tweet.rawContent: The raw content of the tweet.
* tweet.renderedContent: The rendered content of the tweet.
* tweet.replyCount: The number of times that the tweet has been replied to.
* tweet.retweetCount: The number of times that the tweet has been retweeted.
* tweet.retweetedTweet: The ID of the tweet that this tweet has retweeted, if any.
* tweet.source: The source from which the tweet was posted (e.g., Twitter for iPhone).
* tweet.user: The ID of the user who posted the tweet.
* tweet.username: The username of the user who posted the tweet.
* tweet.vibe: The sentiment score of the tweet.
* tweet.viewCount: The number of times that the tweet has been viewed.

## Data Cleaning and Preprocessing 
After loading all the datasets into one, a series of data cleaning and preprocessing steps were performed on the Twitter data to ensure it was in a usable format for analysis. First, missing values in each column were checked and the 'Unnamed: 0' column was dropped, as it was an artifact from the data import process and did not contain any useful information.

Next, the 'date' column was cast to a timestamp data type to facilitate time-based analyses. Unwanted columns such as 'card,' 'cashtags,' 'coordinates,' and others that were not relevant to the analysis were also dropped.To handle missing values, numeric columns with missing values were filled with 0, and empty strings in text columns were replaced with 'None' values. This step ensured that the dataset was complete and that missing data did not skew the analysis.

For text data preparation, several cleaning steps were performed:
* All text was converted to lowercase to ensure consistency.
* Leading and trailing spaces were removed to avoid any inaccuracies in text analysis.
* Duplicate whitespaces were eliminated, and any remaining multiple whitespaces were replaced with single whitespaces.

Overall, these data cleaning and preprocessing steps were crucial to ensure the data was in a usable format for analysis. By removing unnecessary columns and filling missing values, the noise in the data was reduced, ensuring that the analysis was based on a complete and clean dataset.

## Data Architecture
The project started with the goal of analyzing Twitter data related to a particular hashtag to gain insights. To achieve this, a cloud-based architecture was used to handle the large volume of data and the processing required.

Initially, Snscrape and Sntwitter were used for data collection. Then, TwitterSearchScraper was employed to retrieve Twitter data related to the hashtag and dump it into an S3 bucket in JSON format. S3 was chosen because it is a scalable and cost-effective way to store large volumes of unstructured data. Next, PySpark was used to perform data cleaning, analysis, and structuring of the data on AWS EMR. PySpark's capabilities allowed for efficient handling and processing of large datasets. After cleaning and processing, the data was stored in a structured form in Parquet format back in S3. Parquet was chosen because it is a columnar storage format optimized for performance and can handle large datasets efficiently.

Finally, the structured data from S3 was loaded into AWS Redshift, a cloud-based data warehousing solution. Redshift was chosen for its ability to perform high-speed querying and efficiently manage large volumes of structured data. AWS QuickSight was then connected to Redshift to create an interactive dashboard that provides real-time insights into user sentiment and behavior related to the hashtag.

<img width="1006" alt="Screenshot 2024-08-06 at 1 33 42 PM" src="https://github.com/user-attachments/assets/7bf28f0d-dadf-424c-89a6-cbb49f43634d">

This architecture ensured efficient data collection, processing, and analysis, leveraging the scalability and performance benefits of AWS services to derive valuable insights from Twitter data.

## Twitter Trends Analysis: #Gobackmodi vs #Welcomemodi
During the Indian General Election in February 2019, two significant Twitter trends emerged: one in support of Prime Minister Narendra Modi with the hashtag #Welcomemodi, and the other against him with #Gobackmodi. Data engineering and analytics techniques were employed to extract and process data related to these two trends to gain insights into user engagement and sentiment.

For the anti-Modi campaign (#Gobackmodi), the following observations were made:
* Total Tweets: 57,202
* Total Retweets: 188,825
* Total Likes: 289,639
* Tweet Engagement: 18% of tweets had more retweets than likes.
* Duplicate Tweets: 19% of tweets were duplicates.
* Distinct Users: 14,162 distinct users.
* Average Retweets per Account: Four retweets.
* Average Time Gap Between Tweets: 2,248 minutes.
* Quote Tweets: 17,658
* Replies: 24,039
* Common Users in Trends: Only 2.86% of users were common between the trends.

For the pro-Modi campaign (#Welcomemodi), the data revealed:
* Total Tweets: 32,493
* Total Retweets: 75,053
* Total Likes: 114,410
* Tweet Engagement: 18% of tweets had more retweets than likes.
* Duplicate Tweets: 40% of tweets were duplicates.
* Distinct Users: 5,992 distinct users.
* Average Retweets per Account: Three retweets.
* Average Time Gap Between Tweets: 455 minutes.
* Quote Tweets: 7,490
* Replies: 10,014
* Common Users in Trends: Only 2.86% of users were common between the trends.

These findings provide insights into the engagement and sentiment associated with each campaign. The similarity in the percentage of tweets with more retweets than likes across both trends suggests similar patterns in user engagement. However, the higher proportion of duplicate tweets in the pro-Modi campaign and the differences in the average time gaps between tweets reflect distinct characteristics in user behavior and campaign dynamics.

<img width="789" alt="Screenshot 2024-08-06 at 1 41 01 PM" src="https://github.com/user-attachments/assets/e37217cb-ce66-431f-92b5-d11a839cbf44">

<img width="679" alt="Screenshot 2024-08-06 at 1 41 25 PM" src="https://github.com/user-attachments/assets/66592684-1799-485a-bf50-e9ec1247f940">

Overall, this data visualization and analysis allowed for the identification of key patterns and insights into user engagement and sentiment within the two Twitter trends. By examining metrics such as tweet counts, retweets, likes, duplicate tweets, and engagement rates, the analysis revealed distinct characteristics of each campaign.

## Conclusion
In conclusion, this project on uncovering coordinated campaigns by analyzing artificial inflation of trend popularity on Twitter has successfully addressed its research questions and achieved its objectives. By analyzing a dataset of over 300,000 tweets, the project identified the presence of coordinated campaigns designed to artificially inflate trend popularity on Twitter. Key findings from the analysis included several notable trends and patterns, such as the high percentage of likes compared to retweets and the significant number of duplicate tweets. These insights reveal how engagement metrics can be manipulated and highlight the importance of scrutinizing social media data for authenticity.

Despite facing limitations and technical challenges during the project, an end-to-end data engineering and data visualization pipeline was developed using AWS technologies, including S3, EMR, Redshift, and QuickSight. This pipeline enabled efficient data processing and visualization, providing valuable insights into the dynamics of trend manipulation. The findings from this project are valuable for researchers, social media platforms, and policymakers. They contribute to a better understanding of coordinated campaigns on social media and offer tools and methodologies for detecting and combating artificial trend inflation. By addressing these issues, the project supports efforts to maintain the integrity of social media platforms and ensure that online trends reflect genuine user engagement.

## Future Work
As mentioned, due to pricing restrictions, it was not possible to gather data for some hashtags, which limited the scope of the analysis. In the future, exploring cost-effective solutions to collect a larger volume of data could enable more comprehensive and accurate analyses. Currently, batch data processing was utilized for the analysis. Moving forward, investigating the feasibility of real-time streaming data processing could allow for more timely analysis and insights, providing a more dynamic view of trend developments as they occur.

Additionally, incorporating advanced machine learning and deep learning techniques could enhance the analysis. Techniques such as sentiment analysis, network analysis, and anomaly detection could uncover more nuanced patterns and improve the accuracy of detecting coordinated campaigns. The use of graph databases could also be explored to analyze connections between users and detect potential coordinated campaigns or networks of bots. This approach would allow for a deeper understanding of user interactions and the identification of sophisticated manipulation tactics. Overall, this project has provided valuable insights into the problem of coordinated campaigns on Twitter and has demonstrated the potential of data engineering and data visualization techniques for social media analysis.
