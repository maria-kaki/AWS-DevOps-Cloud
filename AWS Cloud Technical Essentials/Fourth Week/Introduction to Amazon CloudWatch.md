In this video, I'm gonna run through some of the features that Amazon CloudWatch has to offer. We've already deployed resources into our AWS account with the employee directory application, so to get a handle on what CloudWatch is and how it works, let's dive into the AWS console and see what we can see.
# __
The end goal of this demo is to set up a dashboard that shows us the CPU utilization of the EC2 instance over time and set an alert that will be sent out if the CPU utilization of the instance goes over 60% for a period of time. 
# __
![[Pasted image 20230707203011.png]]
I'm already in the console and I will navigate to Amazon CloudWatch. 
# __
![[Pasted image 20230707203025.png]]
A lot of the AWS services begin reporting metrics to CloudWatch automatically when you create resources. Let's explore what types of metrics are available from the resources that we have already created in a previous lesson.  
# __
![[Pasted image 20230707203120.png]]
To do that, let's first create a dashboard. A dashboard in CloudWatch is a customizable page in the console that you can use to monitor your different types of resources in a single view. This includes resources that are spread across different AWS regions. I want to create a dashboard that shows me the CPU utilization over time for the EC2 instance hosting the employee directory application. 
# __
![[Pasted image 20230707203222.png]]
So now I'm going to click dashboards in the left-hand navigation and then click create a dashboard and we can then name this dashboard mydashboard. AWS resources automatically send metrics to CloudWatch and it's built into the service. 
# __
![[Pasted image 20230707203300.png]]
I'm going to select which widget we can add to the dashboard, 
![[Pasted image 20230707203322.png]]
and I will select a line graph here.
# __
![[Pasted image 20230707204343.png]]
Next, we can take a look at what the data source will be for this widget, and I will select metric for this. 
# __
![[Pasted image 20230707204406.png]]
Now we can browse through all of the available metrics. This is organized by service, so I will find EC2. 
# __
![[Pasted image 20230707204421.png]]
I will select EC2, and then I want to view per instance metrics. 
# __
![[Pasted image 20230707204445.png]]
From here, I can scroll through the different EC2-specific metrics that are being reported to CloudWatch and I want to select CPU utilization. 
# __
![[Pasted image 20230707204509.png]]
Click save, and now we are brought back to the dashboard with one line graph for one specific instance's CPU utilization. This gives us visibility into one aspect of the health of our EC2 instance. 
# __
You can explore in your own account what other metrics are available for you through CloudWatch by default but you can also report some custom metrics to CloudWatch programmatically. This is good to know because with EC2 and CloudWatch, you only get visibility into the health of the instance by default, which doesn't really give you a holistic picture of the health of your application. 
# __
The application running on the instance might not be operating correctly, but the CPU utilization could be fine. So keep in mind that you may choose to use custom metrics to get a more detailed and accurate view of the health in these dashboards. Once a dashboard is created, you can then share it with your team members. Now let's move on to another feature of CloudWatch called Amazon CloudWatch alarms. CloudWatch alarms allow you to create thresholds for the metrics you're monitoring, and these thresholds can define normal boundaries for the values of the metrics. If a metric crosses a boundary for a period of time, the alarm would be triggered, and then you can take a couple of different automated actions after an alarm is triggered. In our use case, I want to notify someone if the CPU utilization spikes over 70% for a period of time, say five minutes. Let's create an alarm to do that. 
# __
![[Pasted image 20230707204646.png]]
Let's navigate to the Alarm section and click Create alarm. 
# __
![[Pasted image 20230707204712.png]]
Now, what I want to do is create an alarm for CPU utilization, so I will select metric, 
![[Pasted image 20230707204732.png]]
click on EC2, 
![[Pasted image 20230707204746.png]]
per instance metrics 
![[Pasted image 20230707204801.png]]
and scroll down to select CPU utilization. 
# __
![[Pasted image 20230707204818.png]]
Now I will select the time period we are monitoring to trigger the alarm, which in this case is five minutes. You want to make sure you pick a reasonable time period where you don't wait too long to respond but you also don't respond to every short-lived uptick in CPU utilization. There is a balance to strike here and it will be highly dependent on your specific situation and your desired outcome. 
# __
![[Pasted image 20230707204910.png]]
Okay, so now we'll scroll down and type in 70 for the static threshold, which we are watching for, which is representing the CPU utilization threshold. If it goes over 70% for more than five minutes, it's likely that there's a problem, 
![[Pasted image 20230707204945.png]]
and now we will configure the action that will be taken if the metric triggers the alarm. 
# __
![[Pasted image 20230707205008.png]]
For CloudWatch alarms, there are three states an alarm can be in: either an ALARM, OK, or INSUFFICIENT_DATA. An alarm can trigger an action when it transitions between these three states. 
# __
![[Pasted image 20230707205104.png]]
In our case, I want to have this send out an alert to an email address when it transitions from OK to an alarm. AWS has a service called Amazon Simple Notification Service, or SNS, which allows you to create a topic and then send out messages to subscribers of the topic. You can imagine a scenario where we have systems admins or developers on call for our employee directory application and if something goes wrong, we want to send them an email paging them, letting them know that something is going wrong with the app. 
# __
![[Pasted image 20230707205140.png]]
So we will select create a new SNS topic since we do not have one in place already. 
# __
![[Pasted image 20230707205211.png]]
Name it CPU_Utilization_Topic, and then I will put in an email address here to receive the alert. Notice as I scroll down here that there are other actions you can take for a CloudWatch alarm. We will talk more about some of these options in upcoming lessons. 
# __
![[Pasted image 20230707205249.png]]
So then click Next 
![[Pasted image 20230707205316.png]]
and give this a name and description.
# __

![[Pasted image 20230707205354.png]]
And finally, click Create alarm. 
# __
![[Pasted image 20230707205421.png]]
It will take some time for the alarm to begin collecting enough information to leave the insufficient data state and transition into the OK state. 
# __
That is it for now. We will continue to use CloudWatch in upcoming lessons to make our solution elastic through EC2 auto scaling.