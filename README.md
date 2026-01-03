# PROJECT : AWS S3 SECURITY MONITORING – DATA EXFILTRATION & PUBLIC ACCESS DETECTION




## CLOUD-NATIVE SECURITY MONITORING SOLUTION FOR AWS S3



## Introduction
In this project, I implemented a cloud-native security monitoring solution for AWS S3 using CloudTrail, CloudWatch Logs, Metric Filters, and Alarms.
The goal was to detect:
-	Public exposure of a sensitive bucket (control-plane / management events)
-	Object-level activity such as downloads, uploads, deletions (data-plane / data events)
This setup mimics real-world SOC detection workflows, allowing near-real-time alerts for suspicious S3 activity.




## Project Objectives
-	Enable CloudTrail logging for S3 management and data events
-	Configure CloudWatch metric filters to detect risky bucket changes and data access
-	Create CloudWatch alarms to notify of potential security issues
-	Test and validate that alerts are triggered by relevant actions
-	Gain hands-on experience with AWS control-plane and data-plane monitoring




# <p align = center>STEPS INVOLVED





## STEP 1 – CREATING THE S3 BUCKET
-	I created an s3 bucket named “sensitivedata101”.
-	This was the bucket intended to hold the sensitive objects that must be protected
-	I uploaded some file into the bucket




![S3 IMGS](S3M-IMGS/s3.jpg)




## STEP 2 – CREATING A TRAIL IN CLOUDTRAIL
-	I created a trail on CloudTrail for management event and data events
-	Since the goal is to log data events for a particular s3 bucket, I made sure to select CUSTOM in the log selector option.
-	In the Advanced event selector, I choose the resource arn, starts with, and then inputted my bucket ARN. 
-	I also Enabled CloudWatch logging
-	An IAM role was automatically created for me to enable proper logging to CloudWatch



## STEP 3 – LOG GROUP AND LOG VALIDATION
-	I verified that CloudTrail logs were being sent to CloudWatch Logs for near-real-time monitoring.
-	The log groups was created automatically and logs available
-	I created another s3 bucket and uploaded some file and checked the logs once again to make sure that the data events weren’t being logged, this ensures that only the data events of the intended s3 bucket is the one being logged.



![S3 IMGS](S3M-IMGS/log-group.jpg)



![S3 IMGS](S3M-IMGS/logs.jpg)




## STEP 4 – CREATING METRIC FILTERS
I created 3 different metric filters to detect different activities which includes:


**Detecting Public Access Changes (Management Events)**


- I wanted to detect any changes that made my bucket more public.
-	I created a metric filter for PutBucketPublicAccessBlock targeting my bucket.


**Detecting Data Exfiltration and Object Activity (Data Events)**


I wanted to monitor all object-level actions in my bucket. I created a comprehensive metric filter for:</p>
- GetObject (downloads / exfiltration)
- PutObject (uploads / potential malware or data injection)
- DeleteObject (deletions / tampering)
- CopyObject (object duplication)
- PutObjectAcl (permission changes)


**Detecting Anonymous Access**


- I also wanted to catch any unauthenticated access.
- I created a metric filter for userIdentity.type = "Anonymous"



![S3 IMGS](S3M-IMGS/filter1.jpg)



![S3 IMGS](S3M-IMGS/filter2.jpg)




## STEP 5 – CREATING AN SNS TOPIC
-	I created a single SNS topic for all alarms and subscribed my email address.
-	This allowed centralized alerting for all metric filters, making it easy to track all security events in one place.




![S3 IMGS](S3M-IMGS/sns.jpg)
