# Team 14 - Manage and Share Big Data Insights through AWS RedShift, QuickSight, and Lambda
**MSBA 6330 Trends Marketplace Spring 2022**  
Eshan Bhushan, Bradshaw Irish, Likhith Karanuthala, Ka Lok Carol Ng, and Sheetal Pasam

## Full Presentation Video Found Here: 
[youtu.be/O6L0bPjqYwA](https://youtu.be/O6L0bPjqYwA)

## Project Summary
Our project seeks to showcase the ease of ingesting big data into AWS S3, creating materialized views and exploring data quickly using AWS RedShift, visualizing meaningful dashboards to drive business insights through AWS QuickSight, and automatically sharing reports with teammates via AWS Lambda. Combined, our project shows a full data analytics pipeline capable of managing very large amounts of data with exceptional performance at a fraction of the cost of alternative tools. Our project would be suitable for any oraganization that needs to analyze and visualize large amounts of structured and unstructured data quickly.
  
This project uses the Iowa Liquor Sales 2020 dataset available on Kaggle through [this link](https://kaggle.com/datasets/sibmike/iowaliquorsales2020). This dataset includes transactions for multiple locations and dates throughout Iowa and includes both structured data, such as price per unit sold, and unstructured data, such as free text product descriptions. The goal of the project is not to explore this particular dataset for actionable insights, but to show the process of ingesting, manipulating, visualizing, and sharing data for such a large and complex file. Our pipeline could be adapted easily to other forms of transactional data, or the principles could be aplied to another large data source or project.  

You can view our summary handout [here](Team14_TrendsHandout.pdf) or our full presentation slides [here](<Team 14 - Full Presentation.pdf>). A 10 minute video of our presentation including demonstrations of S3, RedShift, QuickSight, and Lambda is hosted on youtube and linked above. You can also view the individual video demos on youtube through the following links:
- [S3 and RedShift](https://youtu.be/DXHbHHed9vA)
- [QuickSight](https://youtu.be/yPrk14ex-ew)
- [Lambda](https://youtu.be/9kuMvx_Qxd4)

## QuickSight Setup

1. "Dataset" -> "New dataset" in Quicksight allows you a variety of data sources, you can upload from your computer, connect with S3, RDS, Redshift, and even external servers such as Twitter, Github mySQL etc. 
<img width="791" alt="image" src="https://user-images.githubusercontent.com/50436546/167036372-019ffbb9-7008-433f-ba85-24bdbbf1645b.png">


2. As we uploaded our dataset in S3 Bucket and Redshift, we will connect the data source from redshift cluster. , we imported our csv from Redshift - "iowa_2020.csv", from the dataset click "create analsis"
<img width="589" alt="Screen Shot 2022-05-05 at 5 35 31 PM" src="https://user-images.githubusercontent.com/50436546/167036064-efde4368-912e-4a53-8483-3b513494ec30.png">
<img width="791" alt="image" src="https://user-images.githubusercontent.com/50436546/167036385-9335aff2-3fd5-48d7-ae32-290825b3b403.png">

3. In QuickSight, we can create dashboard with a handful of embedded visualization tools, like figures, charts, bars. We can also add calculated fields for our dataset, for example formulating the profit by subtracting revenue over cost and use the new profit function to add another graph. Another helpful feature in Quicksight is the forecast tool, it’s using machine learning based on the dataset which allows users to adjust forecast length and interval. the orange area is the sales and profit forecast of our dataset. Adding some insights such as top 3 and bottom 3 in the dasboard.

![ezgif com-gif-maker (2)](https://user-images.githubusercontent.com/50436546/167038317-4bb31e51-f8f6-4e47-82c8-ca4fdffa8b7a.gif)
<img width="791" alt="image" src="https://user-images.githubusercontent.com/50436546/167036468-a74ab866-fc87-4af6-bf1f-b09b80b72d20.png">

Here is a simple dashboard build by Quicksight, interactive features, month, shows data accordingly

![ezgif com-gif-maker (1)](https://user-images.githubusercontent.com/50436546/167037001-8a695d04-699c-40de-9fff-1a26b1d93f9d.gif)
  
## Lambda and SES Setup

1. After we built dashboard, we can use Lambda and Simple Email Service to distribute to clients. In AWS Lambda, we can create function from scratch, using java, python, ruby etc. There are also over 700 open sources available that you can search for in the repository.

<img width="791" alt="image" src="https://user-images.githubusercontent.com/50436546/167038010-aa6106d6-fbd0-4618-a2fb-9f1a97d2b7bf.png">

2. Here we built a function with python to automatically send out a dashboard pdf file to distribution list. In the function, we can add trigger configuration from a lot of sources like Alexa, kinesis, dynamoDB, and of course we will choose our S3 bucket where we are storing the dashboard pdf file. 
<img width="791" alt="image" src="https://user-images.githubusercontent.com/50436546/167038123-d22eb152-9bb2-4987-bcd1-739163c1aa48.png">
<img width="791" alt="image" src="https://user-images.githubusercontent.com/50436546/167038211-19122d6a-e5f1-4eae-b76c-5ef79e46704a.png">

3. We wrote a lambda function that detects for any trigger config in S3, and passes an event to SES to send an email to a distribution list. Now whenever we save the "Iowa Liquor Sales.pdf" to S3  folder "trends 6330", an email is automatically sent out. For function code please go <a href="https://github.com/eshanbhushan5/Team15_TrendsMarketPlace_UMN/blob/main/lambda_quicksight-share"><u><b>here</u></b></a>.
<img width="791" alt="image" src="https://user-images.githubusercontent.com/50436546/167038427-e5994e16-12a3-4594-a72e-6d6908a35e4f.png">
  
4. In S3 bucket you can upload an "email.csv" with the subject and body you designed. And we save the Iowa Liquor Sales reports in the folder in S3.
<img width="791" alt="image" src="https://user-images.githubusercontent.com/50436546/167038493-0f4e3a06-c74e-472e-ba38-c2b0aaa73ded.png">
<img width="791" alt="image" src="https://user-images.githubusercontent.com/50436546/167038534-6393cecd-506e-454b-8f23-9bfd2c87b809.png">
<img width="791" alt="image" src="https://user-images.githubusercontent.com/50436546/167038610-3ded9ac0-ae3d-46bf-890a-9da974fc9221.png">

5. An email is automatically sent out when a file is uploaded to the S3 bucket folder we assigned. Of course you can also add lambda functions to automate the dashboard saving process as well. 
<img width="791" alt="image" src="https://user-images.githubusercontent.com/50436546/167038641-661078b5-d80d-474d-bdb3-bb4c9a4afba0.png">

## SES - Simple Email Service

1. One more thing you might want to know, only the identities added in SES can distribute the emails from our AWS accounts, so you need to add all the emails and verify them.

<img width="791" alt="image" src="https://user-images.githubusercontent.com/50436546/167038675-aa1e5b30-ddfe-4428-adb9-a76653cdbddf.png">


_This project repository is created in partial fulfillment of the requirements for the Big Data Analytics course offered by the Master of Science in Business Analytics program at the Carlson School of Management, University of Minnesota._
