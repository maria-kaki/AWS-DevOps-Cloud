EC2 instances give you a lot of flexibility and control in the cloud, and you configure them to meet your needs. You can provision one or many instances easily and at the end of the billing cycle, you only pay for what you use, either per second or per hour depending on the type of the instance. When you no longer need an instance, you can terminate or stop the instance and you will stop incurring charges. Not all servers are the same, and you are probably looking to run a specific type of operating system on your EC2 instance. AWS supports a range of operating systems including Linux, MacOS, Ubuntu, Windows, and more.
# __
![[Pasted image 20230701014753.png]]
To select the operating system for your server, you must choose an Amazon Machine Image or an AMI.
# __
![[Pasted image 20230701014839.png]]
The AMI contains information about how you want your instance to be configured including the operating system, possible applications to be pre-installed on that instance upon launch, and other configurations. You can launch one or many instances from a single AMI, which would create multiple instances that all have the same configurations. Some AIs are provided by AWS whereas others are provided by the community and could be found using the AWS Marketplace or you can build your own custom AMIs as needed.
# __
For example, Amazon Linux 2 is the AMI we selected when we launched our Employee Directory Application. This AMI is provided by AWS and it's essentially a pre-built EC2-optimized Linux Image that has long-term support provided by AWS. Beyond the properties determined by the AMI, you can also configure the instance type in size which correspond to the amount of compute, memory, and network capabilities available per instance. Different applications have different hardware requirements and choosing the instance type for your application gives you the ability to pick the hardware that it runs on. It's also really nice that you have a wide variety of choices as it's hard to achieve that same level of variety with on-premises resources.
# __
![[Pasted image 20230701015332.png]]
The instance types you can choose from are grouped for use cases like compute-optimized, memory-optimized, storage-optimized instances, and more. There's a list of instance types you can find in the AWS documentation, and you can expect this page to be updated regularly as new instance types are released.
# __
For example, the G instance family are optimized for graphics intensive applications, which would work best for use cases such as 3D visualizations or video encoding. Whereas the M5 General Purpose EC2 instance family provides a balance of resources and are great for applications that use these resources in equal proportions like web servers, our Employee Directory Application example, or co-repositories.
# __
![[Pasted image 20230701015647.png]]
When you are launching an EC2 instance, you will see something like this when selecting an instance type and size. The T3 or A1 is the instance type that determines the blend of hardware capabilities, then the dot, then the size like small, medium, large. It goes down to nano and up to many, many extra large sizes.
# __
![[Pasted image 20230701104127.png]]
The great thing about this type of selection existing right at your fingertips is that you are no longer locked into hardware decisions upfront. You can choose an initial EC2 instance type, evaluate its performance for your specific use case, and then later change it to a different type that is better suited for the application.
# __
![[Pasted image 20230701104231.png]]
EC2 is also re-sizable with a few clicks in the console or can be done programmatically through an API call.
# __
![[Pasted image 20230701110259.png]]
![[Pasted image 20230701110316.png]]
All of these configurations being available to you via API enables you to embrace change over time easily as your workloads mature and change.
# __
So okay, virtual machines are cool and totally not new, so how exactly does this impact your business? Well, the important thing is this. The flexible and low-cost nature of EC2 instances as well as the ease of provisioning servers allows for programmers and businesses to innovate more quickly by spinning up servers for a short amount of time to run experiments and find optimal configurations for your applications.
# __
![[Pasted image 20230701112352.png]]
EC2 offers a wide variety of hardware options to choose from so you can optimize your solutions by selecting the right EC2 instance type for your application, and then you can optimize even further by right-sizing the resource or selecting an instance size that is appropriate for your application and not over provisioning like is often done on premises.
# __
This type of optimization is hard to achieve on your own because with traditional on-premises deployments, you are working with hardware constraints that simply don't exist in the same way with the cloud. The ability to adapt to changes and choose really specific configurations for your virtual machines all through a couple of API calls is very powerful and EC2 is really just the beginning of the story.
# __