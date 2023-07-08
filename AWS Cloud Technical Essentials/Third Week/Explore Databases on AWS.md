The employee directory application that we've been building out lets you keep track of employee data, like their name, location, job title, and badges. The app supports adding new employees, viewing existing employees, as well as editing and deleting employees. All of this data will be stored in a database, which we haven't created yet. 
# __
![[Pasted image 20230707163216.png]]
According to the architecture diagram, we have chosen Amazon Relational Database, or Amazon RDS, to store this data. 
# __
So let's talk about databases for a moment. Relational databases are widely used across all industries and it's likely your company has many databases supporting a variety of applications and solutions. Relational database management systems, or RDBMS, let you create, manage, and use a relational database. You can install and operate database applications on Amazon EC2 instances, and this is a good option for migrating existing databases to AWS. By running databases on EC2, you are already simplifying things from an operational perspective when it comes to on-premises, and it's a common use case for EC2. 
# __
![[Pasted image 20230707163354.png]]
When migrating a database from on-premises to EC2, you are no longer responsible for the physical infrastructure or OS installation, but you are still responsible for the installation of the database engine, setting up across multiple AZs with data replication in place, as well as taking on any database server management tasks like installing security patches and updating database software when necessary. So EC2 makes it easier, but there is a way to lift even more of the operational burden of running relational databases on AWS. 
# __
What if, instead of managing a database on EC2, you could use one of the managed AWS database offerings like Amazon RDS? The big difference between these two options is instead of taking care of the instances, the patching, the upgrades, and the install of the database, AWS takes care of all of that undifferentiated heavy lifting for you. 
# __
![[Pasted image 20230707163438.png]]
The task that you are then responsible for is the creation, maintenance, and optimization of the database itself. So you are still in charge of creating the right schema, indexing the data, creating stored procedures, enabling encryption, managing access control, and more. But all the rest of the undifferentiated heavy lifting that goes into operating a relational database AWS takes care of. 
# __
To start off this section of lessons on databases, we will first cover RDS. The upcoming reading after the video will dive into the history of enterprise relational databases and explain what relational databases are and how they were used. If you aren't familiar with databases, the readings coming up will give you some useful background information.
# __