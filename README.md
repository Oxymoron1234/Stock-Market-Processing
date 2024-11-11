# Stock Market Kafka Real Time Data Engineering Project

## Introduction 
In this project, you will execute an End-To-End Data Engineering Project on Real-Time Stock Market Data using Kafka.

We are going to use different technologies such as Python, Amazon Web Services (AWS), Apache Kafka, Glue, Athena, and SQL.

## Architecture 
<img src="Architecture.jpg">

## Technology Used
- Programming Language - Python
- Amazon Web Service (AWS)
1. S3 (Simple Storage Service)
2. Athena
3. Glue Crawler
4. Glue Catalog
5. EC2
- Apache Kafka


To set up a stock market data pipeline using Apache Kafka on an EC2 instance, where the producer generates stock market data, the consumer stores the data in an S3 bucket (e.g., "stock-market-bucket"), and AWS Glue crawls the data for querying via AWS Athena, follow these detailed steps.

### **Step 1: Set Up AWS Infrastructure**

#### 1. **Create EC2 Instance**
   - Launch an EC2 instance (Amazon Linux 2 or Ubuntu is recommended).
   - Ensure the EC2 instance has proper IAM roles attached to access S3 and AWS Glue services.

#### 2. **Create an S3 Bucket**
   - Go to the S3 console and create a bucket named `stock-market-bucket` (or any name you prefer).
   - Set up the appropriate permissions (bucket policy) for EC2 and Glue to read/write the data.

#### 3. **Set Up IAM Role**
   - Create an IAM role that allows access to:
     - S3 (for storing and retrieving data).
     - Glue (for crawling and querying data via Athena).
   - Attach this IAM role to your EC2 instance.

#### 4. **Create Athena Database and Tables**
   - In Athena, create a database for your stock market data, for example, `stock_market_db`.
   - Define the table structure based on the data format (e.g., CSV, Parquet) that the consumer will write to S3.

### **Step 2: Set Up Apache Kafka on EC2**

    - Use command_kafka.txt to setup kafka on EC2

### **Step 3: Set Up AWS Glue for Crawling Data**

#### 1. **Create AWS Glue Crawler**
   - In the AWS Glue Console, create a new Glue Crawler.
     - Data Store: S3.
     - S3 path: `s3://stock-market-bucket/`.
     - IAM Role: Use an IAM role that has permissions to read from S3 and access Glue.
     - Set the crawler to crawl your stock market data folder, and choose a schedule (e.g., run every hour).

#### 2. **Run the Crawler**
   - After setting up, run the crawler. It will infer the schema of your stock market data (e.g., JSON or CSV) and create a table in AWS Glue.

### **Step 4: Query Stock Data Using Athena**

#### 1. **Set Up Athena**
   - Go to the AWS Athena console.
   - Set the S3 output location for query results (e.g., `s3://stock-market-bucket/athena-results/`).

#### 2. **Run Queries**
   - Once the Glue crawler has completed and created the table, you can query your stock market data using SQL:
     ```sql
     SELECT * FROM stock_market_db.stock_market_table LIMIT 10;
     ```

### **Step 5: Monitor and Optimize**

#### 1. **Monitor Kafka**
   - Use Kafka’s built-in monitoring tools or integrate with AWS CloudWatch for monitoring the producer and consumer.

#### 2. **Optimize Data Flow**
   - Consider using Avro or Parquet formats for more efficient storage in S3 and querying in Athena.
   - You can partition your data in S3 by timestamp to improve query performance in Athena.

#### 3. **Scale as Needed**
   - If you expect high traffic or large amounts of data, consider setting up multiple Kafka brokers, partitions, and consumers. You can also adjust EC2 instance types for better performance.

---

By following these steps, you'll have a fully functioning pipeline where stock market data is produced, consumed, and stored in S3, ready to be queried via Athena with the help of AWS Glue crawlers.




