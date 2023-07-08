At this point, you've covered a few different AWS compute services. The services covered so far can handle a wide variety of use cases. So how do you know when to use each one? To figure that out, I think it's time to play a game. 
# __
Welcome to the "Which AWS Compute Service Should I Choose For My Use Case?" game show. We are your hosts and you are the contestant. 
# __
We will present three different use cases that require compute on AWS, and it's up to you to choose the right service for the use case. You'll have five seconds to answer each question. Ready? - I'm ready and I hope you are, too. Let's do it.
# __
#### First question is up. 
![[Pasted image 20230703132803.png]]
Consider a scenario where you are a developer who is tasked with creating a new feature for a web application being hosted on EC2. The web application is an online store. And right now, all the items being sold in the store are loaded into a database manually behind the scenes. 
# __
By manually, I mean there is a person who adds a new row to a database for each new item to be sold in the store. 
![[Pasted image 20230703133251.png]]
This process takes a long time, isn't very scalable, and is prone to error. You are tasked with automating the process of getting the new item information loaded into the inventory database. The goal is to have a person upload an inventory spreadsheet into Amazon S3, the object storage service, then have a process automatically load the data into the inventory database. 
![[Pasted image 20230703133335.png]]
### What compute would you use to host the processing logic to load the items from the file into the database?
You could have decided to use Amazon EC2 here. You could spin up a new instance specifically for this process and write some code that polls the location of the spreadsheet for a new upload every so often. Updating the database when it finds a new file, that would work, but before I make my final answer here, I have a question. How often does new inventory get added to the database? - New inventory gets updated once a quarter. - Good to know. So it's not very often, which means this process would only run once a quarter and that does change my answer. Here's why. Amazon EC2 charges per second or per hour. So if I have an instance running all the time to serve requests that happens once per quarter, that seems like a lost opportunity to optimize for cost. I would be spending money on a resource I rarely use. It certainly would work, but it may not be the best fit for this use case. I could automate the process of starting and stopping the instance when needed. But instead, what about using AWS Lambda? 
# __
AWS Lambda is the correct answer for this one. There are a few reasons. First of all, to address your concern on cost, AWS Lambda only charges you for the compute you consume when the code is actually running. And code is only run in response to triggers or a direct invitation. So here's my suggestion. You know that the goal is to have someone upload an inventory document to S3, which should kick off the process of updating the database. You also learned that AWS Lambda has triggers that run your Lambda functions code. AWS Lambda integrates with many AWS services to act as triggers, and Amazon S3 is one of them. 
# __
![[Pasted image 20230703133953.png]]
So my suggestion would be to create an AWS Lambda function; configure a PutEvent as the trigger from Amazon S3; then when the inventory is uploaded, Amazon S3 will trigger the Lambda function to run and the code in the function will parse the inventory document and add each item to the database. 
# __
### Time for the next question. 
![[Pasted image 20230703143012.png]]
Let's say you have an application currently hosted in your on-premises data center, which needs to be migrated to AWS. It's currently running on Linux servers in the data center, and you want to minimize the amount of refactoring needed to migrate to AWS. It's important that this workload is elastic and can support varying demand. What compute option would you choose?
# __
Now, I'll go over the answer. Considering the fact that minimizing refactoring is an important aspect of this workload, I would architect a solution using Amazon EC2 as the compute service. EC2 instances can be launched from Linux-based AMIs, and the application could be hosted on the EC2 instance the same way it would be hosted on a Linux server on premises. Amazon EC2 also has the ability to scale in or out based on demand, so I think EC2 is the best service for this one. 
# __
That's correct. So if you answered EC2 at home. Before we move on to the final question, let's dive into this answer a little more. Morgan, can you explain the thought process behind eliminating the other compute services we covered in the answers to this question? - Sure thing. So AWS Lambda could work, but you can't just upload the same code you would run on Amazon EC2 into a Lambda function. There would have to be a decent amount of refactoring in order to take advantage of that service. Same idea with any of the AWS container services, like ECS or EKS. Again, you'd have some amount of rework required to migrate to containers. Therefore, Amazon EC2 is the best option for this migration. 
# __
![[Pasted image 20230703143551.png]]
Now, time for one final use case, and this one is for all the marbles. Imagine a scenario where you are planning to write a brand-new application using a microservices or service-oriented design. And you want to architect the application where it can scale up or down quickly, and you want to lower the risk of deploying new changes to production. Which AWS compute service would you use?
# __
The answer for this use case is... One of the AWS container services like Amazon ECS or Amazon EKS. - Correct. The answer is either ECS or EKS for this one because using containers makes it easier to support microservice or service-oriented designs. Containers boot up quickly, so scaling is quicker than EC2 instances, and the use of containers helps with code portability. 
# __
![[Pasted image 20230703144046.png]]
Meaning, if I write the code on my laptop and run it in a container, test it in QA in a container, I can then expect the same container to behave the same way once deployed to production, thus reducing the risk of deployments causing errors because of environmental issues. 
# __
All right, there you have it. Different use cases for a few of the AWS compute services. Make sure you read up on AWS's other compute offerings and make informed decisions when architecting your solutions. You'll find there are a lot of options. - Remembering that these services exist to best suit different use cases helps. Don't try to use the same compute service for all of your use cases. Instead, pick the right one for the job and consider reevaluating choices for existing workloads as AWS continues to release and improve offerings.