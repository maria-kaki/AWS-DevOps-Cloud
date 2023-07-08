Before we move on to learning about Amazon DynamoDB, I want to touch on an idea that's important when you're making architecture decisions for your AWS solutions, choosing the right database to fit your business requirements rather than forcing your data to fit a certain database choice. There is no one size fits all database for all purposes. You should pick a database that fits your specific use case, and with AWS, you have multiple choices for databases. We covered Amazon RDS and relational databases, and that was the default option for businesses for a long time, but relational databases aren't the best choice for all business needs. 
# __
AWS creates services to support purpose-built databases, meaning that there are many database services that AWS offers, and they each were built with a certain use case in mind, and therefore are optimized for those use cases. 
# __
Let's think about the Employee Directory app. We had originally decided that we would use RDS for the database, but now after thinking about it some more, RDS might not be the best fit for our needs. All we are really doing is storing one record in a table for each employee. There are no complex relationships that need to be managed, and it's essentially just a lookup table. 
# __
Relational databases offer all sorts of features that are great for complex schemas and relationships, but those features add overhead that is unnecessarily complex for simple things like a lookup table. On top of that, the RDS option we chose charges per hour of instance run time, so we will get charged for the running instances regardless of whether we're using it or not. Our employee directory application will have much higher usage during the week and no usage on the weekends. Is there an AWS database offering that better fits our needs? 
# __
![[Pasted image 20230707182741.png]]
Introducing Amazon DynamoDB. Amazon DynamoDB is a NoSQL database that is great for storing key value pairs or document data. This service works great at a massive scale and provides millisecond latency. 
# __
It also charges based on the usage of the table and the amount of data that you are reading from the table, not by the hour or by the second. This is a better option for our simple employee lookup table. 
# __
Now, besides the employee directory app, there are other use cases that require databases of varying types. What if you are writing an application that needs a full content management system? Neither RDS nor DynamoDB would be the best solution. Luckily, AWS has quite a number of other database offerings. 
# __
![[Pasted image 20230707182831.png]]
For this use case, you might look into Amazon DocumentDB. It's great for content management, catalogs, or user profiles. 
# __
Let's think of another use case. What if you had a social network that you wanted to track? Keeping track of those kind of social webs, figuring out who is connected to who can be difficult to manage in a traditional relational database. 
# __
![[Pasted image 20230707182920.png]]
So you could use Amazon Neptune, a graph database engineered for social networking and ecommendation engines, but it's also good for use cases like fraud detection, or perhaps you have a supply chain that you have to track with assurances that nothing is lost, or you have a banking system or financial records that require 100% immutability. 
# __
![[Pasted image 20230707182957.png]]
What you really need is an immutable ledger, so perhaps Amazon QLDB, or Quantum Ledger Database, is a better fit for this use case. It's an immutable system of record where any entry can never be removed, and therefore is great for industries that need to be audited for regulatory and compliance reasons. 
# __
It can take a lot of experience and expertise to operate databases at scale, and that's why it's so beneficial to utilize one of the AWS database offerings. You don't need to be an expert on running all of these different types of databases. Instead, you can just use the database service that is best for your use case and focus on your application and providing value to your end users. You don't need to build up a ton of in-house expertise to operate a highly scalable immutable ledger database. You can just use AWS QLDB instead. The key thing to understand is AWS wants to make sure that you are using the best tool for the job. Coming up next, we will explore Amazon Dynamo DynamoDB and get a look at more of the details.
# __