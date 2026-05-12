---
title: "Week 4 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

* 

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
|  6  | - nội dung cần thay thế | 08/05/2026 | 08/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
|  2  | - nội dung cần thay thế | 11/05/2026 | 11/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
|  3  | - nội dung cần thay thế | 12/05/2026 | 12/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
|  4  | - nội dung cần thay thế | 13/05/2026 | 13/08/2026 | <https://cloudjourney.awsstudygroup.com/> |
|  5  | - nội dung cần thay thế | 14/05/2026 | 14/05/2026 | <https://cloudjourney.awsstudygroup.com/> |


### Week 4 Achievements:

## Friday: Storage Services on AWS
  * Amazon Simple Storage Service – S3
  * Amazon Storage Gateway
  * Snow Family
  * Disaster Recovery on AWS
  * AWS Backup

  * **Amazon Simple Storage Service (S3)**
    * Amazon S3 is object-level storage, meaning if you want to change a part of a file, you must modify it and then re-upload the entire modified file
    * S3 is suitable for write-once, read-many (WORM) data types
    * The smallest storage unit in the system is 1 object
    * When storing data this way, to change the content inside an object, you must replace the entire object by overwriting it with a new object
    * Different from block storage but commonly used
    * (WORM – Write Once Read Many)
    * Amazon S3 has no limit on total data storage volume
    * Each object cannot be larger than 5 TB
    * * In the case of Elastic Block Store, 3 replicas are only within 1 Availability Zone
    * By default, data in Amazon S3 is replicated across 3 AZs in 1 Region
    * Amazon S3 has the ability to trigger events, allowing you to automatically trigger actions when certain events occur, such as uploading or deleting an object from a specific storage area
    * These events can trigger serverless functions
    * When uploading data to S3, S3 itself has many background mechanisms to ensure data integrity and uniqueness
    * Amazon S3 is designed to achieve 99.999999999% durability and 99.99% availability
    * Amazon S3 supports multipart upload for uploading large objects to a bucket
    * We need to create S3 buckets to be able to store objects in Amazon S3
      * https://[bucket-name].s3.amazonaws.com
      * https://[bucket-name].s3.amazonaws.com/capture.mp4
    * Working with S3 via REST API (HTTP)

  * **Amazon Simple Storage Service (S3) – Access Point**
    * Amazon S3 Access Point is a feature that allows you to create unique connection points (unique hostnames) for applications, individual users, or groups
    * We can configure different permissions for each Access Point created
    * When multiple applications need to store data inside S3, we had to create separate S3 buckets for each application, making management and access policy management complex and difficult
    * Assigning access rights to each individual bucket leads to risks, operational errors such as missing or excessive permissions, and it is also difficult to track and maintain those policies
    * Now there is a new feature called Access Point, which allows creating multiple connection points with different hostnames for applications
    * However, all these connection points connect to a single bucket
    * Assigning access rights to each application or user becomes much easier than creating multiple S3 buckets
    * Create S3 Access Points for applications with different access permissions

  * **Amazon Simple Storage Service (S3) – Storage Class**
    * Amazon S3 divides storage into multiple storage classes to help us optimize costs
    * S3 Storage Classes:
      * S3 Standard: Frequently accessed data
      * S3 Standard IA: Infrequently accessed data
      * S3 Intelligent Tiering: Automatically moves objects between tiers based on the number of days the object has not been accessed
      * S3 One Zone IA: Data that can be recreated, long-term storage, infrequently accessed but requires fast access
      * Amazon Glacier / Deep Archive: Long-term archival with very infrequent access
    * We can set up automatic data lifecycle management (Object Lifecycle Management) stored in Amazon S3. By using lifecycle policies, we can transition data within an S3 bucket between storage classes according to customized time (days)
    * Having multiple tiers is to optimize costs
    * S3 has 2 main costs: total storage volume of objects uploaded to S3
    * The second is the number of requests to the S3 service, each upload or download (GET request) is also counted, and these two have different pricing
    * For Standard, the storage price is higher but the request price is lower, so frequently accessed data should be stored here
    * For Standard Infrequent Access, data that is not accessed frequently has a slightly lower storage price but higher request price
    * If you put frequently accessed data into Standard Infrequent Access, you will actually pay a higher fee than S3 Standard
    * Object Lifecycle Management will move the object after the number of days we specify, calculated from the day the object was created

  * **




## Monday: 
