Amazon RDS is a service that makes it easier for you to set up, operate, and scale a relational database. Instead of telling you about RDS, I am going to show you. 
# __
![[Pasted image 20230707163851.png]]
As you can see, I'm already in the Amazon RDS dashboard. We are going to create the relational database our employee directory application can use to store employee data. 
# __
![[Pasted image 20230707181600.png]]
First, we will click Create database, and then we are going to select the Easy create option, which gives us the ability to accept the standard best practices for backups and high availability. 
# __
![[Pasted image 20230707181653.png]]
You could select Standard create if you wanted more granular control to pick and choose the different features of your database setup. Next, you choose the database engine. You can see what is currently supported at the time of this filming for database engines on RDS. The common engines out there are MySQL, PostgreSQL, MariaDB, Microsoft SQL Server, and then there's this one, Amazon Aurora. 
# __
![[Pasted image 20230707181730.png]]
Amazon Aurora is an AWS-specific database that was built to take advantage of the scalability and durability of the AWS Cloud. Aurora is designed to be drop in incompatible with MySQL or PostgreSql. It can be up to five times faster than the standard MySQL databases and three times faster than standard PostgreSQL databases. So if you have some use cases that require large amounts of data to be stored with high availability, durability, and low latency for data retrieval time, consider using Amazon Aurora over a standard MySQL or PostgreSQL RDS instance. 
# __
![[Pasted image 20230707181810.png]]
In our case, we really only need a simple database without any high performance or large storage requirements. So I'm going to select a standard MySQL instance. 
# __
![[Pasted image 20230707181839.png]]
Next up, we will choose the database instance size and type. This database instance is similar to how we choose an EC2 instance size and type. Since this is just a demo, I'm going to select a free tier eligible instance. 
# __
![[Pasted image 20230707181914.png]]
Now we'll give this database a name and assign the database and admin user and password that would be used to connect to the database. 
# __
![[Pasted image 20230707181940.png]]
Then we will accept the rest of the Easy create defaults and we are done with this instance creation. You can see that the instance is in the process of booting up, and that will take a few minutes to complete. So in the meantime, let's talk about high availability and RDS. 
# __
![[Pasted image 20230707182050.png]]
When you create an RDS DB instance, it gets placed inside of a subnet inside of a VPC, very similar to an EC2 instance. As you learned already in a previous lesson, subnets are bound to one AZ, and as a best practice for production workloads, we recommend that you always replicate your solutions across at least two AZs for high availability. With RDS, one DB instance belongs to one subnet inside of one AZ, so that isn't meeting the criteria for best practices. Now, before you get worried about managing this all on your own, just know that you can easily configure RDS to launch a secondary DB instance in another subnet and another AZ using RDS Multi-AZ deployment. RDS will manage all of the data replication between the two instances so that they stay in sync. 
# __
![[Pasted image 20230707182227.png]]
The other cool thing about RDS Multi-AZ deployments is that RDS also manages the failover for the instances. One instance is the primary and the other is the secondary database. Your app connects to one endpoint. If the primary instance goes down, the secondary instance gets promoted. The endpoint doesn't change, so no code change is needed. All of the failover happens behind the scenes and is handled by RDS. All you do need to do is to make sure that your app can reconnect to the database if it experiences a momentary outage by updating any cache DNS lookups and reconnecting to the endpoint which now connects to the secondary instance. 
# __
![[Pasted image 20230707182321.png]]
we're back in the console and we can see that our instance is up and running. At this point, you can connect to the database instance and load your database schema onto it ready to go and much, much simpler than trying to install and manage this all on your own. 
# __
Using services like RDS make operating databases significantly more accessible and lowers the operational overhead that comes along with relational database management.
# __