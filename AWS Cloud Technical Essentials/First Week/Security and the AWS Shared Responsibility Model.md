![[Pasted image 20230629143304.png]]
![[Pasted image 20230629145354.png]]
You can see we have the responsibility of security broken into two groupings, you and AWS each being responsible for different components. We describe AWS as being responsible for security of the cloud. For example, one piece of the puzzle for AWS is the AWS global infrastructure. And when I say global infrastructure, I mean the physical infrastructure that the cloud is running on. This is iron and concrete buildings with fences protected by security guards and various other security measures. It also includes the AWS global backbone or the private fiber cables that connect each AWS region to each other. Managing the security of these pieces is all in AWS. You don't need to worry about that as far as security goes. Then there is the infrastructure in various software components that run AWS services. This includes compute databases, storage, and networking. AWS is responsible for securing these services from the host operating system up through the virtualization layer. For example, let's say you want to host some virtual machines or VMs on the cloud. We primarily use the service Amazon EC2 for this use case. When you create a VM using EC2, AWS manages the physical host the VM is placed on as well as everything through the hypervisor level. If the host operating system or the hypervisor needs to be patched or updated, that is the responsibility of AWS. This is good news for you as the customer, as it greatly reduces the operational overhead in running a scalable and elastic solution leveraging virtualization.
# __
![[Pasted image 20230629145752.png]]
Similar to how a construction company builds a building and it's on them to make sure that the building itself is stable and secure then you can rent out an apartment in that building. It's up to you to lock the door to your apartment. Security of the building and security in the building are two different elements. For security in the cloud, the base layer is secured by AWS. It's up to you to lock the door. So for our EC2 example, you are responsible for tasks like patching the operating systems of your VMs, encrypting data in transit and at rest, configuring firewalls and controlling who has access to these resources and how much access they have.
# __














