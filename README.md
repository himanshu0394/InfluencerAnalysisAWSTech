# Future of marketing : Identifying real time social media influencers using AWS Kinesis, Spark and Amazon RDS
### Trends Marketplace Fall MSBA'19 - Team 2

## Project overview and objective
Due to social media outreach, identifying and leveraging social media influencers for business development has become crucial aspect of developing a successful marketing strategy for organisations. Below are some of the facts why influencer reach is of high importance:

![Influencer Importance](https://github.umn.edu/singh899/trends-project-team2/blob/master/Diagrams/Inf.PNG)

One of such popular social media platforms is twitter and various factors define how an influencer can be spotted:
1. Retweets: The number of retweets a person's tweet gets
2. Favourites: Number of accounts that have account under consideration as their favourite
3. Followers: Number of followers a person has
4. Depth: If a tweet is retweeted by another influencer then it is likeliy that the followers of that influencer will retweet the tweet. Hence it creates a second branch of retweets for the maub influencer which can create further layers of retweets. Depth signifies how farther is the reach of such non-primary retweets.

Our project aims to:
1. Understand what twitter users are talking about 
2. Important component of a marketing campaign
3. Identify influencer networks, leverage them for marketing
4. Optimize budget allocation in real-time using influencer efficiency, geographic penetration, etc.

## Architecture details

An iterative process flow to continually stream, process and generate insights has been implemented to gain information at the earliest:
![Methodology](https://github.umn.edu/singh899/trends-project-team2/blob/master/Diagrams/process.PNG)

The project pipeline consists of four main components. An amazon EMR instance is used to run the streaming script constantly while the data is sent to S3 using Amazon Kinesis Firehose. The data is batch processed and moved to Amazon RDS database using Spark and this dataset is further used to calculate influencer metric and build insightful visualizations in Tableau. Below is the detailed description of each of the component in the pipeline from streaming live data from twitter till storage and visualization.

![Project Architecture](https://github.umn.edu/singh899/trends-project-team2/blob/master/Diagrams/Arch2.PNG)

1. Streaming Data Source: The data collection began by implementing the streaming Twitter API using Python. We also implemented the Google NLP API to understand and analyze the sentiment of the data being scraped. The script constantly ran on the cloud on an Amazon EMR instance.
2. Streaming Pipeline: The streaming data was sent to Amazon S3, for convenient data storage using Amazon Kinesis Firehose. Amazon Kinesis Firehose provided an easy way to send streaming data into Amazon Web Services (AWS) to enable near real-time analytics with existing business tools.
3. Data Storage and Processing: The data stored on S3 was then batch processed using Apache Spark to ensure a scalable and reliable product for the clients of TwitterTalker. We used Spark to implement the majority of our analysis, e.g. calculate the influence score, etc. The data was processed every 15 minutes.
4. Database: The final output from our analysis in Spark was sent to Amazon RDS as a SQL table and updated every 15 minutes as mentioned earlier. The Python Flask App called the database to display the real time data to the client interface.

## Code walkthrough
Below are the details of key code components in sequence and their utility:
1. create_aws_pipeline: This code creates the pipeline used to stream data and store it in S3. The data is captured every 300 seconds or once the data reaches 5MB size limit, whichever reaches first.
2. data_producer: This is the main streaming component of the pipeline. The function on_data of class StreamListener specifies all the components from twitter data that will be streamed and stored on S3.
3. delete_kinesis_pipeline: This snippet drops the kinesis pipeline used to stream data from twitter to S3
4. download_unzip_mysql_driver: This shell script downloads and unzips the required MySQL driver.
5. run_analysis_updated: This code moves json data from S3 and stores it in a database on RDS by processing it and taking the relevant columns. It collects various columns such as number of followers, number of friends, total number of tweets and retweets and number of favourites. This data is ten appended to a table in RDS with specified paramteres.

