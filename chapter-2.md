# Chapter 2 - AWS - 10,000 Foot Overview

### The History So Far
* Not quizzed on the history ever
* From 2003 launch to today
* "Invention requires two things: 1. The ability to try lots of experiments, and 2. not having to live with the collateral damange of failed experiments" - Andy Jassy CEO AWS
* Time Line
  * 2003 - Chirs Pinkhan & Benjamin Black present a paper on what Amazon's own internal infrastructure should look like
  * Suggested selling it as a service and prepared a business case
  * SQS launched in 2004
  * AWS Officially launched in 2006
  * 2007 over 180,000 developers on the platform
  * 2010 all of amazon.com had moved to AWS
  * 2012 First re:Invent Conference
  * 2013 Certifications Launched
  * 2017 AI and VR Services

### 10,000 Foot Overview - Part 1
* 16 Regions & 44 Availability Zones (6 more Regions & 17 AZ's coming in 2018)
* A Region is a geographical area - each region consists of 2 (or more) Availability Zones
  * US East (Northern VA)
  * US East (Ohio)
  * US West...etc
* An Availability Zone is simply a data center - they are in a region, they are far enough apart so that if you get flooding in southern London, your northern London AZ will be ok
* Edge Locations are endpoints for AWS which are used for caching content. Typically this consists of CloudFront, Amazon's Content Delivery Network (CDN)
  * There are 96 Edge Locations
  * A CDN - if you have all your media files in London, and someone in Sydney has to pull all that down - adding latency - an Edge Location will cache that information after the first person pulls it down at a location close to them
* Exam Tips:
  *  Understand the difference between a Region, an Availability Zone, and an Edge Location

### 10,000 Foot Overview - Part 2
* Image 1: The AWS Platform - all of those systems sit on top of the Global Infrastructure
* Image 2: How AWS splits up all of the services
  * You are not expected to know what every single service is
  * Some questions are just checking to see if you generally know what the services are
* Compute
  * EC2 - Elastic Compute Cloud (sometimes call Cloud Compute) - these are essentially virtual machines inside the AWS platform. You can have physical dedicated machines under EC2, but typically you have VMs
  * EC2 Container Service - run and manage docker containers at scale
  * Elastic Beanstalk - for developers who don't understand AWS, just want to upload their code - provisions auto-scaling groups, load balancers, EC2 instances, etc
Features heavily in the developers associate course and the devops pro course
  * Lambda - the entire A Cloud Guru platform runs on Lambda. It is code that you upload to the cloud and control when it executes. You don't have to worry about any underlying phyiscal or virtual machines - nothing to manage, no OS or anything. All you worry about is your code
    * EX: you have a meme site where people upload an image and add text to it - you have a trigger for an image upload, and then you have the text that is added after
    * We will use Lambda, API Gateway, S3, and Polly in this course - this is important for the solutions architect
    * We'll make a service that reads our notes that we take in the course
  * Lightsail - Amazon's VPS - Virtual Private Service - for people who don't want to understand the underlying services. It provisions you with a server and you get a fixed IP you can log into, so you can manage that through a console - a watered down version of EC2
  * Batch - batch computing, not covered in any certification course currently
* Storage
  * S3 - Simple Storage Service - object based storage, you have a bucket and you upload your files into buckets in the cloud
  * EFS - Elastic File System - effectively a NAS (network attach storage) - store files on an EFS volume and mount that to multiple VMs. A simple, scalable file storage for use with Amazon EC2 instances - allowing you to connect it to multiple EC2 instances
  * Glacier - data archival - archive off your data, or you only check it every year or so - you can store it for cheap
  * Snowball - bring in large amounts of data into the AWS data center - rather than transfer it over wifi. Sometimes it's easier to write it physically to a disk, and then they will import it manually
    * In the storage of the solutions architect class that we're going to get a snowball
  * Storage Gateway - essentially virtual appliances that you install in your data center or in your head office - it will replicate information back to S3. There are 4 different types of Storage Gateways. Allows you to connect an on-premise software appliance (or VM) with cloud based storage. Seamlessly allows your on-prem applications to use storage in AWS Cloud  

* Databases
  * RDS - Relational Database Service - MySQL, PostgreSQL, Aurora, Oracle...
  * DynamoDB - Non Relational Database
  * Elasticache - is a way of caching commonly queried things from you DB Server - aka cache your top 10 products
  * Redshift - for data warehousing or business intelligent - where you're doing really complex queries with lots of joins, etc
Migration

* AWS Migration Hub - allows you to track your services as you migrate to AWS
  * Application Discovery Service - automated set of tools that detects what applications you have and what their dependencies are - ex: might have a sharepoint service with a dependency on a SQL server
  * DMS - Database Migration Service - Oracle hated this when it was released. It's an easy way to migrate your on-prem database to AWS - helps you keep track of your migrations
  * Server Migration Service - migrate your virtual and physical servers up to the cloud
  * Snowball - it's between storage and migration - used for migrating large amounts of data to cloud (TBs)

* Networking & Content Delivery
  * VPC - Virtual Private Cloud - a virtual data center - you'll go in and configure the firewalls, AZs, address ranges, network ACLs, route tables, etc
    * it is pretty complicated, but we have entire VPCs section
    * In order to pass any associate course, you have to be able to build a VPC by memory
  * CloudFront - Amazon's Content Delivery Network - if you think about your media assets or your video or image files, if you have users far away, CloudFront stores the assets closer to your users, at a closer Edge Location
  * Route53 - their DNS service - it's like an old school telephone book, you know a persons name and it gives you their telephone - DNS is similar where if you give it a website, it gives you an iPV4 and IPV6 address
    * we will go through a nd buy a domain name for the course
  * API Gateway - important in developer associate course - we'll use it when we create our serverless website using Polly, we'll use it for that - it is a way of creating your own API for your other services to talk to
  * Direct Connect - big topic for Associate Solutions Architect - how to get a dedicated line from your corporate HQ or data center directly to AWS

* Developer Tools
not a single service is in the any of the associate exams, but is good to know
  * CodeStar - way of getting a group of developers working together easily, set up your code and you have a continuous delivery toolchain
  * CodeCommit - a way to store your code - source control service, store your own private git repositories
  * CodeBuild - once you've got your code ready, it will compile your code for you, run tests for you, and produce software packages for you
  * CodeDeploy - this is a deployment service, automates application deployments to your EC2 instances or Lambda functions or on prem instances
  * CodePipeline - a continuous delivery service, use it to model and visualize and automate the steps required to release your software
  * X-Ray - debug and analyze your serverless applications. it has request tracing, you can find the route causes of issues and performance bottlenecks
  * Cloud9 - an IDE environment, where you can develop your code inside the AWS console 


### 10,000 Foot Overview - Part 3

* Management Tools
  * CloudWatch - monitoring service (including metrics such as CPU Utilization, Disk IO, etc.), the bread & butter of the SysOps Administration Associate exam
  * CloudFormation - if you are ever going to work as a solutions architect in real life, you'll use this all the time. In the solutions architect associate and pro exams - it's a way of scripting infrastructure. CloudFormation templates allow you to deploy a wordpress site or Joomla all with code, and it can be reused to deploy in different regions. People open source their templates, etc
  * CloudTrail - every time you click inside the AWS management consule and you do something, creating a new instance or user or S3 bucket, you are triggering an API call and CloudTrail logs that. It logs everything that is happening in your AWS environment. It only stores records for 1 week - you can turn them on for more accounts and regions in case you get hacked
  * Config - monitors the configuration of your entire AWS environment, it has point in time snapshots, so you can move the timer backwards or forwards - monitors the configuration of your entire AWS environment. On March 3rd I had one EC2 instances, March 4th I had 6 of them
  * OpsWorks - very similar to ElasticBeanstalk, it is a lot more robust - it uses Chef and Puppet, it's a way of automating your environments and the configuration - big in SysOps course
  * Service Catalog - typically you have to manage a catalog of IT services that are approved for use - anything from VM images to OS, software, databases, to complete multi-tier architecture. Used for governances and compliance reasons
  * Systems Manager - interface for managing your AWS resources - typically it's used for EC2, it's used for patch management, if you want to roll it out to thousands of servers, you can do that. You can also group resources together. Not in any of the exams yet
  * Trusted Advisor - favorite in the security associate, or the AWS solutions architect associate - understanding the difference between a Trusted Advisor and Inspector is good. A Trusted Advisor - gives you advice across multiple disciplines - security (ports are open), extra space (how to save money), sort of like an accountant/advisor on your account
  * Managed Services - if you don't want to have to worry about your EC2 instances or auto-scaling, this can help you out

* Media Services
  * Elastic Transcoder - when you upload a video, it kicks off an Elastic Transcoder session that resizes the video to work on different devices
  * MediaConvert - file based media transcoding service (multi-screen delivery)
  * MediaLive - live video processing service
  * MediaPackage - prepares and protects your videos for delivery over the internet
  * MediaStore - great place to store your media, great performance and low latency
  * MediaTailor - allows you to do targeted advertising in video streams, without sacrificing service
    * none of the Media services are in the exams

* Machine Learning
  * SageMaker - makes it really easy for developers to use Deep Learning when coding for their environments
  * Comprehend - does sentiment analysis around data - whether people are saying good or bad things
  * DeepLens - artificially aware camera. the camera itself can figure out what it's looking at, doing it on the camera itself (not sending it to the server). Physical piece of hardware that you can buy
  * Lex - this powers the Amazon Alexa service - a way of communicating with customers. Artificially Intelligent way of chatting to your customers
    * None of these come up in the exams (probably it's own specialty at some point)
  * Machine Learning - different to Deep Learning. DL is around neural networks, ML is just regular logistics. ML you throw a dataset into the cloud and give you some results - it will determine what the outcome is with new data
  * Polly - isn't used in an exam, but we use it to build. Takes text and turns it into speech - not like the old school robot talk. They sound really human.
  * Rekognition - does both video and image recognition. It will tell you what's in that file
  * Amazon Translate - translate languages for you. Competing with Google Translate

* Analytics
  * Athena - allows you run SQL queries against things in your S3 bucket. You have a bunch of excel sheets in an S3 bucket. You can design a SQL query that will go through all of your buckets and return a result
not in any exams
  * EMR - used for processing large amounts of data, used for big data solutions. Has a whole bunch of different services and chops up your data for analysis. Managed cluster platform for things like Apache Hadoop or Apache Spark (and Apache Hive and Pig)
is featured in the solutions architect associate exam
  * CloudSearch - used for searching, seems to be slow
  * ElasticSearch  Service - 
    * not exam topics
  * Kinesis - huge topic for solutions architect exams. A way of ingesting large amounts of data into AWS - social media feeds or tweets, or get a particular hashtag in there (millions of tweets in a day). Can be from multiple sources
  * Kinesis Video Streams - also under media services. Allows you ingest a lot of video at the same time
  * QuickSight - business intelligent tool - fraction of the cost of other tools. A fast, cloud-powered business analytics service that makes it easy to build visualizations, perform ad-hoc analysis, and quickly get business insights from your data. Not in any of the exams
  * Data Pipeline - is a way of moving your data between different services. Does come up in some exams
  * Glue - very new service, used for ETL - Extract Transform and Load - if you have to migrate large amounts of data, so you have to do an ETL to get it in the format you want


### 10,000 Foot Overview - Part 4

* Security & Identity & Compliance
  * IAM - Identity & Access Management
  * Cognito - a way of doing device authentication - you authenticate using a mobile app, or fb, or gmail, etc on your phone. Once you've authenticated, you can use the Cognito service to request temporary access to the AWS resources. Want your users to be able to store data in a DynamoDB - you give them write access to that DB and it would store things like their geographic data
  * GuardDuty - brand new AWS service, not in the exams, monitors for malicious activities on your AWS account
  * Inspector - is in exams. An agent you install on your VMs or EC2 instances and you can run a whole bunch of tests against it. Do my EC2 instances have any security vulns? You can run it weekly or monthly. It will generate a report with a severability list.
  * Macie - scan your S3 buckets and look for things that contain personally identifiable information - PII and alert you about it
  * Certificate Manager - SSL certificates for free and you register the domains through Route53
  * CloudHSM - Hardware Security Module - dedicated bits of hardware to store your keys (private and public) use them to access your EC2 instances, could use other encryption keys too. Used to be super expensive, now it's much less - $1.20/hour
  * Directory Service - basically a way of integrated your Active Directory service with Amazon services
  * WAF - Web Application Firewall - like a layer-7 firewall, stops things like cross site scripting or SQL injection - it looks at the application level and saying "what is this user doing? are they being malicious? do I want to prevent that?"
  * Shield - by default for a bunch of services included CloutFront, load balancers, Route53 - DDOS mitigation. Dedicated 24/7 team to prevent them, and you will not be charged extra if one occurs
  * Artifact - great for audit and compliance, on demand access to download AWS Compliant reports. Manage select agreements as well. Go in and download their SOC controls (service organization controls) get PCI reports

* Mobile Services
  * Mobile Hub - A management consule - if you have a mobile app, you can create a mobile hub that will set up your AWS services for you and generats a cloud configuration file. You use the mobile SDK to connect your mobile app to your backend (not in exams)
  * Pinpoint - A way of using targeted push notifications to drive mobile engagement - target for restaurant ads
  * AWS AppSync - automatically updates the data in mobile and web applications in real time - updates offline users as soon as they reconnect
  * Device Farm - way of testing your apps on real live devices (Android, iPhone, etc)
  * Mobile Analytics - analytic service for mobiles, and it does not come up in exams
    * pretty much none of them are relevant to the exams

* AR/VR
  * Sumerian - the first language that was written down - once we wrote things down we had a common set of tools to communicate ideas together. Used for AR/VR/application design. You don't have to understand how to code to build 3D rooms

* Application Integration
  * Step Function - managing your different lambda functions
  * AmazonMQ - message queues - like RabbitMQ
  * SNS - notification service, we'll set up a billing alarm - get a message to your email or phone
  * SQS - decoupling your infrastructure, SQS will sit there and hold the message until something pulls from the queue to act from it. If you EC2 instance and the message isn't processed successfully, it will go back in the queue and another EC2 instance will handle it
  * SWF - Simple WorkFlow - uses this in their warehouses - every time you order a package it creates a SWF job. Can have human beings as a component in it. Everything is tracked through the workflow

* Customer Engagement
  * Connect - Contact Center as a service - your own call center in the cloud. You can have dynamic, personal, and natural customer engagements. Not yet an exam topic
  * Simple Email Service - great way of sending large amounts of email, highly scaleable, great deliverability, highly customizable, pay as you go

* Business Productivity
  * Alexa for Business - dial into a meeting room, reorder ink for a printer
  * Chime - Google Hangouts or Zoom, used for video conferencing at work, can record them
  * Work Docs - dropbox for AWS, way of safely an securely storing your work documents
  * WorkMail - sort of like Office365, their competitor

* Desktop & App Streaming
  * Workspaces - a VDI solution, you're running the actual OS inside the cloud and then streaming that down to your device
  * AppStream 2.0 - you can stream the actual applications. The application is being streamed in the cloud, but you are using it on your device. Similar to Citrix

* Internet of Things
  * iOT - temperature, humidity, video/audio feeds
  * iOT Device Management - managing these at scale can be difficult, so this helps with that
  * FreeRTOS - operating system for your microcontollers, you go in an install it on your devices
  * Greengrass - software that lets you run local compute, messaging, data caching, sync, and ML interface capabilities for connected devices in a secure way
    * not in exams

* Game Development
  * GameLift - a way of developing games, VR games as well in AWS Cloud


### Don't Freak Out!
* Just watch the S3 section, DynamoDB section, Application Integration and Analytics sections after Solutions Architect and then you're ready for the Developer exam - probably 1.5 hours of extra study to get the second cert
* VPCs are important for all 3 associate exams (and they teach the same thing for all of them)

### AWS This Week
### Setting Up A Free Tier Account
### 10,000 Foot Quiz



Image 1: The AWS Platform - everything sits on top of the Global Infrastructure


Image 2: How AWS splits up their services
