At this point, you know how to set up alarms to notify you when your infrastructure is having capacity, performance, or availability issues. But we need to go one step further. We don't just want to know about these issues. We want to either prevent them or respond to them automatically. In this section of the course you'll learn how to do just that.
# __
![[Pasted image 20230707205717.png]]
Currently, our infrastructure looks like this. We have one EC2 instance hosting our employee directory application in a single availability zone with DynamoDB as its database, and S3 for storage of static assets. If I wanted to evaluate the availability of our infrastructure, I have to look at each individual component. I know that both DynamoDB and Amazon S3 are highly available by design, so that leaves one issue, this singular instance of our application.
# __
![[Pasted image 20230707205754.png]]
If that instance goes down employees have no way to connect to our application. How do we solve this? Well, as you already know, to increase availability, we need redundancy. We can achieve this by adding one more server, but the location of that server is important. If instance A goes down we don't want instance B to go down for the same reasons. So to avoid the unlikely event of, say, an AZ experiencing issues, we should ensure that instance B is put in another AZ.
# __
![[Pasted image 20230707205846.png]]
So now we have two instances that we've manually launched, but let's say our company grows rapidly, and the employee directory application is constantly being accessed by thousands of employees around the world. To meet this demand we could scale our instances vertically, meaning we could increase the size of the instances we have, or we could scale our instances horizontally, meaning we could add more instances to create a fleet of instances. If we scale vertically eventually we'll reach the upper limit of scalability for that instance. But if we scale horizontally, we don't have those same limitations. I can add as many instances to my fleet as I'd like, but if I need, say, 15 more instances to meet demand, that means I'd have to manually launch those 15 instances and manually shut them down, right? 
# __
Well, you could do it that way, or you could automate this process with Amazon EC2 auto scaling. This service will allow you to add and remove EC2 instances based off of conditions that you define. With this service, you can also maintain the health of your fleet of instances, but with more EC2 instances comes a bigger issue. How do we access those servers? 
# __
![[Pasted image 20230707205956.png]]
Before we were simply using the instance public DNS name, or public IP address, but when you have multiple instances, you have multiple of IPs to route to. Instead of maintaining the logic to send requests to your various servers, you would use a load balancer to distribute those requests across a set of resources for you. And since you can connect from your load balancer to access the application, you no longer need to use the public IPs of your EC2 instances.
# __
Before the next video I'll spin up two instances hosting our employee directory application. See you soon.
# __