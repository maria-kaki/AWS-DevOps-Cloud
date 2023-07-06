![[Pasted image 20230703115648.png]]
AWS Lambda is one of the serverless compute options you have available to you on AWS. Lambda allows you to package and upload your code to the Lambda service, creating what is called a Lambda function. Once you create a Lambda function, it isn't always running all of the time. 
# __
![[Pasted image 20230703115839.png]]
Instead, Lambda functions run in response to triggers. You can configure a trigger for when you want your function to run, and from there the Lambda service waits for the trigger or polls for an event to trigger the function depending on what the trigger is that you choose. 
# __
There's a long list of available triggers for AWS Lambda, and new ones are being supported all of the time, so I won't run through them all now. However, a couple of common examples of triggers for Lambda functions are an HTTP request, an upload of a file to the storage service Amazon S3, events originating from other AWS services, or even in-app activity from mobile devices. 
# __
![[Pasted image 20230703120020.png]]
When the trigger is detected, the code is automatically run in a managed environment, an environment that you do not need to worry too much about because it is automatically scalable, highly available, and all of the maintenance of the environment itself is done by AWS. You do, however, get to choose the language your Lambda function is coded in, the amount of memory and CPU your function is allocated in the environment, permissions, dependencies, and many other aspects of how the function runs. 
# __
![[Pasted image 20230703121415.png]]
If you have 1 or 1,000 incoming triggers AWS Lambda will scale your function to meet demand, each in its own isolated environment. Lambda is currently designed to run code that has a runtime of under 15 minutes. 
# __
![[Pasted image 20230703121445.png]]
So this isn't for long running processes like deep learning or batch jobs. You wouldn't host something like a WordPress site on AWS Lambda. It's more suited for quick processing like a web backend handling request, or a backend report processing service or microservice hosting.
# __
![[Pasted image 20230703121541.png]]
One of the best things about Lambda is that you aren't billed for code that isn't running. You only get billed for the resources that you use rounded up to the nearest one millisecond interval. 
# __
To understand Lambda more thoroughly, let's run through a quick demo. In this demo, I will create a Lambda function that resizes images uploaded into the employee directory to be uniform thumbnail size. It makes sense to create this sort of logic with a Lambda function. You don't need an application to be running 24/7 on EC2 to resize photos uploaded to the application. You really only need to run the resize logic when a new photo is uploaded. 
# __
![[Pasted image 20230703121744.png]]
So here's our diagram for the app.
# __
![[Pasted image 20230703121830.png]]
What I want to do here is when a new photo is uploaded to S3, it triggers a Lambda function that then resizes the image and uploads it into that same S3 bucket, but to a different location than where the original image is stored. 
# __
![[Pasted image 20230703121943.png]]
All right, let's go ahead and build this out. You can see that I'm already in the AWS Lambda console and I'm going to first click Create function. 
# __
![[Pasted image 20230703122236.png]]
Next, we get to select what type of function we want to build. Do we want to author a function from scratch? Do we want to use a blueprint which will give you some sample code and configuration presets? Or you can use a container image with AWS Lambda as Lambda does support running containers. We are going to author a function from scratch. 
# __
![[Pasted image 20230703122436.png]]
For the function name, we will call this ResizeImage, and then we get to select the runtime. The runtime is the language that your Lambda function is written in, because with Lambda, it runs in the Lambda environment, but it's still your code. So I'm gonna go ahead and select Python 3.9 for this as we wrote this function in Python. 
# __
![[Pasted image 20230703122720.png]]
And then we have to select the permissions. And the permissions are going to be delegated to the function through IAM roles. 
# __
![[Pasted image 20230703123003.png]]
So I'm gonna click Use an existing role, and then if I expand this dropdown, we can select LambdaS3FullAccess which is an IAM role that I've already created in this account that will give this function permissions to read and write from S3. Now we can scroll down and select Create function. 
# __
![[Pasted image 20230703123355.png]]
Now we can add a trigger for this Lambda function, and I'll select Add trigger. 
# __
![[Pasted image 20230703123924.png]]
And here we get to configure the trigger source, and if we expand this dropdown, you can see a list of AWS services that can act as triggers like API Gateway, an Application Load Balancer, DynamoDB. We're going to scroll down and select S3 for our trigger. 
# __
![[Pasted image 20230703124042.png]]
And then we need to select which S3 bucket will be the event source. I already have an S3 bucket created in this account called photo-upload-bucket-mw, we'll select that one. 
# __
![[Pasted image 20230703124119.png]]
And then if we scroll down, I'm going to select the event type. I want to select only a PUT, so I want PUT operations to trigger this AWS Lambda function. 
# __
![[Pasted image 20230703124606.png]]
Then we can provide a prefix. With this prefix, what we're essentially doing is we're going to say: I only want to trigger this Lambda function if a PUT occurs in a specific location inside of this bucket. We're going to upload photos to an input prefix and that will then trigger the Lambda function. We then need to acknowledge that if we're using the same S3 bucket for both input and output that it could cause recursive invocations. So the way that we're getting around that is by supplying this input prefix, the event will be triggered when an image is uploaded to this prefix, but then the output will actually be uploaded to a different location. We'll have an output prefix where the image will be uploaded to. So we're gonna go ahead and acknowledge by checking this checkbox and then click Add. 
# __
![[Pasted image 20230703125146.png]]
Now back on our Function overview page, what we need to do next is actually upload the code for this. 
# __
![[Pasted image 20230703125246.png]]
So if we scroll down, we can select the Code tab, and then you can see that there's a stubbed out Lambda function here that essentially just says, "Hello world, hello from Lambda." And what we need to do is upload our code. 
# __
![[Pasted image 20230703125330.png]]
![[Pasted image 20230703125434.png]]
So I'm going to click Upload from, and then select zip file. Click Upload, and then I will select this ResizeImage.zip, click Open, and then click Save.
# __
![[Pasted image 20230703125629.png]]
All right, our function has been successfully created. We have our trigger defined, and we have our code uploaded. What I want to do now is test this out by actually uploading an image to S3 and then viewing the output. So in the search bar, I'll type in S3 and then select S3. 
# __
![[Pasted image 20230703130845.png]]
Then from here we'll select the bucket
# __
![[Pasted image 20230703130925.png]]
![[Pasted image 20230703130959.png]]
and then we'll go into the input folder and then select Upload
# __
![[Pasted image 20230703131021.png]]
click Add files
# __
![[Pasted image 20230703131045.png]]
and then I'll upload Seph's image, and select Open
# __
![[Pasted image 20230703131111.png]]
and then Upload. 
# __
![[Pasted image 20230703131233.png]]
We can see that that upload was successful. So now if we go check, we should see the output with the thumbnail version of that image. 
# __
![[Pasted image 20230703131314.png]]
So now going back into our bucket, if we go up one level, we can now see that the output prefix has been created, so I'll select that
# __
![[Pasted image 20230703131402.png]]
and we can see that the thumbnail image was created.
# __
And that's it, that's how you create an AWS Lambda function. You could host the entire employee directory applications backend on Lambda with some refactoring, but I'm gonna go ahead and save that for a later conversation.
# __