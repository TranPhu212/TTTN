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

  * **Amazon Simple Storage Service (S3) – Static Website & CORS**
    * Amazon S3 has the capability to host static websites (HTML, media, etc.), making it suitable for Single Page Applications (web applications or websites that interact with users by dynamically rewriting the current page with new data from the web server using JavaScript and its frameworks such as AngularJS, ReactJS, instead of the browser’s default method of loading an entirely new page).
    * Amazon S3 supports CORS. CORS is a mechanism that allows various resources (fonts, JavaScript, etc.) of a website to be requested from a domain different from the website’s own domain. CORS stands for **Cross-Origin Resource Sharing**.
    * https://docs.aws.amazon.com/AmazonS3/latest/userguide/cors.html
    * Amazon S3 supports hosting static websites (HTML, media, etc.), which is suitable for Single Page Applications.
    * Amazon S3 allows configuration of CORS (Cross-Origin Resource Sharing) policies, enabling client web applications to interact with resources located on different domains.

  * **Amazon Simple Storage Service (S3) – Access Control**
      * Amazon S3 provides 2 mechanisms for controlling access to buckets
      * **S3 Access Control List (ACL)** is an access control mechanism that existed before IAM. However, if you are already using S3 ACLs and find them sufficient, there is no need to change. S3 ACLs are attached to both buckets and objects. They define which AWS accounts or groups are granted access and the type of access permitted
      * **S3 Bucket Policies** and **IAM Policies** define permissions by specifying the objects in the `Resource` section of the policy. The statement applies to those objects within the bucket. Consolidating object-specific permissions into a single policy (as opposed to multiple S3 ACLs) makes it easier to determine access rights
      * Every object in S3 is at the same level (no hierarchy) and is identified by an **object key**. Example: `/image/sample.jpg`, `sample.jpg`

  * **Amazon Simple Storage Service (S3) – Endpoint & Versioning**
      * **Amazon S3 Endpoints** allow access to S3 buckets through AWS’s private network. By default, access to S3 goes over the public internet
      * You can enable **Versioning**, which allows you to recover objects after accidental deletion or overwriting. It also helps protect against ransomware/encryption attacks
          * When you delete an object, Amazon S3 does not remove it permanently but instead adds a delete marker
          * When you overwrite an object, a new version of the object is created in the bucket
      * => In both cases, you can restore a previous version
      * Versioning allows you to recover objects after accidental deletion or overwriting and provides protection against ransomware/encryption attacks

  * **Amazon Simple Storage Service (S3) – Object Key & Performance**
      * Every object in S3 is at the same level (no hierarchy) and is identified by an **object key**. Example: `/image/sample.jpg`, `sample.jpg`
      * Internally, S3 divides data into **Partitions**. Partitions are automatically split when the number of requests increases or when there are too many object keys in one partition (which slows down object lookup)
      * S3 stores a **key map** (the key map is also divided into multiple partitions and hashed by the prefix of the object key)
      * To optimize S3 performance, you can use **random prefixes** (e.g., `/fscd/img/sample.jpg` instead of `/img/sample.jpg`). The goal is to distribute objects across as many partitions as possible, since S3 performance scales with the number of partitions

  * **Amazon Simple Storage Service (S3) – Glacier**
      * **Amazon S3 Glacier** is a low-cost storage option suitable for data that does not require immediate or frequent access — ideal for long-term archival
      * When data is stored in Amazon S3 Glacier, you cannot access it directly. You must initiate a **retrieve** request to bring the data back to an S3 bucket
      * There are three retrieval options with different access times and costs:
          * **Expedited** – typically completes in 1–5 minutes
          * **Standard** – typically completes in 3–5 hours
          * **Bulk** – typically completes in 5–12 hours
      * Amazon S3 Glacier is a low-cost storage class for long-term data that does not require direct or frequent retrieval.

  * **Snow Family - Storage Gateway - Backup**
      * **Snow Family – Snowball**
          * A service that helps migrate data from on-premise environments to AWS at petabyte (PB) scale. Each Snowball device can hold up to 80 Terabytes (TB)
          * The Snowball device is shipped back to the chosen AWS Region, where the data is loaded into your selected service (S3 or Glacier)
          * You need to install the Snowball Client on your local machine to perform verification, compression, encryption, and data transfer

      * **Snow Family – Snowball Edge**
          * A service that helps migrate data from on-premise environments to AWS at petabyte (PB) scale. Each Snowball Edge device can hold up to 100 Terabytes (TB)
          * The Snowball Edge device is shipped back to the chosen AWS Region
          * It includes built-in compute resources for processing data locally before importing into the device

      * **Snow Family – Snowmobile**
          * A service for migrating data from on-premise to AWS at exabyte scale. Each Snowmobile can hold up to 100 PB.
          * The Snowmobile is shipped back to the chosen AWS Region

      * **AWS Storage Gateway**
          * AWS Storage Gateway is a **hybrid storage** solution that combines AWS cloud storage with on-premise storage capacity.
          * It allows you to leverage the scale and cost-effectiveness of cloud storage for large volumes of data that require long-term retention
          * AWS Storage Gateway supports three main storage interfaces:
              * **File Gateway**: Allows you to store and retrieve objects in Amazon S3 using standard file protocols (NFS and SMB). Objects written through File Gateway can be accessed directly in S3
              * **Volume Gateway**: Provides block storage for your applications using the iSCSI protocol. Data is stored in Amazon S3. You can create EBS snapshots (automatically via AWS Backup) to restore as EBS volumes
              * **Tape Gateway**: Provides a virtual tape library (VTL) interface via iSCSI, including virtual tape drives and virtual tapes. Virtual tape data is stored in Amazon S3 or can be archived to Amazon Glacier
          * AWS Storage Gateway is a hybrid storage solution combining on-premise and cloud storage

  * **Disaster Recovery on AWS**
      * **RTO / RPO**
          * **Recovery Time Objective (RTO)**: The maximum acceptable time to restore a service to normal operation after a disaster
              * Example: If a disaster occurs at 2:00 PM and the RTO is 4 hours, the service must be restored by 6:00 PM at the latest
          * **Recovery Point Objective (RPO)**: The maximum acceptable amount of data loss (measured in time)
              * Example: If backups are performed once per day, in the worst case you could lose 24 hours of data → RPO = 24 hours

      * **Disaster Recovery Strategies on AWS**
          * Different applications have varying complexity and Service Level Agreements (SLAs) with different RTO/RPO requirements. You should choose the appropriate DR strategy accordingly
          * There are **4 main disaster recovery strategies** on AWS:
              * Backup and Restore
              * Pilot Light (Active–Standby)
              * Warm Standby (Low Capacity Active–Active)
              * Multi-Site Active–Active (Full Capacity)

      * **AWS Backup**
          * AWS Backup is a centralized service to manage backup tasks. You can configure backup schedules, retention policies, and monitor backup activities for various AWS resources, including:
              * Amazon EBS
              * Amazon EC2
              * Amazon RDS databases
              * DynamoDB
              * Amazon EFS
              * AWS Storage Gateway volumes

## Monday: 
