## What Is Amazon EC2?

![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/J8AK7AJ5Rd-CJYWBoshBqg_cb704f22a39746e398bff9b1838c91f1_image.png?expiry=1688342400000&hmac=UHwyRFvQxhjYdJoneiPler1CBCHtl_ElI7_7FxHQ_D4)

Amazon EC2 is a web service that provides secure, resizable compute capacity in the cloud. It allows you to provision virtual servers called EC2 instances. Although AWS uses the phrase “web service” to describe it, it doesn’t mean that you are limited to running just web servers on your EC2 instances. You can create and manage these instances through the AWS Management Console, the AWS Command Line Interface (CLI), AWS Software Development Kits (SDKs), or through automation tools and infrastructure orchestration services.In order to create an EC2 instance, you need to define:

- Hardware specifications, like CPU, memory, network, and storage.
- Logical configurations, like networking location, firewall rules, authentication, and the operating system of your choice.

When launching an EC2 instance, the first setting you configure is which operating system you want by selecting an Amazon Machine Image (AMI).

## What Is an AMI?

In the traditional infrastructure world, the process of spinning up a server consists of installing an operating system from installation disks, installation drives, or installation wizards over the network. In the AWS Cloud, this operating system installation is no longer your responsibility, and is instead built into the AMI that you choose.Not only does an AMI let you configure which operating system you want, you can also select storage mappings, the architecture type (such as 32-bit, 64-bit, or 64-bit ARM), and additional software installed.

## What Is the Relationship Between AMIs and EC2 Instances?

EC2 instances are live instantiations of what is defined in an AMI, much like a cake is a live instantiation of a cake recipe. If you are familiar with software development, you can also see this kind of relationship between a Class and an Object.

A Class is something you model and define, while an object is something you interact with. In this case, the AMI is how you model and define your instance, while the EC2 instance is the entity you interact with, where you can install your web server, and serve your content to users.When you launch a new instance, AWS allocates a virtual machine that runs on a hypervisor. Then the AMI you selected is copied to the root device volume, which contains the image used to boot the volume. In the end, you get a server you can connect to and install packages and any additional software. In this case, you install a web server along with the properly configured source code of your employee directory app.

![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/VBk76PGITdKLGz9RPTGtXw_16b6431eb1354ab889f7433d964da9f1_image.png?expiry=1688342400000&hmac=uLtD1ijozPMABZXWWaDY_rFDH0CqcVeUHyk2C87sQ7Y)

One advantage of using AMIs is that they are reusable.

You might choose a Linux-based AMI and configure the HTTP server, application packages, and any additional software you may need to run your application.

If you wanted to create a second EC2 instance with the same configurations, how can you easily do that? One option is to go through the entire instance creation and configuration process and try to match your settings to the first instance. However, this is time consuming and leaves room for human error.

The second, better option, is to create an AMI from your running instance and use this AMI to start a new instance. This way, your new instance will have all the same configurations as your current instance, because the configurations set in the AMIs are the same.

![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/rGO-wfxDSs6pvOl6I3QaYQ_28d2e58cdf33439bb53d1af93d907cf1_image.png?expiry=1688342400000&hmac=Hq33FDfFSO7et3kV7oZTA6STLnBU161_cG5uFsX5lmM)

## Where Can You Find AMIs?

You can select an AMI from the following categories.

- Quick Start AMIs that are premade by AWS and allow you to get started quickly.
- AWS Marketplace AMIs that provide popular open source and commercial software from third-party vendors.
- My AMIs that are created from your EC2 instances.
- Community AMIs that are provided by the AWS user community.
- Build your own custom image with EC2 Image Builder.

Each AMI in the AWS Management Console has an AMI ID, which is prefixed by “ami-”, followed by a random hash of numbers and letters. These IDs are unique to each AWS region.

![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/bCYne2MSRlS010zJsiNAZA_84eae9f67a694edfbc19cee7e2750bf1_asset-v1-AWS-AWS-AWS-OTP-AWSD16-1T2023-type-asset-block-Reading_2.2_AMI_s.png?expiry=1688342400000&hmac=rwrnvHdYjK4R0lCw7dPgymtAylfOz9zmzccRjHg8NHQ)