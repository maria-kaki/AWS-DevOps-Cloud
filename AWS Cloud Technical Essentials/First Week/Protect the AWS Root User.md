When you create an AWS account, you sign up with an email address and you create a password. The email address you sign up with becomes the root user of the AWS account. This root user has unrestricted access to everything in your account in most cases. We will discuss in a later lesson what types of users can be restricted and how to do that. But for now, I want you to understand that when you log into your AWS account using an email address and password, it means you are logging in as the root user. This root user can do whatever they want in the account. It has all of the powers that can be had. And with great power comes great responsibility, or something like that. So knowing that the root user is all powerful, you should do everything you can do to make sure that no one can gain access to this root user. Let's say there's a nefarious actor of sorts, and they have an evil plan to log into your AWS account with your root user, gaining access to all of the powers and permissions. And they go and delete all of your valuable data and AWS resources, and in their place, they spin up a lovely and expensive cryptocurrency mining operation. Leaving you with the bill and none of your data as they walk away with a full crypto wallet. Sounds less than ideal. Well, how can you prevent that from happening? You could, of course, create a hard-to-crack password, and that will give you some level of security. This, however, is an example of single factor authentication where all someone needs to do is match the password with the email address, and boom, they're in. We recommend as a best practice that right after you create your AWS account, you enable multi-factor authentication, or MFA, on the root user. MFA introduces an additional unique piece of information that you need to enter to gain access to the account. There are a variety of devices, virtual or physical, that generate one-time passwords that can be integrated with your AWS account for MFA. For example, I personally use a virtual MFA device that is an app on my phone. This app produces a string of numbers for one time use that I type into the console after I log in using my email address and password. Even if someone guessed the password, they cannot gain access to the account without the numbers generated by the virtual MFA device. No matter what type of MFA device that you choose to use, and I will include a link to the supported devices and the readings for you to look into, the most important thing is that you are using MFA on the root user. That way, even if someone, the nefarious actor, cracks your password, they still cannot gain access to your account. All thanks to MFA. On top of enabling MFA for the root user, we strongly recommend that you do not use the root user for your everyday tasks, even the administrative ones. There are really only a few actions that require root user access. Coming up, you'll learn how to create an IAM user, and use that to log into your AWS account instead of using the root user.
# __