Now that we have multiple EC2 instances hosting our application in private subnets, it's time to distribute our request across our servers using the Elastic Load Balancing or ELB service.
# __
![[Pasted image 20230707212415.png]]
Conceptually, how this would work is a typical request for the application would start from the browser of the client and is then sent to the load balancer. From there, the load balancer determines which EC2 instance to send the request to. 
# __
![[Pasted image 20230707213237.png]]
After it sends the request, the return traffic would go back through the load balancer and back to the client browser, meaning your load balancer is directly in the path of traffic. 
# __
![[Pasted image 20230707213259.png]]
Now if we're looking at the architecture, the ELB looks like one thing. It looks like a single point of failure. But ELB is actually, by design, a highly available and automatically scalable service, much like S3 is. 
# __
What that means is that A, the ELB is a regional service, so you don't have to worry about maintaining nodes in each availability zone or having to configure high availability yourself. AWS maintains that for you. 
# __
![[Pasted image 20230707213625.png]]
And B, the ELB is designed to handle additional throughput and will automatically scale up to handle the traffic coming in, without you having to configure that feature. 
# __
![[Pasted image 20230707213703.png]]
Now there are several types of load balancers that you can choose. There's the Application Load Balancer that load balances HTTP and HTTPS traffic. There's the Network Load Balancer that routes TCP, UDP, and TLS traffic. And there's the Gateway Load Balancer that is mainly used to load balance requests to third-party applications. 
# __
For our employee directory application, we'll be load balancing web traffic so we'll be using the Application Load Balancer or the ALB. 
# __
![[Pasted image 20230707232426.png]]
When you create an ALB, you'll need to configure three main components. The first component is a listener. The goal of the listener is to check for requests. To define a listener, a port must be provided as well as the protocol. For example, since we're routing web traffic and we set our application to use port 80, we'd want our load balancer to listen to port 80 using the HTTP protocol. Additionally, we could set up a listener port for 443 using the HTTPS protocol. 
# __
![[Pasted image 20230707232440.png]]
The second component is a target group. A target is the type of backend you want to direct traffic to, such as an EC2 instance, AWS Lambda functions, or IP addresses. A target group is simply just a group of these backend resources. Each target group needs to have a health check, which is how the load balancer can check that the target is healthy so that it can start accepting traffic. The ALB operates on the application layer, which is layer seven of the OSI model. This gives the load balancer a lot of cool features, and one of those is the third component, which is a rule. 
# __
![[Pasted image 20230708134043.png]]
A rule defines how your requests are routed to your targets. Each listener has a default rule and you can optionally define additional rules. 
# __
![[Pasted image 20230708134122.png]]
So if we had two target groups, A and B, we can set up an additional rule that says if traffic is coming to our /info page, we can deliver that traffic to target group B. So because of the fact ALB operates on layer seven, you can customize paths for your traffic. 
# __
![[Pasted image 20230708134223.png]]
Let's create an Application Load Balancer in the console. If you want to find the ELB service, you'll need to go to the EC2 console, so we'll type in EC2 to the service search bar and then on the side panel, 
![[Pasted image 20230708134305.png]]
we'll select Load Balancers. Once we bring up our load balancers dashboard that shows all of the load balancers for this region, 
![[Pasted image 20230708135213.png]]
we'll then click Create load balancer. 
# __
![[Pasted image 20230708135852.png]]
Here's where we choose which type of ELB we want and you see the three main types. We'll be using the ALB. 
# __
![[Pasted image 20230708135925.png]]
From here, we'll choose a name and call it app-elb. 
# __
![[Pasted image 20230708135956.png]]
The next setting asks if we want an internet-facing or an internal-facing load balancer. 
# __
![[Pasted image 20230708140450.png]]
An internet-facing load balancer does what you might expect, which is route requests from clients over the internet to your backend servers or targets. An internal load balancer, on the other hand, will route requests from clients with a private IP to targets with a private IP. For example, if you had a three-tier application with a web, app, and database tier, you could use an internal-facing load balancer to route traffic from your web tier to your app tier. 
# __
![[Pasted image 20230708140534.png]]
For this app, we'll be routing internet traffic, so you can leave it as internet-facing. After that, we choose which availability zones we want to route traffic to. First, we'll choose the VPC, 
![[Pasted image 20230708140604.png]]
select both availability zones, and then choose the two public subnets. 
# __
![[Pasted image 20230708140642.png]]
Now you choose your security group for your load balancer. 
# __
![[Pasted image 20230708140707.png]]
This is where you decide which traffic you want to allow in. Here we'll choose a security group that will allow traffic on port 80 from anywhere. 
# __
![[Pasted image 20230708140800.png]]
Then, we configure the listeners and routing. Currently, the default setting is to allow HTTP traffic on port 80. If we want to allow or limit to HTTPS traffic, we can click Add listener and choose HTTPS, but for this demo, we'll stick with the default. 
# __
![[Pasted image 20230708140848.png]]
Next, we'll configure routing, and for this, we need to click on Create a target group. 
# __
![[Pasted image 20230708140909.png]]
This will open a new page where we can configure the target group. First, we will select the target type, which will be instances. 
# __
![[Pasted image 20230708140941.png]]
Then we can scroll down and we'll give it a name, such as app-target-group, and leave all of the defaults selected. 
# __
![[Pasted image 20230708141001.png]]
Then we'll click Next to choose which instances we want to live in the target group. 
# __
![[Pasted image 20230708141150.png]]
For here, I'll choose the two instances I've created in private subnets and click Include as pending below
![[Pasted image 20230708141228.png]]
and click Create target group. 
# __
![[Pasted image 20230708141251.png]]
Now coming back to the load balancer creation page, if we refresh the dropdown for target groups, we'll see the target group that was just created. 
# __
![[Pasted image 20230708141317.png]]
We will select this and then scroll down, accepting the rest of the defaults and 
![[Pasted image 20230708141348.png]]
clicking on Create load balancer. 
# __
![[Pasted image 20230708141407.png]]
After the load balancer has been created, we can then select it and find the DNS URL in the description box. 
# __
![[Pasted image 20230708141435.png]]
We can then pull that DNS URL, copy and paste it into a new tab, and from here you can see our app. 
# __
![[Pasted image 20230708141512.png]]
If I go to the /info page of our app, you can see which availability zone we're currently in. If I refresh the page a few times, you should see eventually that I'm being directed to both my EC2 instances in both AZs.
# __