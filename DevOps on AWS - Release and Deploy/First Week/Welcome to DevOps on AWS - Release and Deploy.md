When you hear that your code is getting deployed, how does that usually make you feel? Anxious, sweaty, excited, maybe all of the above? Well, these nerves might be partially caused by the way your organization is doing deployments. It may be a very brittle process, prone to errors, and you might always feel certain that something will go wrong.
# __
In this course, we talk about how to improve the deployment process with DevOps methodology, and also some tools that might make deployments easier, such as infrastructure as code, or IAC, and AWS CodeDeploy.
# __
![[Pasted image 20230708234230.png]]
But to do this, it's important that you have some background experience or knowledge on source control and continuous integration. We discussed this largely in the previous course, Code, Build, Test. In that course, we discussed continuous integration, and we left off with a scenario that looks a little like this. You've written code and tests for the critical parts of your application, and you have somewhere to put this code. In this case, a CodeCommit repository, as well as a strong branching strategy. You also have a CI service--in this case, CodeBuild-- that monitors the repository and runs tests automatically for every commit that is pushed. Also, you learned how to deploy a serverless application. In summary, you have a pipeline that has built and tested your code, and you've deployed from your local environment manually. We'll take the scenario a step further in this course, where we'll orchestrates automatic deployments. Since we focused on a serverless app last time, we'll be mixing it up and deploying to Amazon Elastic Compute Cloud, or Amazon EC2 instances instead, so you'll be familiar with both compute platforms. By the end of the course, you'll be able to answer the question: How do we actually get our features out to production in an automated and safe way?
# __
To help me out, we have Russ Sayers from the previous course here to break down some of the deployment-related topics, and also my friend, Raf Lopes, who will guide us through infrastructure as code. Raf will also be leading the third course in the series. So, stay tuned for more Release and Deploy content. From all of us here at AWS, we hope you learn something, and most of all, we hope you have fun. Thanks, and see you soon.