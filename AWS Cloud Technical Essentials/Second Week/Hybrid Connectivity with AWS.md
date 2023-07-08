The solution we are building out with the employee directory application is an all in cloud meaning that the components needed to run and operate the application will be in AWS. However, many solutions require a hybrid model to be followed, where some components are in AWS and others are hosted in an on-premises data center. Let's take some time to talk about connectivity to AWS for hybrid deployments. For hosting your resources in AWS you would use a VPC which you learned about in the previous lessons. For hosting resources on-premises you'd have your own solutions in an on-premises data center. So for connectivity to AWS how will you connect the remote data center to AWS? Let's talk about a few choices you can pick from where you're looking at connectivity between AWS and a remote site like a data center.
# __
![[Pasted image 20230705235939.png]]
First, let's talk about AWS Virtual Private Network or AWS VPN. VPNs are a really common and popular way to securely connect your remote network to AWS. AWS VPN consists of two different services, AWS Site-Site VPN and AWS Client VPN. 
# __
![[Pasted image 20230706000008.png]]
AWS Site-Site VPN is used to connect a remote network like a data center to a VPC. This would allow resources living in a customer managed data center to connect to AWS. 
# __
![[Pasted image 20230706000030.png]]
Then there is AWS Client VPN which is more for connecting your administrators to AWS or to your data center. So this is more like when you need to log into a VPN on your laptop to access corporate resources. 
# __
Using AWS VPN you can connect to your VPC through the virtual private gateway which we covered in an earlier video. Just like the internet gateway is the doorway to the internet. The virtual private gateway is the doorway to your private data center through a VPN connection or through another service called AWS Direct Connect. 
# __
![[Pasted image 20230706000123.png]]
AWS Direct Connect is a service that provides a hosted private connection to AWS through a Direct Connect delivery partner, or through AWS. 
# __
![[Pasted image 20230706000205.png]]
Direct Connect provides a private dedicated connection. This isn't using the regular open internet to send data between point A and point B. While the data sent over Direct Connect is in transit the network traffic remains on the AWS global network and never touches the public internet. This reduces the chance of hitting bottlenecks or unexpected increases in latency when compared to a VPN connection. AWS Direct Connect supports a larger and more reliable throughput. 
# __
If you plan to send a high volume of traffic to AWS and you do need reliability in throughput for this connection AWS Direct Connect would be a good choice. It really depends on your use case which one you would use or in some cases you may use both. Where VPN is a failover for Direct Connect. Now, let's get back to building the employee directory application.
# __