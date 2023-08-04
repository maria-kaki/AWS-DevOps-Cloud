![[index (10).mp4]]
# __
In this video, I will highlight one of the most important features of Systems Manager, that can be used when you have a fleet of servers and want to run remote commands without having to connect on them, one by one.
# __
One of the core features of Systems Manager is the Run Command. With Run Command, you can remotely and securely manage configurations of your managed instances.
# __
A managed instance is any EC2 instance or on-premises server in your hybrid environment, that has been configured for Systems Manager. In other words, they have the SSM agents up and running, with proper credentials. You can use IAM roles for EC2 instances, or IAM credentials for on-premises servers. Run Command allows you to automate common administrative tasks, and perform one-time configuration changes at scale. You can use Run Command from the AWS Management Console, the AWS Command Line Interface--or the AWS CLI-- and AWS Tools for Windows PowerShell, or the AWS SDKs. Run Command is useful for running non-interactive commands remotely. Like adjusting all your instances' time zones, cleaning up old log files, or configuring logrotate to do so. You can do that all of that without having to connect over SSH, or messing up with bastion hosts.
# __
When you go to the Run Command screen on the AWS Management Console, you can see some blueprints, and get an idea of the possibilities. For example, there is one that does Windows updates, another one that configures Docker, another one that configures the CloudWatch agent, so on and so forth, the list is long. You can specify parameters for running the command, and also how and where you want that command to be run among your instances. We call them targets. These targets can be a group of instances with specific tags, manual instances, where you provide the instance ID, or resource groups, which is a collection of resources where you can manually add instances.
# __
You can add parameters to the command, allowing to input custom information that gets passed. You can also choose how you are going to roll it out. If it is gradually, one by one, a percent of your fleet, or all at the same time. If you want to install packages in your operating system, you can run a command to do so, using the specific package manager available in the OS. Or you can offload that to Run Command. There is option where you can declare what you want to install, and the Run Command takes care of the rest. So you don't need to know the specific package manager, such as apt or yum. This creates more maintenance resiliency, across the operation. For the sake of auditing, all these generate a trail, and because there are commands that can take longer to run, you can follow up the status by doing API calls to the service. There are also third-party solutions that can be used to operate. If that's the case, and you already have a solution, based on Chef, Puppet, or any other framework, you can use Run Command to install and configure the agents of your choice. In the hands-on exercise at the end of this week, you will have the chance to follow a guide that shows you how to use Run Command to troubleshoot ongoing issues, in a production server. Ah, and the best part, Run Command is offered at no additional cost.