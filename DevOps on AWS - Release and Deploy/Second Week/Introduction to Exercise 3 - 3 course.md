![[index (20).mp4]]
So, you're now ready for the next exercise. This is where we put all the pieces of what we learned together. If you took the first class in the series, you'll already be familiar with CodeCommit, CodeBuild, and CodePipeline, and in this course, you spent time learning about CodeDeploy and CloudFormation. So, if we're using all of these services, what could this lab possibly be about? Well, you might have already guessed it. You'll be automating the creation of an entire CI/CD pipeline. Here's how this will work. I'll provide you the template that I showed in the Automation of a Pipeline video. You'll upload this template to CloudFormation, and it will provision every piece of your pipeline, including CodeCommit, CodeBuild, and CodeDeploy. It will also kickstart your pipeline initially. Take a look at the template and try to understand each resource that gets created. You can also see some of the CloudFormation features that Raf mentioned earlier, such as the Parameters section.
# __
For example, one of the parameters is an AMI ID for the EC2 instance.
Reproduza o vídeo começando em :1:6 e siga a transcrição1:06
Instead of you specifying an Amazon Machine Image, or AMI ID, the template grabs the latest AMI ID from AWS Systems Manager Parameter Store, so you don't have to worry about choosing the wrong AMI.
Reproduza o vídeo começando em :1:21 e siga a transcrição1:21
After you provision the template, you'll look at the pipeline that CodePipeline created and check the output of the pipeline, which is the application on your EC2 instance, in this case, a website that shows a blog. The other output of the pipeline is your acceptance test. We've populated the CodeCommit repository with a buildspec that shows the acceptance tests we'll be performing on this application. I'll display that same file on screen. As you can see, we're getting the IP address of the server, using cURL to get data from that IP address, and the result we should get is the index.html page, when we go to look at the output of this test. That'll tell us that the website is reachable. From there, you'll make a change to the index.html file in the repository, which will kick off the pipeline once again. You'll then check the results of that pipeline by verifying the code on your instance was changed. Once again, feel free to post in the forums if you run into any issues. All right, let's get started with Exercise 3.