Let's talk about AWS services you can use to add instruments to your cloud environment. In this video, I will talk about Amazon CloudWatch, what it is, what it does, and what are the core components. 
# __
![[Pasted image 20230708204346.png]]
Amazon CloudWatch is a suite for cloud resources and applications. It gives you the instruments to see what's going on, and it can notify you when something doesn't look right. The core components of CloudWatch are metrics, alarms, and logs. Let's talk about the metrics first. CloudWatch metrics are data points collected over time. Some managed AWS services send metrics automatically to CloudWatch, like EC2 instances, for example. If you run an EC2 instance, you can expect to have metrics for CPU utilization, network packets in and out, and some other metrics. Most managed AWS services send metrics to CloudWatch automatically, such as Amazon SQS, Elastic Load Balancing, Amazon RDS, API Gateway, AWS Lambda, and many, many, many others. You can also have custom metrics by doing API calls to the service. So, you can use CloudWatch to collect metrics from things that are not sensed by default, such as the number of connected users and business-logic metrics. We will cover custom metrics in another video, so let's stick with the default metrics for now. 
# __
![[Pasted image 20230708204507.png]]
For example, if you want to see data about the duration of a specific Lambda function, 
![[Pasted image 20230708204526.png]]
you can go to the CloudWatch console, select Lambda as the service, 
![[Pasted image 20230708204539.png]]
sort By Function Name, 
![[Pasted image 20230708204552.png]]
select the function, and simply hit the box, Duration. 
![[Pasted image 20230708204620.png]]
You will see a line chart.
# __
![[Pasted image 20230708204641.png]]
You can also also check multiple metrics at the same time, and see all of them in the same graph, such as duration from multiple Lambda functions. If you have a CI/CD in place, and you were working with CloudFormation to deploy identical environments, a good idea is to compare the amount of time across functions on different stages, like dev, test, and prod. 
# __
Good architectures have excellent metrics regardless of the scale. So, speaking about good practice, have you heard the term, "If you see something, say something"? In CloudWatch, you can specify an alarm that triggers an action if something doesn't look right. This alarm gets enabled when values from metrics hit a specific threshold for a specific time. Introducing CloudWatch alarms. 
# __
![[Pasted image 20230708204744.png]]
The thing is, what threshold should I put for the alarm? What number? Well, if there are two things that are hard for a DevOps person, it is naming variables and choosing thresholds for what is considered good or bad. So, why not let the machine decide? If you want CloudWatch to take a look at your metric and define the thresholds for you, you can use a feature called CloudWatch anomaly detection. CloudWatch anomaly detection uses machine learning algorithms that continuously analyze metrics off systems and applications, determine normal baselines, and surface anomalies with minimal user intervention. It may look complicated, but look how easy it is to use it. Here is a function that stores items into DynamoDB. It's a core function in an app I made. The app itself is not relevant, so let's focus on the CloudWatch part. Here, I would like to set an alarm if there is a spike in the duration of the Lambda execution, indicating that potentially there is something wrong. We can click on the function's name, then select graphed metrics for that function, and then click on that little icon to enable anomaly detection for that metric. Some magic happens, look.
You can see the expected values. 
# __
In my case, it was quick because I already have the ML model trained. If you're doing this for the first time, this gray threshold may take some minutes to be created. Here, we can see an algorithm defining thresholds for us, based on min and max values. To create an alarm for that, simply click the bell icon to create the alarm and choose Anomaly detection to use the band as a threshold, click Next, and then choose the alarm action, which can be an Auto Scaling action, an EC2 action, a notification to an SNS topic, or a Systems Manager action, which I will talk about next week.
# __
Oh, don't worry. I used the AWS Management Console for that just to illustrate the feature. Of course, you can set up all that programmatically.
Last, but not least, CloudWatch Logs. CloudWatch Logs is another core components of this service. It allows you to centralize log files from all your systems, applications, and everything you want. Once you have your logs in there, you can basically teach CloudWatch how to parse the log lines and populate metrics out of specific fields of the text. And once you have a metric, you can use anomaly detection and create alarms.
# __
If you're running applications on EC2 instances, you can use the CloudWatch agent to push log files to CloudWatch. If you're using Lambda functions, API Gateway, or any other AWS managed service like CodeBuild, the integration and the logs are already there. All you need to do is use it. For example, if you do a print or console.log statements inside your Lambda function, that output will end up showing in the CloudWatch Logs logstream for that Lambda function.
That's it! I hope that this video gave you a good idea about how to better understand what CloudWatch is. Don't forget to read the course notes. I will put some more detailed information in there regarding anomaly detection, which is a pretty interesting feature. There is a big trend on applying machine learning capabilities to DevOps components, and anomaly detection is a very easy way to achieve it.
# __
![[index (2).mp4]]