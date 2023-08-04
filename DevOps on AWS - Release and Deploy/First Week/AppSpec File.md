The application specification file (AppSpec file) is file used by AWS CodeDeploy to manage a deployment. It can be written in [YAML](http://www.yaml.org/) or JSON.

### **AppSec file for Amazon ECS applications**

For Amazon Elastic Container Service (Amazon ECS) applications, the AppSpec file is used by AWS CodeDeploy to determine:

- Your Amazon ECS task definition file. This file is specified with its Amazon Resource Number (ARN) in the TaskDefinition instruction of the AppSpec file.

- The container and port in your replacement task set where your Application Load Balancer or Network Load Balancer reroutes traffic during a deployment. This setting is specified in the LoadBalancerInfo instruction of the AppSpec file.

- Optional information about your Amazon ECS service, such the platform version it runs on, its subnets, and its security groups.    

- Optional Lambda functions to run during hooks that correspond with lifecycle events during an Amazon ECS deployment.

Here is an example of an AppSpec file for deploying an Amazon ECS service, written in YAML.
```yml
version: 0.0 
Resources: 
	- TargetService: 
		Type: AWS::ECS::Service 
		Properties: 
			TaskDefinition: "arn:aws:ecs:us-east-1:111222333444:task-definition/my-task-definition-family-name:1" 
			LoadBalancerInfo: 
				ContainerName: "SampleApplicationName" 
				ContainerPort: 80 

# Optional properties 
	PlatformVersion: "LATEST" 
	NetworkConfiguration: 
		AwsvpcConfiguration: 
		Subnets: ["subnet-1234abcd","subnet-5678abcd"] 
		SecurityGroups: ["sg-12345678"] 
		AssignPublicIp: "ENABLED" 
	CapacityProviderStrategy: 
		- Base: 1 
		CapacityProvider: "FARGATE_SPOT" 
		Weight: 2 
		- Base: 0 
		CapacityProvider: "FARGATE" 
		Weight: 1 
Hooks: 
- BeforeInstall: "LambdaFunctionToValidateBeforeInstall" 
- AfterInstall: "LambdaFunctionToValidateAfterInstall" 
- AfterAllowTestTraffic: "LambdaFunctionToValidateAfterTestTrafficStarts" 
- BeforeAllowTraffic: "LambdaFunctionToValidateBeforeAllowingProductionTraffic" 
- AfterAllowTraffic: "LambdaFunctionToValidateAfterAllowingProductionTraffic"
```


### **AppSpec file for AWS Lambda applications**

For Lambda applications, the AppSpec file is used by CodeDeploy to determine:

- Which Lambda function version to deploy.    
- Which Lambda functions to use as validation tests.    

For Lambda, you must specify your application alias, and the current and target version you’re deploying to. Here is an example of an AppSpec file for deploying a Lambda function version, written in YAML.

```yaml
version: 0.0 
Resources: 
	- myLambdaFunction: 
		Type: AWS::Lambda::Function 
		Properties: 
			Name: "myLambdaFunction" 
			Alias: "myLambdaFunctionAlias" 
			CurrentVersion: "1" 
			TargetVersion: "2" 
Hooks: 
	- BeforeAllowTraffic: "LambdaFunctionToValidateBeforeTrafficShift" 
	- AfterAllowTraffic: "LambdaFunctionToValidateAfterTrafficShift"
```


### **Hooks**

The content in the 'hooks' section of the AppSpec file varies, depending on the compute platform for your deployment. The 'hooks' section for an Amazon EC2 or on-premises deployment contains mappings that link deployment lifecycle event hooks to one or more scripts. The 'hooks' section for a Lambda or an Amazon ECS deployment specifies Lambda validation functions to run during a deployment lifecycle event. If an event hook isn’t present, no operation is run for that event. This section is required only if you are running scripts or Lambda validation functions as part of the deployment.

### **Permissions**

The 'permissions' section specifies how special permissions (if any) should be applied to the files and the directories in the 'files' section after they are copied to the instance. You can specify multiple object instructions. This section is optional. It applies to Amazon Linux, Ubuntu Server, and RHEL instances only. **Note:** The 'permissions' section is used only for Amazon EC2 or on-premises deployments. It’s not used for Lambda or Amazon ECS deployments.

### **Resources**

[CodeDeploy AppSpec File reference](https://docs.aws.amazon.com/codedeploy/latest/userguide/reference-appspec-file.html) [AppSpec File example](https://docs.aws.amazon.com/codedeploy/latest/userguide/reference-appspec-file-example.html) [AppSpec File structure](https://docs.aws.amazon.com/codedeploy/latest/userguide/reference-appspec-file-structure.html) [AppSpec ‘permissions’ section (EC2/On-Premises deployments only)](https://docs.aws.amazon.com/codedeploy/latest/userguide/reference-appspec-file-structure-permissions.html)