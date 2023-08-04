![[index (5) 1.mp4]]
Let's take a look at completing the exercises in your own environment. The exercise instructions we have supplied include steps for getting everything working in the Cloud9 environment. Developers like to personalize their IDE and dev environments, maybe you'd like to attempt to exercises in your own local environment. It doesn't take too much modification to do this. This is a bit of an advanced approach. If the concepts in this course are new to you, you might want to follow the supplied instructions first. If you are pretty familiar with the AWS Serverless Application Model, Python, and the AWS CLI, then follow along. I'm going to go through the process of debugging the application in Visual Studio Code. The requirements are actually pretty simple. This is a completely new setup. All I have installed is Python 3, Node, Visual Studio Code, and the AWS CLI. This will be exactly the same on macOS and Linux. We start by downloading the exercise source we supplied in the first exercise.
# __
I can unzip this and move this to my Documents folder. Now that that's done, I can open a command window and I'll install the AWS SAM CLI, with pip3 install aws-sam-cli. Next, I'm going to configure the AWS CLI with aws configure. I need to configure the CLI with an AWS identity and a default Region. I'm going to paste in an access key ID and secret access key. They belong to an AWS Identity and Access management, or IAM, user, that I want to use for authentication on my laptop.
# __
I need to supply a Region, so I'm going to use us-west-2. Now, let's go to the Documents folder, where trivia-app is unzipped. There is the template YAML that I can use to build and deploy the SAM application. This is the same commands that we used in Exercise 1, sam build, and sam deploy --guided. I give the application a name. And I'm just going to go with the defaults for everything else. That has completed. We began Exercise 2 by installing the pip requirements for the backend code and the unit tests. We can do the same here. Now, let's open the backend code in Visual Studio Code. I've opened up the code. This is Python application, and I already have the Python extensions installed here for Visual Studio Code. There's one more thing I need to set up here. In Exercise 2, the integration test expects an environment variable. So let's add a .env file, and we'll add the environment variable. There we go, I've set AWS_SAM_STACK_NAME equal to trivia-app. That's what our integration test expects. I need to tell the IDE about the tests that we have. So, I can open the command palette, here. And I search for Python Configure Tests. There it is there. We are using the pytest framework, and my tests in the tests folder. That has added a configuration to our project over here, in settings.json, and we can see pytest is enabled. Now, I can open tests from the activity bar here, and the IDE has discovered all the unit tests and integration tests in my project. Let's go into the test, here, that is calculating the scores. I can set a breakpoint over here, and click the little debug icon. And now, I can step over code, I can step in to code. In the testing activity, on the left, back here, I can select all unit tests and hit play. And we see that they all pass. That's just one way of getting the project to run in a local environment. I'm sure developers in the audience all have their favorite IDEs and environments for testing. Please come over to the forums and share with us how you are setting up your own environments.