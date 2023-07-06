In this video, you'll be learning how to create a VPC with Morgan's help. We'll both be conceptualizing and building a VPC throughout the next few videos. The idea of a VPC is similar to how you think of walls around a data center. In a data center, walls act as a boundary between the outside world and all of your infrastructure. A VPC in AWS acts the same way. It creates a boundary where your applications and resources are isolated from any outside movement, so nothing comes into the VPC and nothing comes out of the VPC without your explicit permission. 
# __
![[Pasted image 20230705154746.png]]
When you create a VPC, you have to declare two specific settings; the region you're selecting, and the IP range for the VPC in the form of CIDR notation. (notification dings) For our VPC, we'll be locating it in the region where the rest of our infrastructure will be, the Oregon region. and our IP range will say is 10.1.0.0/16.
# __
Alright, so currently our VPC looks just like a box. Time to build the VPC. (swoosh effect) Okay, Morgan, let's build out a VPC for the Employee Directory app. I was hoping you could build us a VPC that matches this diagram. 
# __
![[Pasted image 20230705204512.png]]
If you're looking at the console, you'll first check to make sure that you're in the correct region by clicking on the upper right hand corner. Seph mentioned we're going to run out of the Oregon region, so we'll go ahead and make sure that this says Oregon. 
# __
![[Pasted image 20230705204538.png]]
Once we choose the right region, we can now build our network. You'll type in VPC in the service search bar and that'll bring up your VPC dashboard for this region. 
# __
![[Pasted image 20230705204606.png]]
![[Pasted image 20230705204643.png]]
From there, you'll click your VPCs and then Create VPC. 
# __
![[Pasted image 20230705204707.png]]
Now we'll have a few settings to configure. We'll put in the CIDR block, which is 10.1.0.0/16, and the VPC name, which we'll say is app-vpc.  
# __
![[Pasted image 20230705204739.png]]
We'll leave the rest as default, and then we'll click Create VPC. 
# __
![[Pasted image 20230705204848.png]]
After you create your VPC, you then divide the space inside the VPC into smaller segments called subnets. You put your resources, such as your EC2 instances, inside of these subnets. The goal of these subnets is to provide more granular control over access to your resources. So if I have public resources, like our Employee Directory app, that we want to be accessed over the internet, I could put these resources inside a subnet with internet connectivity. 
# __
![[Pasted image 20230705205045.png]]
If I have more private resources, like a database, I could create another subnet and have different controls to keep those resources private. To create a subnet, you need three main things; the VPC you want your subnet to live in, which is this one, the AZ you want your subnet to live in. In this case, we'll choose AZ A, or in other words us-west-2a, and then the CIDR range for your subnet, which must be a subset of the VPC CIDR range. For this, we'll choose the range 10.1.1.0/24. We'll call this our Public Subnet for public facing resources. Then we'll create another subnet for our private resources. We'll place it in the same AZ, specify a different non-overlapping CIDR range, say 10.1.3.0/4, and then name it our Private Subnet. 
# __
![[Pasted image 20230705205143.png]]
Alright, now that we've got two subnets added to our VPC, it's time to put Morgan to the test again and have her build these out. And this time I'm timing her. - All right, we're on a time limit here, so let's create these subnets. Let's go ahead and start creating the public subnet. 
# __
![[Pasted image 20230705205236.png]]
Back in the console, we'll click on Subnets in the side panel, and then select Create subnet. 
# __
![[Pasted image 20230705205349.png]]
Then we'll select the VPC we're working with, in this case is app-vpc. 
# __
![[Pasted image 20230705205430.png]]
Once you do that, you'll be prompted to provide a name. We'll say this one is Public Subnet 1. Then we'll choose the AZ, which Seph mentioned was us-west-2a, and then the CIDR range will be 10.1.1.0/24. 
# __
![[Pasted image 20230705205503.png]]
We'll leave the rest as defaults, scroll down to the bottom, and click Add new subnet. 
# __
![[Pasted image 20230705205534.png]]
![[Pasted image 20230705205628.png]]
We'll now repeat the same steps for our private subnet. Give it a name such as Private Subnet 1. Put it in the same availability zone, us-west-2a, and then type in the CIDR range, which is 10.1.3.0/24. Now we can click Create subnet, and both subnets will be created. 
# __
As we mentioned earlier, when you create a new VPC, all the resources you put in it are isolated, and only have access to other resources in that VPC by default. For websites like our corporate directory application, we want users to access our site over the internet. 
# __
![[Pasted image 20230705210026.png]]
To enable internet connectivity, we need a component called an internet gateway. Think of this gateway as similar to a modem. Just as a modem connects your computer to the internet, the internet gateway connects your VPC to the internet. When you create an internet gateway, you then need to attach it to your VPC. 
# __
If you create an internet gateway and don't attach it, it won't do anything except sit there. Okay, Morgan, show us how it's done. Create an internet gateway and attach it to our VPC.
# __

Back in the VPC dashboard, you'll click on Internet gateways on the side panel, then Create internet gateway. You'll give the internet gateway a name, and then click Create. On the details page, you'll then select the Actions dropdown box and select Attach to VPC. Choose the app-vpc we've been working with, and then click Attach. Okay, Seph, what's next? - Oh, sorry, I thought I'd have more time to drink my tea. So we have an internet gateway that we can use to allow access from the internet, but what if we had a VPC with all internal private resources that we want to reach only from our on-premises data center? If we only want traffic to flow between AWS and our data center, and we don't want to allow direct access from the internet, what do we do? Luckily, there's another gateway designed for this very purpose called a virtual private gateway or VGW. It allows you to create a VPN connection between a private network, like an on-premises data center or internal corporate network, to your VPC. With the help of a VGW, you can establish an encrypted VPN connection to your private internal AWS resources. We won't be using a VGW for our application but it's good to know. We'll talk more about that in an upcoming lesson. Alright, so we have one VPC, two subnets, and an internet gateway. Now, every time you look at an architecture, you should begin to think, how do I make this better? You're not going to have all of the answers right away, but I do want you to take 10 seconds and think about some solutions. (light jazz music) Okay, well, one option to make this better is the idea of having high availability. What that means is if this AZ goes down for whatever reason, what happens to our resources in that AZ? They go down too. So ideally we would have resources in another AZ to take on the traffic coming to our application. To do this, we'd need to duplicate the resources in the first AZ to the second AZ, so that means we'd need to create two additional subnets, each within another AZ, say AZ B. As a best practice, you should always be using at least two AZs, and hosting your resources redundantly. Morgan is going to build out some subnets in another AZ in the background for the rest of our demos. She's also going to launch an EC2 instance hosting our application in one of the public subnets. Sound good, Morgan? - Sounds good. Okay, we'll see you in an upcoming video. This time with one VPC, four subnets across two AZs, and one running EC2 instance.