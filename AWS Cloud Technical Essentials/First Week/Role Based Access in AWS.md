All right, so you've learned about IAM users, groups, and policies. Policies can be applied to AWS identities like users and groups to assign permissions. They also, however, can be applied to another AWS identity, IAM roles. An IAM role is an identity that can be assumed by someone or something who needs temporary access to AWS credentials. Let's dive into what I mean when I say AWS credentials. Most AWS API calls that are made must be signed and authenticated, but how does that process work? When you send HTTP request to AWS you must sign the request. This signing process happens programmatically and allows AWS to verify your identity when a request is made and run through various security processes to ensure a request is legit. IAM users have associated credentials like an access key ID and secret access key that are used to sign requests.
# __
![[Pasted image 20230629171532.png]]
However, with regards to our architecture, the code running on the EC2 instance needs to sign the request sent to S3. I already told you that I don't intend for you to create an IAM user with credentials to be used by this app, so how will the application gain access to the needed AWS access key ID and AWS secret access key to sign the API call? The answer is IAM roles.
# __
IAM roles are identities in AWS that like an IAM user also have associated AWS credentials used to sign requests. However, IAM users have usernames and passwords as well as static credentials
![[Pasted image 20230629172410.png]]
whereas IAM roles do not have any login credentials like a username and password and the credentials used to sign requests are programmatically acquired, temporary in nature, and automatically rotated.
# __
![[Pasted image 20230629172547.png]]
In our example the EC2 instance will be assigned an IAM role.
![[Pasted image 20230629172649.png]]
This role can then be assumed by the application running on the virtual machine to gain access to its temporary credentials to sign the AWS API calls being made. A role can be assumed by many different identities and they have many use cases. The important thing to know about roles is that the credentials they provide expire and roles are assumed programmatically.To get an idea of this, let's create a role using the AWS console.
# __
###### **I'm already logged in and will navigate to the IAM service. Now I want to create the role the EC2 instance is going to use for the employee directory application. Now, we will click Roles in the left-hand side and select Create role. We will then select the trusted entity this role is intended to be used for, and in our case this will be EC2, then we will click Next. Now we get to select the permissions assigned to this role. Again, permissions being what actions does this identity have the authority to take? We want this identity to be able to read and write to Amazon S3, so I will search for S3 and you can see there are multiple options here for pre-written policies that I can choose from. I also can write my own custom policy which would also show up here if I created it ahead of time. I'm going to select S3 full access for the policy.**
# __
In the real world you would choose a more restrictive IAM policy for this but for a proof of concept like this course is intended to provide, we will leave the permissions a bit looser for now. You would come back and change the permissions, attach this role to be more granular if this were ever to make it to a production type environment.
# __
###### **Now we also need to add another permission here, and that's for DynamoDB. So I will exit out of the S3 filter and then type in DynamoDB and hit Enter. And then we will select the AmazonDynamoDBFullAccess permission. Then we will click Next. Then we can give this role a name, which is EmployeeWebAppRole. Then we can scroll down and we can click Create role. We can see that this role has now been created successfully and if we click on the role and scroll down, we can then see that this role has two permissions attached.**
# __
It's very common for roles to be used for access between AWS services. Just because two resources exist in the same AWS account, it doesn't mean that they can send any API calls to each other. If one AWS service needs to send an API call to another AWS service, it would most likely use role-based access where the AWS service assumes a role, gains access to contemporary credentials and then sends the API call to the other AWS services who then verifies the request.
# __
![[Pasted image 20230629182517.png]]
Another identity that can assume an IAM role to gain access to AWS is external identity providers. For example, let's say you have a business that employs 5,000 technical employees that all need access to AWS accounts. You already have an identity provider system in place that allows these employees to log into their laptops and gain access to various corporate resources. Should you also now go create 5,000 IAM users for these employees to access AWS? Well, that doesn't sound very efficient. You instead can leverage IAM roles to grant access to existing identities from your enterprise user directory.
# __
![[Pasted image 20230629182620.png]]
These are known as federated users. AWS assigns a role to a federated user when access is requested through an identity provider.
# __
![[Pasted image 20230629182733.png]]
We also have AWS services that can make this process easier such as AWS IAM Identity Center.
# __
These are a couple of examples of role-based access in AWS and this is just the introduction. Check out the class readings for more information and don't worry if you don't quite grasp this concept yet as we will continue using roles in our demos and examples throughout this course.
# __