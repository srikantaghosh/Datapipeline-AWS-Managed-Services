# Datapipeline-AWS-Managed-Services

### This project implements a robust and efficient data pipeline in the AWS cloud environment to process and store customer invoice data. The system is designed to automatically manage data ingestion, transformation, storage, and querying processes using various AWS services.

### Architecture
![Architecture](https://github.com/srikantaghosh/Datapipeline-AWS-Managed-Services/blob/main/Screenshot%202023-07-09%20at%208.51.14%20PM.png)

1. **Amazon S3**: The pipeline starts with the customer uploading invoice data, in text format, to an Amazon S3 bucket. This S3 bucket serves as the initial data landing zone and is configured with a lifecycle policy to automatically delete any content that is older than 24 hours. This ensures that only the most recent data is kept in the bucket, preserving storage space and maintaining data freshness.

2. **Amazon SNS**: Whenever new data is uploaded to the S3 bucket, an event is triggered. This event then sends a message to an Amazon Simple Notification Service (SNS) topic. SNS is a fully managed messaging service that decouples microservices, distributed systems, and serverless applications.

3. **Amazon EC2**: A custom program running on an Amazon EC2 (Elastic Compute Cloud) instance is subscribed to the SNS topic. This EC2 instance automatically receives the message sent by the S3 event via the SNS topic. EC2 provides secure, resizable compute capacity in the cloud and allows for scalable computation.

4. **Amazon RDS and S3 API**: The custom program on the EC2 instance utilizes the S3 API to read the uploaded file from the S3 bucket. It then parses the content of the file, creates a CSV record, and saves these details in an Amazon RDS (Relational Database Service) database. RDS makes it easy to set up, operate, and scale a relational database in the cloud, providing cost-efficient and resizable capacity.

5. **S3 API**: After the transformation, the program uses the S3 API to write the CSV record back to a destination S3 bucket as a new object. This bucket serves as a repository for transformed data.

6. **Amazon Athena and Glue**: Finally, to provide an interface for querying and analyzing the data stored in S3, Amazon Athena and Glue are used. Amazon Athena is an interactive query service that makes it easy to analyze data directly in Amazon S3 using standard SQL. AWS Glue is used to catalog the data, making it available for queries in Athena.

This architecture automates the entire data pipeline process, from ingestion to query, making it efficient and scalable. It is useful for processing and storing large volumes of data, providing valuable insights from the transformed and structured invoice data, and it ensures that the system remains responsive even as data volume grows.

