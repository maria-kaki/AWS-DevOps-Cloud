![[index (18).mp4]]
As Raf and I mentioned earlier, a pipeline is also programmable infrastructure. For example, take CodeDeploy. In Exercise 2 of the course, you created an application and a deployment group in the console manually. While you were doing that, I created an application and deployment group in a CloudFormation template. Here's what it looks like. We have our application declared at the top of the screen, here. We gave it a name and we also determined that we're deploying to Amazon EC2 as our compute platform. So overall, six lines of code to declare this resource. Not bad. If I scroll down, you can also see my deployment group and all of its properties. So, not only do we have the name of the deployment group, which application it belongs to, our configuration settings, and the deployment style, we also declare which EC2 instance we'll be deploying to, in this case, the instance that's tagged as CodePipelineBlog. And you can also see that it references the application, so that means when I run this template through the CloudFormation console, CloudFormation won't build the deployment group until after it builds the application. This makes sense because we need an application before we can create a deployment group. I also, in the same template, created a service role for CodeDeploy and an EC2 instance that has the CodeDeploy agents installed. So basically, everything you did in Exercise 1 and 2 is now in this one template.
Reproduza o vídeo começando em :1:35 e siga a transcrição1:35
To build off of all that, I also created all the other components of a pipeline, including CodeCommit and CodeBuild. And then, I created a code pipeline
Reproduza o vídeo começando em :1:46 e siga a transcrição1:46
with a source stage,
Reproduza o vídeo começando em :1:50 e siga a transcrição1:50
a deploy stage, and an acceptance test stage.
Reproduza o vídeo começando em :1:56 e siga a transcrição1:56
So, let's see this run. I'll go to the AWS Management Console, search for CloudFormation,
Reproduza o vídeo começando em :2:7 e siga a transcrição2:07
click Create stack,
Reproduza o vídeo começando em :2:15 e siga a transcrição2:15
upload this template file called final_pipeline,
Reproduza o vídeo começando em :2:20 e siga a transcrição2:20
and click Next.
Reproduza o vídeo começando em :2:23 e siga a transcrição2:23
Here, I'll have to name the stack.
Reproduza o vídeo começando em :2:26 e siga a transcrição2:26
I'll call it final-pipeline-stack,
Reproduza o vídeo começando em :2:31 e siga a transcrição2:31
and then, I'll call the pipeline, final-pipeline.
Reproduza o vídeo começando em :2:39 e siga a transcrição2:39
So, I'll go ahead and keep all the other defaults, click Next, keep the defaults again, and Next again,
Reproduza o vídeo começando em :2:48 e siga a transcrição2:48
acknowledge that it might create IAM resources, and click Create stack.
Reproduza o vídeo começando em :2:55 e siga a transcrição2:55
However, I've already created this CloudFormation stack earlier to save us some waiting time, which is why we got this error here, so I'll go ahead and cancel out of this, and click on the stack that I created earlier to find all of its resources. All right, so this CloudFormation template has already been provisioned and everything looks good, and if I click on this Resources tab here, we can see all the resources that were created when I ran this template. So, let's jump over to our pipeline that was created by this template by going to the CodePipeline console.
Reproduza o vídeo começando em :3:28 e siga a transcrição3:28
As you can see, the pipeline has already started running, but here's what happened behind the scenes. If I go back to the template, when I wrote the code to create CodeCommit,
Reproduza o vídeo começando em :3:43 e siga a transcrição3:43
as you can see here, I chose to propagate the repo with code from an S3 bucket. So, the commit was made, which kicked off the deployment, which if I go back to the console, I can see has succeeded.
Reproduza o vídeo começando em :3:57 e siga a transcrição3:57
If I click on the Details and scroll down,
Reproduza o vídeo começando em :4:2 e siga a transcrição4:02
I can find that the instance that it deployed to is right here, so I'll go ahead and click it, which brings me to the EC2 console.
Reproduza o vídeo começando em :4:12 e siga a transcrição4:12
Select the instance, copy the public IP address, and paste it into my browser. And it looks like the deploy worked! My app is up and running.
Reproduza o vídeo começando em :4:24 e siga a transcrição4:24
Okay. let's go back to the pipeline and see the final stage, the acceptance test. All this test does is access the instance and check if it can access the landing page. If we click Details of this stage, we can look at the commands we ran in the buildspec
Reproduza o vídeo começando em :4:42 e siga a transcrição4:42
and the output of those commands. As you can see here, it pulls the HTML from our landing page and that's exactly what we wanted to accomplish, so everything looks good.
Reproduza o vídeo começando em :4:54 e siga a transcrição4:54
So that's how I automated a pipeline with CloudFormation. If you're looking for this template to download so you can try it yourself, I'll be providing it to you in Exercise 3 of the course, along with the buildspec file, the AppSpec file, and the app itself. Now, if I wanted to take it a step further, I could change the HTML file and commit it to my repo, kicking off the pipeline once again, and see my changes in real time, but you'll be doing that in the next exercise, so see you soon.
(Obrigatória)
