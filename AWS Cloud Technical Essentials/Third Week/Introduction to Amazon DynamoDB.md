Let's talk some more about Amazon DynamoDB. At the most basic level, DynamoDB is a database. It's a serverless database, meaning that you don't need to manage the underlying instances or infrastructure powering it. 
# __
![[Pasted image 20230707183244.png]]
With DynamoDB, you don't create a database with tables that relate to each other like a relational database. Instead, you create standalone tables. A DynamoDB table is just a place where you can store and query your data. Data is organized into items and items have attributes. 
# __
If you have one item in your table or 2 million items in your table, DynamoDB manages the underlying storage for you and you don't need to worry about scaling the system up or down for storage. 
# __
![[Pasted image 20230707183350.png]]
DynamoDB stores data redundantly across AZs and mirrors the data across multiple drives for you under the hood, this lessens the burden of operating a highly available database. 
# __
DynamoDB, beyond being massively scalable, is also highly performant. DynamoDB has a millisecond response time and when you have applications with potentially millions of users, having scalability and reliable lightning fast response times is important. 
# __
Now, DynamoDB isn't a normal database in the sense that DynamoDB doesn't require a rigid schema or manage complex relationships or constraints. Relational databases like the MySQL database we created in an earlier lesson require that you have a well-defined schema in place that might consist of one or many tables that may or may not relate to each other. Relational databases work great for a lot of use cases and have been the standard type of database historically, however, these types of rigid SQL databases can have performance and scaling issues when under stress. The rigid schema also makes it so that you cannot have variation in the types of data that you store in a single table, so it might not be the best fit for a data set that is a little bit less rigid and is being accessed at a high rate. This is where no SQL databases like DynamoDB are handy. 
# __
![[Pasted image 20230707183556.png]]
No SQL databases have flexible schemas. With DynamoDB, you can add or remove attributes from items in the table at any time. Not every item in the table has to have the same attributes. This is great for data sets that do have some variation from item to item. 
# __
The types of queries you can run on no SQL databases tend to be simpler and focus on a collection of items from one table, not queries that span multiple tables. 
# __
![[Pasted image 20230707183631.png]]
This along with other factors, including the way the underlying system is designed, allow DynamoDB to be very quick in response time and highly scalable. 
# __
So things to remember, DynamoDB is no SQL. It is purpose-built, meaning it has specific use cases and isn't the best fit for every workload out there. 
# __
![[Pasted image 20230707183700.png]]
Taking a look at our architecture, we modified it to use DynamoDB. We are going to need to create an employee table for the app to write and read from. 
# __
We will create this DynamoDB table using the console. And you know what? Let's get Seph out here to help us out. - We changed our minds about using RDS and decided to change it over to DynamoDB. It's only one table and it's essentially a lookup table for our employees. How hard do you think this change is gonna be to make? - Well, our app is actually designed to use either RDS or DynamoDB as the backend database so this won't take long at all. 
# __
![[Pasted image 20230707183748.png]]
Here, I'll show you how. I'm in the console and will navigate to the DynamoDB service. 
# __
![[Pasted image 20230707183804.png]]
From here, all you need to do is create a new table. 
# __
![[Pasted image 20230707183830.png]]
Tables in DynamoDB require you to designate certain attributes as keys that will make an item unique. We will select employee ID as the unique identifier for the items in this table. 
# __
![[Pasted image 20230707183844.png]]
Then we will just accept the defaults and create the table. 
# __
![[Pasted image 20230707183919.png]]
Our app was coded to look for a table specifically called employees so this actually should all work now that the table is created. 
# __
![[Pasted image 20230707183946.png]]
To test it out let's head over to the website hosted on EC2
![[Pasted image 20230707184017.png]]
and try to add a new employee. 
# __
![[Pasted image 20230707184032.png]]
See, that was nice and easy. 
# __
![[Pasted image 20230707184049.png]]Now let's go back into DynamoDB 
![[Pasted image 20230707184107.png]]
and refresh the page 
![[Pasted image 20230707184119.png]]
and scan all the items in the table and boom, 
![[Pasted image 20230707184140.png]]
there it is. It's really that simple for a lookup table like this one.