As more people visit our application, the demand on our two web servers is going to increase. At some point, our two instances aren't going to be able to handle that demand, and we're going to need to add more EC2 instances. Instead of launching these instances manually, we want to do it automatically with EC2 Auto Scaling. Autoscaling is what allows us to provision more capacity on demand depending on different thresholds that we set and we can set those in CloudWatch. Okay, so we're going to draw a high level example of how this works and then Seth is going to build it for us. 
# __
![[Pasted image 20230708142335.png]]
So looking at our application, traffic coming in from the outside can come down to either EC2 instance. In this video, these EC2 instances will be part of an auto-scaling group. Each of the EC2 instances that we launch will be completely identical. 
# __
![[Pasted image 20230708142458.png]]
Then we're going to run code to simulate stress on our employee directory application that will make the instances think that they're overloaded. When this happens, the instances will report to CloudWatch and say that their CPUs are overloaded. CloudWatch will then go into an alarm state and tell auto-scaling, give me more EC2 instances. As each instance comes online, they will pass ALB Health checks. They'll start to receive traffic and give us the horizontal scalability that we need. 
# __
![[Pasted image 20230708174817.png]]
So to get this built out, the first thing we need to do is create a launch template. This is going to define what to launch. So it's all about setting the configurations for the instances we want to launch. Morgan said we want our instances to be identical and that's what we'll be configuring here. First thing we're going to do in the EC2 dashboard is find launch templates on the side panel and click create launch template. 
# __
![[Pasted image 20230708174853.png]]
We'll first provide a name and description. I'll call this app-launch-template and give it a description of a web server for the employee directory app. Then you'll notice this handy check box that asks if we are going to use this launch template with EC2 Auto Scaling. We are.
# __
![[Pasted image 20230708174919.png]]
So we'll check it and scroll down. 
# __
![[Pasted image 20230708175056.png]]
We'll then choose the AMI, again, the launch template is all about what we launch. So what we want to do is create mirrors of the web servers hosting our app that we already have running. 
# __
![[Pasted image 20230708175324.png]]
That way whenever we scale out, we just have more instances with the exact same configuration. When we launched the instance hosting our app earlier, we use the Amazon Linux, AMI, and a T2 micro instance type. 
# __
![[Pasted image 20230708175457.png]]
So we'll select both of those options. Next we choose the security group for our new instances. 
# __
![[Pasted image 20230708175526.png]]
We'll use the same security group you created earlier in the course, the web security group. 
# __
![[Pasted image 20230708175619.png]]
Then we scroll down and expand the advanced details selection. Here we'll choose our instance role, the same role we used previously in the instance profile dropdown. 
# __
![[Pasted image 20230708175730.png]]
Once we do that, we'll scroll all the way down and paste our user data. This is what grabs our source code and unzips it so that our application runs on EC2. Now we're done and we can click create. 
# __
![[Pasted image 20230708175844.png]]
Now that we've configured our launch template which again defines what we launch, we now have to define an auto-scaling group which tells us where, when and how many instances to launch. 
# __
![[Pasted image 20230708180020.png]]
To create an autoscaling group, we'll select autoscaling groups on the side panel and then create an autoscaling group.
# __
![[Pasted image 20230708180055.png]]
Here, we'll enter a name such as app-asg and then select the launch template we just created app launch template and then click next. 
# __
![[Pasted image 20230708180240.png]]
Then we'll select our network. We'll choose the same VPC we created earlier in the course. 
# __
![[Pasted image 20230708180515.png]]
App-vpc and select both the private subnets we created, 
![[Pasted image 20230708180555.png]]
Private A and private B 
![[Pasted image 20230708180636.png]]and then click next. 
# __
![[Pasted image 20230708180711.png]]
We then need to select attached to an existing load balancer to receive traffic from the load balancer we created earlier 
![[Pasted image 20230708180737.png]]
and then choose our target group, at Target group. 
# __
![[Pasted image 20230708180833.png]]
Click enable ELB health checks so that the load balancer will check if your instances are healthy 
![[Pasted image 20230708180957.png]]
and then click next. 
# __
![[Pasted image 20230708181708.png]]
Now, we'll choose the maximum minimum and desired capacity. The minimum we'll say is two. This means that our auto-scaling group will always have at least two instances, one in each availability zone. The maximum will say is four, which means that our fleet can scale up to four instances. And the desired capacity, which is the number of instances you want to be running, we'll say is two. 
# __
![[Pasted image 20230708181923.png]]
Next, we can configure the auto-scaling policies. With scaling policies, you define how to scale the capacity of your auto-scaling group in response to changing demand. For example, you could set up a scaling policy with CloudWatch that whenever your instant CPU utilization or any other metric that you'd like reaches a certain limit, you can deploy more EC2 instances to your auto-scaling group. So what we want to do is use target scaling policies to adjust the capacity of this group. Earlier, Morgan created a CloudWatch alarm that resulted in the action of sending out an email. Here we're going to create a target tracking policy, much like Morgan created the alarm, but this time it will result in the action of triggering an auto-scaling event. So we'll name this CPU utilization and then we'll say that we want to add a new instance to our fleet whenever the target value is 60%. We'll also keep the instances need setting at 300 seconds to warm up before scaling. 
![[Pasted image 20230708182101.png]]
Then we'll click next to configure notifications when a scaling event happens. 
# __
![[Pasted image 20230708182245.png]]
This is optional, so for now we're going to skip past it. 
# __
![[Pasted image 20230708182300.png]]
All right, here we can review and click create autoscaling group. 
# __
![[Pasted image 20230708182628.png]]
Now all that's left is to stress our application and make sure that it actually scales up to meet the demand. 
# __
![[Pasted image 20230708182657.png]]
To do that, I'll open up a new tab and paste the endpoint for our elastic load balancer. Here's our application. I'm going to go to the info page by app pending/info on the URL. You'll notice here that we built in a stress CPU feature. This is going to mimic the load coming into our servers. In the real world, you would probably use a load testing tool, but instead we built a stress CPU button as a quick and easy way to test this out. Then we can watch our servers scale with that auto-scaling policy. So as the CPU utilization goes up, our auto-scaling policy will be triggered and our server groups will grow in size. I'm going to select 10 minutes for our stress test. All right, some time has passed. We've stressed our application, and if we take a look at CloudWatch, we can see what happened. 
# __
![[Pasted image 20230708182752.png]]
So let's click on CloudWatch. 
# __
![[Pasted image 20230708182820.png]]
If you look here, we can see our alarm summary. We went over 60% CPU utilization across instances. That was our threshold, so we launched new instances. We launched two new instances into our autoscaling group. Then you can see the loads start to come down. Because we've launched more instances into our autoscaling group, there were more hosts to accept traffic for our elastic load balancer and the average CPU utilization went down across servers. All right, let's go look at the EC2 instances that were launched into the autoscaling group.
# __
![[Pasted image 20230708182940.png]]
I'm going to go to the EC2 dashboard. 
# __
![[Pasted image 20230708183035.png]]
From here, I'm going to scroll down to target groups and select the app target group.
# __
![[Pasted image 20230708183222.png]]
I'm going to select targets, and we can now see that we have four healthy target instances in our auto-scaling group. 
# __
So now we have an environment with an auto-scaling group and our launch template. We've set up an alarm in CloudWatch that whenever our CPU utilization goes over 60%, we're going to launch more instances into that group. 
# __
All right, and this app should be able to scale now using EC2 Auto Scaling. - Great. Thank you, Seth. All right. Now if we wait around long enough, what we would see is as the CPU load dropped off then one by one they would each get terminated because we no longer need them. Bringing our state all the way back down to the basic two we need, the minimum number for this particular group. All of that done without any human interaction. If for some reason you are doing this in your AWS account, don't forget to delete the autoscaling group instead of the instances. Otherwise, guess what will happen? The autoscaling group will spin up more instances to replace the ones that were deleted. So ensure you are deleting the auto-scaling group as well.