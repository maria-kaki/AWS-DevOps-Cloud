![[index (3).mp4]]
So far, you have understood that monitoring is a very important part of the overall CI/CD pipeline. All of the monitoring concepts you have learned so far can be applied both to the application serving customers, and why not, to the CI/CD pipeline itself! In this video, I will approach the monitoring that can oversee multiple aspects of your architecture, starting with the CI/CD pipeline monitoring.
# __
Reproduza o vídeo começando em ::27 e siga a transcrição0:27
As part of previous courses in the DevOps series, you learned the components to push code into production by using AWS services to make it happen, like CodeCommit, CodeBuild, CodePipeline, and other AWS services in the DevOps area. In this video, I will be giving you examples on how to use two additional AWS services to monitor a CodePipeline from different perspectives. I will talk about Amazon EventBridge and AWS Config.
# __
Reproduza o vídeo começando em ::55 e siga a transcrição0:55
You can monitor CodePipeline events in Amazon EventBridge, which is a service used for delivering real-time data from your own solutions and AWS services. EventBridge calls events to targets, such as Lambda for code execution, and Amazon Simple Notification Service for notifications, and also even AWS Partner integrations. EventBridge was formally called CloudWatch Events. So, if you heard the name CloudWatch Events, you know it's the same thing.
# __
Reproduza o vídeo começando em :1:27 e siga a transcrição1:27
You know, when you have an IF statement in your code-- "if this, then that"--the thing is that, in order for the IF to satisfy a condition, it must have a comparison. It needs two things to compare to each other, and that's where EventBridge shines. As the name suggests, EventBridge allows you to take actions in response to an event. In the same way you would have an IF operator in a source code, think about a WHEN statement when thinking about EventBridge. With that in mind, it's now easier to know what AWS service to use if you want to get an alert, when a CodePipeline execution fails or succeeds.
# __
Reproduza o vídeo começando em :2:10 e siga a transcrição2:10
Check how easy it is: You just go Amazon EventBridge, click Create rule, choose a Name for the rule, select Events pattern, which is the WHEN logic, select Pre-defined pattern by service, choose AWS from the Service provider, then choose CodePipeline from the Service name. And note how many other AWS services support EventBridge.
# __
Reproduza o vídeo começando em :2:39 e siga a transcrição2:39
Now, choose CodePipeline Pipeline Execution State Change as the Events type. And then point FAILED as the Specific state. Notice that the Event pattern with JSON that gets populated on the right side changes as you click on the Options. Then scroll down and choose a Target, and look how many targets are available: You can queue a message into Amazon SQS or send a notification to an SNS topic, which could do an HTTP POST for a webhook, and post a message into a chat room or open a ticket. For example, if you trigger a Lambda function that fixes the issue, you can bring your pipeline into a self-healing state.
# __
Reproduza o vídeo começando em :3:25 e siga a transcrição3:25
Once you are done, just scroll down and click Create to create the rule.
# __
Reproduza o vídeo começando em :3:32 e siga a transcrição3:32
Ah, and of course, you can--and actually should--create these rules via CloudFormation by using the AWS::Events::Rule CloudFormation resource.
# __
Reproduza o vídeo começando em :3:43 e siga a transcrição3:43
A best practice is to create separate CloudFormation stacks, dedicated for monitoring features, and guess what? You can use a CodePipeline to orchestrate that in the same way you would use to orchestrate any other environment.
# __
Reproduza o vídeo começando em :3:58 e siga a transcrição3:58
All right, we explored a little bit of EventBridge, a service that gives you a WHEN capability in terms of doing something when something else happens. But there is another AWS service that I would like to talk about, which plays a key role in the infrastructure compliance. Introducing: AWS Config. AWS Config monitors administrative API activity, performed to your AWS account, and saves a delta between the configuration differences on how the infrastructure was before and after a specific API call. You can have the option of triggering a Lambda function to evaluate the infrastructure in terms of compliance after the change, and have that function respond back to Config to say if the infrastructure was left in a compliant or non-compliant state after the change. This is called an AWS Config rule.
# __
Reproduza o vídeo começando em :4:53 e siga a transcrição4:53
Think about the term infrastructure delta when thinking about AWS Config. So, if you want to monitor changes in the CodePipeline configuration, AWS Config can detect these API calls and calculate the difference. Now, if you want to monitor a pipeline stage change, like from running to failed, or from running to completed, and then do something when that happens, EventBridge is your way to go.
# __
Reproduza o vídeo começando em :5:20 e siga a transcrição5:20
To better clarify the difference, let me give you a practical example on how both Config and EventBridge can be used for pipeline monitoring from configuration to execution.
# __
Reproduza o vídeo começando em :5:33 e siga a transcrição5:33
If you want your pipelines to be tagged with specific tags, use AWS Config to monitor configuration changes and mark the pipeline as non-compliant if they're not properly tagged. If you want to take an action, such as sending an email to the DevOps team if a specific step of the pipeline fails, use an EventBridge rule to detect and dispatch a notification. Please let us know in the forums how you are using AWS Config and EventBridge as part of your monitoring.