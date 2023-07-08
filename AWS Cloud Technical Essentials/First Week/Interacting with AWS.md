 When you own the infrastructure it's easy to understand how you interact with it because you can see it, touch it and work with it on every level. If I have a server that I've stood up in my closet, interacting with that server is easy because it's mine. I can touch it. When I remove the ability for me to touch and see something like when the infrastructure becomes virtual, the way that I work with that infrastructure has to change a bit. Instead of physically managing my infrastructure, now I logically manage it through the AWS Application Program Interface or API. So now when I create, delete or change any AWS resource 
whether it's a virtual server or a storage system for employee photos, I use API calls to AWS to do that.
# __
![[Pasted image 20230628231327.png]]
You can make these API calls in several ways but the three main ways we're going to talk about in AWS are the AWS Management Console, the AWS Command Line Interface and the AWS Software Development Kits or SDKs.
# __
When people are first getting started with AWS, they typically use the AWS Management Console. This is a web-based method that you log into from your browser. The great thing about the console is that you can point and click. By simply clicking and following prompts, you can get started with some of these services without any previous knowledge of the service. With the console, there's no need to worry about scripting or finding the proper syntax.
# __
![[Pasted image 20230628231554.png]]
![[Pasted image 20230628231620.png]]
When you log into the console, the landing page will show you services you've recently worked with but you can also choose to view all of the possible services organized into relevant categories such as compute, database storage, and more. If I change the region to Paris, you're making requests to eu-west-3.console.aws.amazon.com or the Paris Region's web console. After you work with the console for a while, 
you may want to move away from the manual creation of resources. For example, in the console, you have to go through multiple screens to set configurations to create a virtual machine. And if I wanted to create a second virtual machine I would need to go through that process all over again. While this is helpful, it also leaves room for human error. I could easily miss a checkbox or misspell something or even skip important settings by accident. So when you get more familiar with AWS, or if you're working in a production environment that requires a degree of risk management, you should move to a tool that enables you to script or program these API calls. One of these tools is called the AWS Command Line Interface or CLI. You can use this tool in a couple of ways. One is to download the tool and then use the terminal on your machine to create and configure AWS services. Another is to access the CLI through the use of AWS Cloud Shell, which can be done through the console. With both of these options, instead of having a GUI like the console to interact with, you run, create commands using a defined AWS syntax.
# __
![[Pasted image 20230628231756.png]]
For example, if I wanted to launch a virtual machine with the CLI through Cloud Shell, I first used this quick shortcut to open a session. Once my session is started, I type in AWS which is how we know we interact with the API, then type in the service. In this case, it's EC2, the service that allows us to create and manage virtual machines, which we'll learn about later. And then the command that we want to perform in that service and any other configurations we want to set.
# __
One command versus multiple screens you have to click through in the console can help reduce accidental human errors. But that also means you have to work with defined syntax and get that syntax correct in order for your command to run successfully. So there is some upfront cost in just understanding how to form commands, but after a while, you can begin to script these commands out, making them repeatable which can greatly improve efficiency in the long run. The other tool that allows you to interact with the AWS API programmatically is the AWS Software Development Kits or SDKs. SDKs are created and maintained by AWS for the most popular programming languages such as Python, Java, Node.js, .NET, Ruby, and more. This comes in handy when you want to integrate your application source code with AWS services. For example our employee directory application runs using Python and Flask. 
If I wanted to store all of the employee photos including pictures of employees in an AWS storage service, I could use the Python SDK to write code to interact with that AWS storage service. The ability of managing AWS services from a place where you can run source code with conditions, loops, arrays, lists and other programming elements provides a lot of power and creativity. Alright, that wraps this video up. To recap, you have three main options to connect with AWS, the Console, the CLI, and the SDKs.
# __
In this course we'll mainly be using the console to interact with the services but feel free to challenge yourself by using the CLI if you're a bit more advanced.