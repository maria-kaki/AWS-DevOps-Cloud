![[index (17).mp4]]
Hi there, I'm Raf. In the previous videos, Alana started the conversation about continuous integration, and the AWS Services you can use to leverage a way to develop something in a collaborative manner, from the source code to build and test. She also talked about CodePipeline, the AWS service that can be used to orchestrate your continuous integration workflow, stitching together in CodeCommit and CodeBuild, to automatically have the build done, and tested according to the pushes in the Git repository. In this video, I am going to talk about the next steps, to move your pipeline to the next level, with the usage of infrastructure as code. Logging in the AWS Management Console and manually provisioning your environments is not ideal due to many reasons. It gets easier if you are the only one managing a simple environment in your personal account, but as you start working professionally with it, as a part of our DevOps team, it rapidly becomes more challenging. Automation is key, and infrastructure as code is the process of managing and provisioning environments through code in a declarative way. Let me ask Alana something, and you will understand what I mean by using the word declarative here, in the infrastructure-as-code context. Alana, I have something to ask you. What do you do when you go to a coffee shop, looking for an espresso? Option A. You ask the cashier, I would like to have an espresso please, or option B. You start giving detailed instructions to the barista, in terms of what they should do in order to get your espresso. Like, you start giving instructions like, getting the coffee beans, grinding with a specific granularity, tamper, put in the portafilter, turn on the machine for 25 seconds, et cetera.
# __
- [Alana] Well, if the barista is capable of making an espresso, I would definitely prefer option A. - [Raf] So do I, right? That's what I mean by using infrastructure as code, in a declarative way. The reason why I am saying all of this, is because since you can interact with AWS services programmatically, by using the AWS SDKs or the AWS CLI, you can create your infrastructure through shell scripts, although it gives you more control, because you are exactly specifying the very fine details, of what you want. It is way less convenient, because you also need to concern with complexity, such as managing changes, auditing, rollbacks, in case of failures, infrastructure, consistency, and much more.
# __
AWS CloudFormation is a service that allows you to declare your infrastructure in a text file. In that file, you say what you want, pass it to the service, and CloudFormation brews the coffee, I mean, the environment, for you. This file can be authored in JSON or YAML. Once you input a file and ask CloudFormation to create a stack, CloudFormation starts creating the infrastructure for you. In the CloudFormation nomenclature, we call that file a template, and infrastructure components, a stack.
# __
So, a template is something you define, and a stack is infrastructure that actually gets created. This is what a CloudFormation template looks like. The Resources part is where you declare what AWS services you want. If you want to create an S3 bucket, you can declare a resource of the type, AWS::S3::Bucket. The CloudFormation documentation has a list of the supported properties for every single AWS service that supports CloudFormation, which has almost every service. This is the documentation page for the resource AWS::S3::Bucket. I prefer using YAML because it's simple for me to read, and you can see that a bucket can be created simply by specifying the bucket name as a property.
# __
All right, a CloudFormation template can be as simple as that, just creating a bucket. Pretty simple. You can submit that to CloudFormation, and ask it to create a stack out of it. Once the stack finishes with no errors, you will have the bucket created, as declared in the template.
# __
Now, here comes one of the coolest part. What if, in addition to that S3 bucket, you also want to have a DynamoDB table? Pretty simple, you just edit the template, add the resource, AWS::DynamoDB::Table, and submit it again to CloudFormation. But this time, you will do an update stack operation.
# __
Update stacks are awesome. CloudFormation receives the updates from the template, and says: now, in addition to the bucket, the user wants a DynamoDB table. Let me create it, and voila. It updates the infrastructure for you. Same thing with deletions. If you want to remove something from your infrastructure, you can remove from the template and do an update stack. CloudFormation will calculate the delta, and make the infrastructure match what is desired on the template.
# __
- [Alana] But Raf, S3 buckets and DynamoDB tables may contain data from your users. What if you want to delete a stack, but retain some of the resources? Because when you delete a stack, CloudFormation will erase all the resources associated with the stack, and sometimes you want to erase some resources, but not others, right?
# __
- [Raf] That's right. When you delete a stack, CloudFormation erases every resource defined on that stack. And that's why some of the resources allow you to define an action when you delete this stack.
# __
For example, this S3 bucket has a deletion policy defined as Retain, which will make CloudFormation reserve that specific resource upon stack deletion. The usage of this is actually a best practice every time you define a resource that will be used as a database, like an RDS instance, an Elasticsearch cluster, or a DynamoDB table.
# __
CloudFormation is very powerful. We could spend hours and hours talking about its features, but we have to move on in our DevOps journey. So I strongly recommend you taking a look at the CloudFormation documentation. Having the ability to write a template and have the infrastructure created is super powerful.
# __
Since we are talking about having a CI/CD pipeline, you can have CloudFormation templates, in a CodeCommit repository, and whenever you do a push with a change, CodePipeline orchestrates the environment change by executing an update stack as part of the deployment. When we start doing this practice, we have developers operating the infrastructure, and this is actually where the word DevOps come from, developers who also operate. And because developers are good with code, when we talk about infrastructure as code, developers are the expert.