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


