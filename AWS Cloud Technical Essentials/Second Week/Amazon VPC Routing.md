![[Pasted image 20230705225125.png]]
Let's take a look at our current VPC state. In the last video, we left off with a VPC with an internet gateway attached to it, and two subnets one public, one private, and one availability zone. However, Morgan was kind enough to build additional resources in the background to make sure our application was highly available. So now we have two additional subnets, one public, one private, and a different AZ for a total of four subnets. She also created an EC2 instance hosting our employee directory inside of the public subnet in AZ A. But we are missing one large component here. Say we have a user and that user wants to access our employee directory. Eventually that internet traffic would flow through the internet gateway, but then where would it go? Just because the traffic entered through the door of the VPC it doesn't mean it ever made it to the right room. What we need to do is to provide a path for the internet traffic, not only to enter the door but also make sure traffic reaches the right room or in other words, enter the internet gateway and then find the right subnet. 
# __
![[Pasted image 20230705225252.png]]
The way we provide that path is through route tables. 
# __
A route table contains a set of rules called routes that are used to determine where the network traffic is directed. These route tables can be applied at either the subnet level or at the VPC level. 
# __
![[Pasted image 20230705225350.png]]
When you create a brand new VPC, AWS creates a route table called the main route table and applies it to the entire VPC. AWS assumes that when you create a new VPC with subnets you want traffic to flow between those subnets. In the last video when we talked about VPCs being isolated, this is what we meant. The default configuration of the main route table is to allow traffic between all subnets local to the VPC. 
# __
![[Pasted image 20230705232524.png]]
In the VPC console, we'll click on route tables on the side panel and it will bring up all of the route tables that exist in this region. 
# __
![[Pasted image 20230705232602.png]]
If we scroll to the side, we can see the main column and the VPC column. We're going to look for the main route table for the app VPC, which is this one. When we click on it, 
![[Pasted image 20230705232634.png]]
we can bring up the bottom panel and then click on routes. 
![[Pasted image 20230705232653.png]]
Here we can see the local route that has the destination of the VPC range. This means that all of the components inside of our VPC can communicate with one another locally by default. This local route will be present in every route table that you create. Alright, that's the main route table. 
# __
![[Pasted image 20230705233018.png]]
While the main route table controls the routing for your entire VPC, you may want to be more granular about how you route your traffic to specific subnets. Remember when we mentioned that subnets can be used to group your resources together based on whether they are publicly or privately accessible? Well, the subnet itself doesn't provide that access. Whether a subnet has access to the public internet or not, depends on its associated route table. 
# __
![[Pasted image 20230705233356.png]]
If a route from the internet gateway to the subnet exists, it has public access. If the route table doesn't have a route between the subnet and the internet gateway then it doesn't have public access. So we call subnets public or private but it's really the route table that provides that access. So for your subnets, you'll create custom route tables. Inside these custom route tables, you'll have that default local route inside of it that allows traffic to flow freely within the VPC but then you'll need to create additional routes. So the subnet with the internet facing resource in this case, our EC2 instance with the employee directory website on it, will need a route to the internet gateway. 
# __
So that means, Morgan, we need your help again. Do you mind creating a custom route table and associating it to our public subnet? - Sure can. Let's get started. Let's create the route table for our public subnet. 
# __
![[Pasted image 20230705233442.png]]
![[Pasted image 20230705233503.png]]
Back in the VPC console once again, we'll click on Route tables on the side panel and then Create route table. 
# __
![[Pasted image 20230705233530.png]]
We'll give it a name such as app-routetable-public, choose the app-vpc, and then click Create. 
# __
![[Pasted image 20230705233643.png]]
Our route table has been created, but we're not done yet. We still have to edit the routes to allow traffic to flow from the internet gateway. To do this, we'll click on the ID of the route table and then go to the route section in the bottom of the summary table. 
# __
![[Pasted image 20230705233708.png]]
We'll click Edit routes, 
# __
![[Pasted image 20230705233734.png]]
Add route, put 0.0.0.0/0 for the destination, meaning it can take and deliver traffic from anywhere and then specify the target as an internet gateway. This will bring up available internet gateways to attach it to and from here, we'll select the app IGW. We're done with the routes, so we'll click Save. 
# __
![[Pasted image 20230705233818.png]]
But how do you know which subnet this route table applies to? Well, we have to configure that. If we only want this route table to apply to our public subnets, we'll need to associate it with our two public subnets only. To do this, we'll click on the Subnet associations tab. Select Edit subnet associations 
![[Pasted image 20230705233854.png]]
and choose the public subnets we created earlier. Then click Save. 
# __
Alright, we've hooked up our public subnets to a route table that allows internet traffic from the IGW to our employee directory application. If we wanted to create a route table for the private subnets, we would follow the same steps. Create the route table, make sure there's no route to the internet gateway this time and then associated to the private subnets. 
# __
Okay, now we've configured a route to the internet gateway and we'll configure additional firewall rules later on. - Nice. So this is our final state of the diagram. 
# __
![[Pasted image 20230705234004.png]]
One VPC, four subnets, one public, one private in both availability zones. Our two public subnets are associated with a route table that allows traffic from the internet gateway. Our private subnets don't have a route table associated to them yet, so they follow the rules of the main route table, local traffic only.