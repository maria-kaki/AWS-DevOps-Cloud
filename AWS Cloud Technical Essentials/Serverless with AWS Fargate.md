Now that you have learned about what container services AWS offers and what serverless means, let's continue our conversation about containers. To recap, ECS or EKS is the container orchestrator. This is the tool that is managing the container's lifecycle. Then you need the compute platform. This is where the containers actually run. 
# __
![[Pasted image 20230703111918.png]]
Previously, you learned that ECS and EKS run containers on clusters of EC2 instances. And in that case, you were using EC2 as the compute platform for your containers, and you also have tight control over those instances. Now, EC2 is certainly not serverless. So thinking about serverless compute for containers, I want to introduce to you a service named AWS Fargate. 
# __
![[Pasted image 20230703112046.png]]
AWS Fargate is a serverless compute platform for containers that you can use with either ECS or EKS. With AWS Fargate as the compute platform, you run your containers on a managed serverless platform. The scaling and fault tolerance is built-in, and you don't need to worry about the underlying operating system or environment. 
# __
Instead, you define your application content, networking, storage and scaling requirements. There is no provisioning, patching, cluster capacity management or infrastructure management required. 
# __
![[Pasted image 20230703114105.png]]
To break that down a bit, the way you work with Fargate is you first build your container images and push them into a repository like Amazon Elastic Container Registry, for example. Which is a place where you can store container images for them to be pulled and deployed from. So you have your container images in your repo, and then you define memory and compute resources for your task if you're using ECS or your pod if you're using EKS. Then you run your containers. And at the end, you only pay for the amount of vCPU, memory and storage resources consumed by your containerized applications. 
# __
Fargate does support spot and compute savings plan pricing options just like with Amazon EC2 instances. So there is some flexibility on how you plan to run containers on Fargate. So you can still get a good amount of control for your container's deployment, but without needing to worry about the provisioning, patching and managing the underlying operating systems or instances. And no need to scale the infrastructure in and out to meet demand like you do with EC2. As far as use cases go, AWS Fargate can be used for all of the common container use cases including microservice architecture applications, batch processing, machine learning applications and migrating on-premises applications to the cloud. All right, hopefully, you now have a 10,000-foot view of AWS Fargate. You can see how Fargate is an example of how serverless simplifies your operations and management for running scaled container solutions.
# __