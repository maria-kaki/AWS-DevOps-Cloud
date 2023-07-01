![[Pasted image 20230629154710.png]]
We've already gone over the design of this application and what I want to focus on now is access control.
# __
![[Pasted image 20230629154818.png]]
There are multiple places on this diagram where we can identify the need for access control and credential management. The first being that we need to manage how users log in and use the employee directory application. We could require that people have a valid credential like a username and password to log into the app. That is access management on the application level. Then there is the fact that we know the code running the employee directory application on a virtual machine being hosted by the service Amazon EC2 and that code will need to make API calls to the object storage service Amazon S3 in order to read and write data like images for the employees. Well, here's the thing. Just because both Amazon EC2 and Amazon S3 have existing resources in this account, it doesn't mean that the API calls made from the code running on the EC2 instance to S3 are automatically allowed to be made.
# __
![[Pasted image 20230629154959.png]]
In fact, all API calls in AWS must be both signed and authenticated in order to be allowed, no matter if the resources live in the same account or not. The application code running on the Amazon EC2 instance needs access to credentials to make this signed API call to Amazon S3. So that's another place with a need for a credential and access management. Now let's take this a step further. How are you going to build out this architecture? Well, you'll need access to an AWS account through the use of a login. Your identity within this AWS account will need permissions to be able to do things like create this network, launch the EC2 instances and create the resources that will host and run the solution in AWS. Yet another place you need credentials.
# __
![[Pasted image 20230629160320.png]]
The root user which you have already learned about in a previous lesson has these permissions, but you don't want to be using the root user to administer your AWS resources. And let's assume you won't be the only one working on or building out this application. It's more likely that within one AWS account there would be many people who need access to build and support your solutions. You'll have different groups of people responsible for different parts of the architecture. The people who would write and deploy the code might be software developers, whereas the people who would be responsible for making changes to say the network would be a different group of people. You wouldn't and shouldn't give everyone who needs access to the AWS account, the root user credentials to log in. You instead would have unique credentials for each person logging in. This is where the service AWS identity and access management comes in. We identified three places where we will need access and credential management. AWS identity and access management or IAM can help take care of these two spots on the diagram. AWS IAM manages the login credentials and permissions to the AWS account and it also can manage the credentials used to sign API calls made to AWS services.
# __
![[Pasted image 20230629160550.png]]
IAM would not, however, be responsible for application level access management. The code running on this instance would use separate appropriate mechanisms for authenticating users into the application itself, not IAM.
# __
All right, so let's start with the AWS account level. IAM allows you to create users and each individual person who needs access to your AWS account would have their own unique IAM user. Creating users for everyone who needs access to the account, takes care of authentication. Authentication being verifying if someone is who they say they are because they had the proper credentials to log in. Now it's time to introduce authorization. Authorization is this. Let's say you've logged in and you are who you say you are. You've been authenticated. Now you want to create resources and manage AWS resources like create an Amazon EC2 instance for example. Sure, you've logged in but do you have the correct permissions to be able to complete that action? The idea that your permissions control what you can or cannot do is authorization. Are you authorized to launch an EC2 instance?
# __
![[Pasted image 20230629160953.png]]
IAM users take care of authentication and you can take care of authorization by attaching IAM policies to users in order to grant or deny permission to specific actions within an AWS account. Keep in mind when I say action here, I'm referring to an AWS API call. Everything in AWS is an API call.
# __
![[Pasted image 20230629161124.png]]
Everything in AWS is an API call. IAM policies are JSON-based documents. Let's take a look at an example. This IAM policy document contains permissions that allow the identity to which it's attached to perform any EC2-related action.
# __
![[Pasted image 20230629161248.png]]
The structure of an IAM policy has an Effect which is either allow or deny.
# __
![[Pasted image 20230629161336.png]]
And Action which is the AWS API call, in this case, we have ec2:* which includes all EC2-related actions.
# __
![[Pasted image 20230629161512.png]]
You can restrict this to be specific API calls. For example, I can restrict this action to be just run instances and then any user with this policy attached would only be allowed to run EC2 instances but perform no other EC2-related tasks.
# __
![[Pasted image 20230629161614.png]]
IAM lets you get very granular with your permissions in that way. Continuing with this example, we see the resource which allows you to restrict which AWS resources the actions are allowed to be performed against.
# __
![[Pasted image 20230629161734.png]]
You can also include conditions in your policies that can further restrict actions. IAM policies can also be attached to groups. IAM groups are very simply just groupings of IAM users.
# __
![[Pasted image 20230629162331.png]]
You can attach a policy to a specific user or a group. When you attach a policy to a group, any users that are a part of that group would inherit the permissions.
# __
We recommend that as a best practice you organize users into groups and assign permissions to groups instead of individual users where possible. This makes it easier to manage when people change job roles or multiple users need permissions applied or revoked. Another best practice to follow is that we recommend when you create your AWS account, you set up MFA for the root user. Then create an IAM user with admin permissions. Log out of the root user and then log in with the IAM user that you just created. From there, you can use this user to create the rest of the IAM groups users and policies. The reason we suggest you do this is because you cannot apply a policy to the root user but you can to an IAM user.
# __
![[Pasted image 20230629162723.png]]
Now that I've told you about IAM users, groups and policies, we've addressed this part of access management that we needed for our application but what about this part?
# __
![[Pasted image 20230629162831.png]]
The EC2 instance needs credentials to be able to make the signed API call two S3 for reading and writing employee images. Am I suggesting that you make an IAM user with a username and password for the application running on EC2 to use? No. No, I am not. This is where role-based access comes into the picture.
# __
![[Pasted image 20230629162919.png]]
Coming up we will learn about the temporary access that IAM roles provide and how it can apply to this use case here.