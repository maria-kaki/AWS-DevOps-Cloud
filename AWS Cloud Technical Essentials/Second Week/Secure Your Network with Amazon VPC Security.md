Well, at the base level, we know that any new VPC is isolated from internet traffic, so that prevents risk. But when you start allowing internet traffic by opening up routes, you need other options to keep your network secure. In AWS, you have two options to secure your VPC resources: 

- network access control lists, 
- often referred to as network ACLs, 
- and security groups. 
# __
![[Pasted image 20230705235036.png]]
We'll start with network ACLs. You can think of a network ACL as a firewall at the subnet level. With network ACLs, you can control what kind of traffic is allowed to enter and leave your subnet. So if I were to draw network ACLs in our diagram, they are placed around each of our subnets by default. 
# __
The default network ACL allows traffic in and out of your subnet. Using this default configuration is a good starting place but if needed, you can change the configurations of your network ACLs to further lock down your subnets. 
# __
![[Pasted image 20230705235130.png]]
For example, if I only wanted to allow HTTPS traffic into my subnet, I can do that. 
# __
![[Pasted image 20230705235156.png]]
I can create a rule in my ACL that allows HTTPS traffic from anywhere on port 443 and denies everything else. 
# __
![[Pasted image 20230705235223.png]]
However, just because I allow inbound HTTPS traffic does not mean my job is done. If I don't open up the corresponding outbound port used for the protocol, then that means the traffic is allowed in but the web server's response will never leave the subnet.
# __
![[Pasted image 20230705235244.png]]
This is because network ACLs are considered to be stateless. I need to include both the inbound and the outbound ports used for the protocols. What that means for our HTTPS example is that I need to allow outbound HTTPS traffic from the subnet to the internet by creating an outbound rule. 
# __
The other security feature is security groups. These are firewalls that exist at the EC2 instance level. Security groups are not optional, so anytime you create an EC2 instance, you need to place that EC2 instance inside of a security group that allows the appropriate kinds of traffic to flow to your application. 
# __
![[Pasted image 20230705235401.png]]
In our diagram, if I were to draw security groups, I would draw them around every EC2 instance in the VPC. In our case, we simply just have one EC2 instance. So we would need a security group around that instance. 
# __
You know what? I think it's time for a demo. Let's get Morgan back in here. - Hey, Seph, what should I demonstrate next? - Do you have some time to build out a security group for our employee directory application? I think we need an example. - Sure, let's get started. 
# __
![[Pasted image 20230705235450.png]]
The default configuration of a security group blocks all inbound traffic and allows all outbound traffic. 
# __
![[Pasted image 20230705235519.png]]
![[Pasted image 20230705235544.png]]
If you want your EC2 instance to accept traffic from the internet, you'll need to open up inbound ports. If you have a web server, you may need to accept HTTP and HTTPS requests to allow that type of traffic through your security group. You can create an inbound rule that will allow port 80, HTTP, and port 443, HTTPS, as shown here. 
# __
![[Pasted image 20230705235611.png]]
The beauty of security groups is that I don't have to open up an outbound port for traffic to be able to leave the instance. 
# __
Security groups are considered to be stateful resources. They will remember if a connection is originally initiated by the EC2 instance or from outside and temporarily allow traffic to respond without having to modify the inbound rules. All right, is that everything? - That's it for this one, thanks. Remember that security groups and network ACLs are powerful tools to filter network-wide traffic for a single instance or subnets traffic. With security groups, everything is blocked by default so you can only use allow rules, whereas with network ACLs, everything is allowed by default but you can use both allow and deny rules. These configurations are largely up to you. For example, if you want ultimate convenience, you can leave the network ACLs in the default configuration and use mainly security groups to restrict access. We'll be doing just that with our employee directory application and it will still be secure. But if you want an added layer of security, you can configure your network ACLs further for more fine-grained control.