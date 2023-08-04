### **What is DevOps?**

DevOps is the combination of cultural philosophies, practices, and tools that increases an organization’s ability to deliver applications and services at high velocity. Put simply, DevOps is a way for development teams and operations teams to work better together and ultimately share the responsibility of the software they build. For more information about what DevOps is and how it works, see: [What is DevOps?](https://aws.amazon.com/devops/what-is-devops/)

### **AWS CodeCommit**

AWS CodeCommit is a secure, highly scalable, managed source-control service that hosts private Git repositories. For more information about what CodeCommit is and how it works, see: [AWS CodeCommit User Guide](https://docs.aws.amazon.com/codecommit/latest/userguide/welcome.html) After a repository is created in CodeCommit, you can securely interact with it with the proper authentication and access permissions. For more information about authentication and access in CodeCommit, see: [Authentication and access control for AWS CodeCommit](https://docs.aws.amazon.com/codecommit/latest/userguide/auth-and-access-control.html)

### **AWS CodeBuild**

You can use AWS CodeBuild for continuous integration (CI) practices. It compiles your source code, runs unit tests, and produces artifacts that are ready to deploy. It also reduces the need to provision, manage, and scale your own build servers. With CodeBuild, you only pay for the service when you are using it. For more information about what CodeBuild is and how it works, see: [AWS CodeBuild User Guide](https://docs.aws.amazon.com/codebuild/latest/userguide/welcome.html) In this course, you also learned about two important things to configure so you can get your build processes into CodeBuild: a build project and a build specification (buildspec) file.

- **Build project** - Includes information about how to run a build, including where to get the source code, which build environment to use, which build commands to run, and where to store the build output.    
- **Buildspec file** - Is a collection of build commands and related settings, in YAML format, that CodeBuild uses to run a build.    

For more information about build projects, see: [Working with build projects](https://docs.aws.amazon.com/codebuild/latest/userguide/working-with-build-projects.html) For more information on buildspec files, see: [Build specification reference for CodeBuild](https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html)

### **Branching strategies**

A branch in Git is a pointer to a commit—that’s it! There are many ways to design your branching strategies. For reference, see the strategies used in the following resources:

- [Understanding the GitHub flow](https://guides.github.com/introduction/flow/)    
- [Gitflow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)