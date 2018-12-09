# trends-project-team2
# Future of marketing : Identifying real time social media influencers using AWS Kinesis, Spark and Amazon RDS

## Project overview and objective
__Understanding__ what twitter users are talking about is an important component of a marketing campaign. The sentiment tracking and word cloud functions allow marketing manager to know how audiences feel and what are the frequently mentioned words. If the average sentiment score drops significantly, it means that a potential public relationship crisis might be happening.
1. Retweets
2. Favourites
3. Followers
4. Depth
![Project Objective](https://github.umn.edu/singh899/trends-project-team2/blob/master/Diagrams/Obj.PNG)

## Architecture details

The project pipeline consists of four main components. An amazon EMR instance is used to run the streaming script constantly while the data is sent to S3 using Amazon Kinesis Firehose. The data is batch processed and moved to Amazon RDS database using Spark and this dataset is further used to calculate influencer metric and build insightful visualizations in Tableau. Below is the detailed description of each of the component in the pipeline from streaming live data from twitter till storage and visualization.

![Project Architecture](https://github.umn.edu/singh899/trends-project-team2/blob/master/Diagrams/Arch2.PNG)

1. Streaming Data Source: The data collection began by implementing the streaming Twitter API using Python. We also implemented the Google NLP API to understand and analyze the sentiment of the data being scraped. The script constantly ran on the cloud on an Amazon EMR instance.
2. Streaming Pipeline: The streaming data was sent to Amazon S3, for convenient data storage using Amazon Kinesis Firehose. Amazon Kinesis Firehose provided an easy way to send streaming data into Amazon Web Services (AWS) to enable near real-time analytics with existing business tools.
3. Data Storage and Processing: The data stored on S3 was then batch processed using Apache Spark to ensure a scalable and reliable product for the clients of TwitterTalker. We used Spark to implement the majority of our analysis, e.g. calculate the influence score, etc. The data was processed every 15 minutes.
4. Database: The final output from our analysis in Spark was sent to Amazon RDS as a SQL table and updated every 15 minutes as mentioned earlier. The Python Flask App called the database to display the real time data to the client interface.

## Code walkthrough


## Conclusion
