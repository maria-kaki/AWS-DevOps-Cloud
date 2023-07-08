When you launch an EC2 instance you're going to need some kind of block storage to go with it. This block storage can be used as a boot volume for your operating system or a separate data volume. For example, think about your laptop. 
# __
![[Pasted image 20230706221753.png]]
With a laptop you store your data in drives, and those drives are either built-in internally to your laptop or connected externally. EC2 instances have the same options as far as block storage goes. The internal storage is called Instance Store and the external connected storage is called Amazon Elastic Block Store or Amazon EBS. Let's talk about Instance Store first. 
# __
![[Pasted image 20230706221831.png]]
Instance Store is a form of directly attached storage which means the underlying physical server has at least one storage unit directly attached to it. This direct attachment is also the main advantage of using this form of storage. Because it's so close to the physical server it can be very fast and respond very quickly, but while it can be very fast, there is also one big downside. With Instance Store being directly attached to an EC2 instance, its lifecycle is tied to that of the instance. 
# __
![[Pasted image 20230706221913.png]]
That means if you stop or terminate an instance all data in the Instance Store is gone. It can no longer be used or accessed. 
# __
Naturally there are many use cases where you want the ability to keep data, even if you shut an EC2 instance down. This is where EBS volumes come in. These volumes, as the name implies, are drives of a user configured size that are separate from an EC2 instance. The drives are simply network attached storage for your instances. You can think of it as similar to how you might attach an external drive to your laptop. You can attach multiple EBS volumes to one EC2 instance, and then you can configure how to use that storage on the OS of the EC2 instance. When I connect that EBS volume to my instance, my instance now has a direct communication line to the data in that volume. Nobody else can directly talk to that volume so that it maintains secure communication. You need an EC2 instance to access data on an EBS volume. If I decided I want to use that EBS volume with a different instance, that's no problem. We can stop the instance, detach the volume, and then attach it to another instance in the same AZ. Much like you can unplug your drive from a laptop, and plug it into another one. 
# __
![[Pasted image 20230706222033.png]]
Or depending on the instance type and EBS volume we're using we may be able to attach it to multiple instances at the same time, which is called EBS Multi-Attach. 
# __
And perhaps the most important similarity is that an EBS volume is separate from your instance. Just like an external drive is separate from your laptop. That means if an accident happens, and the instance goes down you still have your data on your EBS volume. This is what we refer to as persistent storage. You can stop or terminate your instance, and your EBS volume can still exist with your data on it. EBS is often the right storage type for workloads that require persistence of data. However, the question typically comes down to which EBS volume type do I use? That's right. There are many different types of volumes, but they've divided into two main volume types. SSD backed volumes and HDD backed volumes. In the readings, you'll learn more about these two options. The last thing we'll need to talk about here is backing up data. Things fail, errors happen, so you need to backup your data, even in AWS. The way you backup EBS volumes is by taking what we call snapshots. EBS snapshots are incremental backups that are stored redundantly. The idea here is that if something goes wrong you can create new volumes from your snapshots and restore your data to a safe state.