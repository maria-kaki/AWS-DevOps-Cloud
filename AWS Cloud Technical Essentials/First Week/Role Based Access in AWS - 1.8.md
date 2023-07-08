Throughout these last few lessons, there have been sprinklings of IAM best practices. It’s helpful to have a brief summary of some of the most important IAM best practices you need to be familiar with before building out solutions on AWS.

LOCK DOWN THE AWS ROOT USER

![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/ScyhjY0FQDOtOVP68EDjzA_296d49447c8a42e5b2bc175d08d84ef1_image.png?expiry=1688169600000&hmac=KEHJLaOqvlrWb_khQlwBkalxwR42AruzSh-0Yvz6DhU)

The root user is an all-powerful and all-knowing identity within your AWS account. If a malicious user were to gain control of root-user credentials, they would be able to access every resource within your account, including personal and billing information. To lock down the root user:

- Don’t share the credentials associated with the root user.
    
- Consider deleting the root user access keys.
    
- Enable MFA on the root account.
    

FOLLOW THE PRINCIPLE OF LEAST PRIVILEGE

![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/NQQo_P0mQyaIOj-iZmNiTA_fb2e6b772598441c8c13049c8c810ff1_image.png?expiry=1688169600000&hmac=DJDqyV1Q9-XUkOZwwkqSAG63jqgCLzzVOnG7AA_SQts)

Least privilege is a standard security principle that advises you to grant only the necessary permissions to do a particular job and nothing more. To implement least privilege for access control, start with the minimum set of permissions in an IAM policy and then grant additional permissions as necessary for a user, group, or role.

USE IAM APPROPRIATELY

IAM is used to secure access to your AWS account and resources. It simply provides a way to create and manage users, groups, and roles to access resources within a single AWS account. IAM is **not** used for website authentication and authorization, such as providing users of a website with sign-in and sign-up functionality. IAM also does **not** support security controls for protecting operating systems and networks.

USE IAM ROLES WHEN POSSIBLE

![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/0xwJK2GtR9qQVwUNvdz6kQ_cb1a68790784423ba0029d3c99dd74f1_image.png?expiry=1688169600000&hmac=S4d5aaP9KuJcGRYRH57zzVkKNYGzRjUEWwCXqte8PQM)

Maintaining roles is easier than maintaining users. When you assume a role, IAM dynamically provides temporary credentials that expire after a defined period of time, between 15 minutes and 36 hours. Users, on the other hand, have long-term credentials in the form of user name and password combinations or a set of access keys.User access keys only expire when you or the admin of your account rotates these keys. User login credentials expire if you have applied a password policy to your account that forces users to rotate their passwords.

CONSIDER USING AN IDENTITY PROVIDER

If you decide to make your cat photo application into a business and begin to have more than a handful of people working on it, consider managing employee identity information through an identity provider (IdP). Using an IdP, whether it be an AWS service such as AWS IAM Identity Center (Successor to AWS Single Sign-On) or a third-party identity provider, provides you a single source of truth for all identities in your organization.You no longer have to create separate IAM users in AWS. You can instead use IAM roles to provide permissions to identities that are federated from your IdP.For example, you have an employee, Martha, that has access to multiple AWS accounts. Instead of creating and managing multiple IAM users named Martha in each of those AWS accounts, you can manage Martha in your company’s IdP. If Martha moves within the company or leaves the company, Martha can be updated in the IdP, rather than in every AWS account you have.

CONSIDER AWS IAM IDENTITY CENTER

![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/AjcGd3TOR3W41EL_x7kkyA_022440022d3540be9aec26fefc9523f1_image.png?expiry=1688169600000&hmac=rwvqflVqfDxinS_V1Mn5YF0B8S6Ki2H0751SzVizMyA)

If you have an organization that spans many employees and multiple AWS accounts, you may want your employees to sign in with a single credential.AWS IAM Identity Center is an IdP that lets your users sign in to a user portal with a single set of credentials. It then provides them access to all their assigned accounts and applications in one central location.AWS IAM Identity Center is similar to IAM, in that it offers a directory where you can create users, organize them in groups, and set permissions across those groups, and grant access to AWS resources. However, AWS IAM Identity Center has some advantages over IAM. For example, if you’re using a third-party IdP, you can sync your users and groups to AWS IAM Identity Center.This removes the burden of having to re-create users that already exist elsewhere, and it enables you to manage those users from your IdP. More importantly, AWS IAM Identity Center separates the duties between your IdP and AWS, ensuring that your cloud access management is not inside or dependent on your IdP.