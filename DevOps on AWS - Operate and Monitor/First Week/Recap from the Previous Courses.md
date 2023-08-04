Thank you for joining us for Course 3 in our DevOps Series, focusing on Operate and Monitor. This reading provides a recap of the previous two courses that are in this series. Both courses focused on processes and practices you would use in a software development team.

## **1. DevOps on AWS: Code, Build, and Test**

The first course focused on the continuous integration aspects of the DevOps journey. This course covered the first three steps of the DevOps loop through lectures, demonstrations, and hand-on exercises about services like AWS CodeCommit, AWS CodeBuild, and AWS CodePipeline. Here is a brief explanation of each step:

![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/A0hysEuxR8OIcrBLsYfDxA_acd23d6686cd4ef2930aed26c45b8ff1_image-1-.png?expiry=1688947200000&hmac=DTohPHI4uh8ym5CXAt-BILE8z_dD3m9hrgV8FstgKQo)

### **Code**

[AWS CodeCommit](https://aws.amazon.com/codecommit/) is a secure, highly scalable, managed source control service that hosts private Git repositories. It makes it easy for teams to securely collaborate on code, with contributions encrypted in transit and at rest. CodeCommit reduces the need for you to manage your own source-control system or worry about scaling its infrastructure.

### **Build**

[AWS CodeBuild](https://aws.amazon.com/codebuild) is a fully managed continuous integration service that compiles source code, runs tests, and produces software packages that are ready to deploy. You don’t need to provision, manage, and scale your own build servers. CodeBuild scales near continuously and can process multiple builds concurrently.

### **Test**

[AWS CodePipeline](https://aws.amazon.com/codepipeline/) is a fully managed service that helps you automate your release pipelines for fast and reliable application and infrastructure updates so that you can deliver features and updates rapidly and reliably. For context, in the first course, CodePipeline was used to test the build before incrementing a continuous delivery pipeline.

## **2. DevOps on AWS: Release and Deploy**

The second course focused on infrastructure as code, and how to start evolving continuous integration into a continuous delivery model. With continuous delivery, you can push features into environments and manage infrastructure with the help of AWS CloudFormation.

![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/FhE8744JRpqRPO-OCTaaVg_a2c3085d0e5c491a9798f6fe9e3caef1_image-2-.png?expiry=1688947200000&hmac=2QhSpAKmq1sDpFMiVnsGws3Q4yT00ssbHDfIaemYSTk)

### **Release**

[AWS CloudFormation](https://aws.amazon.com/cloudformation/) gives you a way to model a collection of related AWS and third-party resources, provision them quickly and consistently, and manage them throughout their lifecycles by treating infrastructure as code.

### **Deploy**

[AWS CodeDeploy](https://aws.amazon.com/codedeploy/) automates code deployments to any instance, including Amazon Elastic Compute Cloud (Amazon EC2) instances and on-premises servers. AWS CodeDeploy makes it easier for you to rapidly release new features, helps you avoid downtime during application deployment, and handles the complexity of updating your applications. **Note**: The exercises on this course _do not_ build on the exercises you might have worked on in the previous two courses. If you didn’t complete the labs from the previous courses before starting this course, it isn’t a blocker on your DevOps journey!