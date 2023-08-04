![[index (12).mp4]]
We walked you through the core components of AWS CodeDeploy in a previous video, but it's time to get a bit deeper into one of them, the AppSpec file. It's important to have a good understanding of this file, as CodeDeploy relies on it heavily. This AppSpec is a YAML or JSON file that contains locations for all the installation files, scripts, and when to initiate specific actions. This is where you get to control how your revision deployments are actually managed, and how you determine a deployment was successful.
# __
Let's take a look at the AppSpec file that we'll be using later in the labs. Note that this is an AppSpec file that's used for Amazon EC2 based deployments. If you're looking for more information on serverless AppSpec files, check out the reading following this video. All right, so this AppSpec file is a YAML file, and it's pretty simplistic in nature. A lot of AppSpec files can get pretty complicated, but I'll talk you through all your options and why we chose the ones we did for this specific file.
# __
So, this file is broken out into four sections: version, os, files, and hooks. We could additionally have another section called the permissions section, which we'll talk about a bit later. Out of all the sections, the version and the os are the simplest parts. The version refers to the CodeDeploy AppSpec version, and not the version of your specific application or deployments. And currently, the only accepted value is 0.0. The os section, as you may have already guessed, stands for operating system, and it only accepts two possible values, Linux or Windows. The EC2 instance you'll be working with in the lab is a Linux box, so we chose Linux. Now, all the rest of the sections are optional. That means the hooks, files, and the permissions sections are not required. So let's talk about why. The files section is only necessary, if you're going to be copying files to your instance during the deployments. It has a source and destination subsection. The source subsection identifies a file or directory from your revision to copy. The destination identifies the location on this instance of where the file or directory should be copied. So for our AppSpec file, we want the index.html file to be copied to the var/www/html directory on our instance. The next section we are going to review is the hooks section. The hooks direct the CodeDeploy agent as to what it needs to do and in what sequence. Some of the main hooks that you can use are BeforeInstall, AfterInstall, ApplicationStart, ApplicationStop, and ValidateService. Each of these is used to run scripts that you specify when the hook is initiated. You'll notice that each of these hooks is structured the same way. You specify the location of the script, the timeout you want to allow for it to run, and if you're running a Linux deployment, runas refers to the level at which you want to run the script. Or, in other words, the user on your Linux instance you want to use to run the script, such as root.
# __
Note that we're not using every one of these hooks. In our file, we're only using three of these hooks, BeforeInstall, ApplicationStop, and ApplicationStart. That's because they're the only ones necessary for this deployment, so we've completely omitted the other options from the file. Let's talk about each of these hooks in detail.
Reproduza o vídeo começando em :3:43 e siga a transcrição3:43
The Before and AfterInstall hooks are used for the script that you need to run before the installation happens, and after the installation is complete. For example, here, we're linking to a script that installs the dependencies needed to run our application. If I look at the script, you can see that I'm installing an Apache web server here, which is needed for the site.
# __
Going back to the AppSpec file, the ApplicationStop and ApplicationStart hooks are used to run any scripts needed to stop and start the application. We're using these hooks to start and stop our Apache server. So, looking at the start_server script in a text editor, you can see we're doing just that, starting the server. And in this stop_server script, you can see that I'm checking to see if the Apache web server is running, and if it is, I stop it. Now, there is another hook that you cannot use to initiate a script, and it's called Install. In CodeDeploy, the Install stage is just the stage where it copies over the files from the source to the destination on your behalf. Lastly, you can use the ValidateService hook to run any scripts that you will use to test and make sure that everything has been installed and started correctly.
# __
After the hooks, that leaves us with one last section, the permissions section. I'll go ahead and paste in a permissions section to this file, so that you can see some of the settings. The permissions section is only valid if the os setting is set to Linux. It refers to the permissions you want to apply to the files being copied in the file section. If you're specifying permissions, then the file section is required. I won't go through every part of the permissions, but I do want to state that if you use permissions, the one required part within permissions that you must include is the object section. Object refers to the set of system files, folders, or directories that the specified permissions are applied to after the file system objects are copied to the instance. There's a lot more to the AppSpec file that I can cover in this video, so make sure to check out the notes section for more information and resources. I'll also provide examples of how you can use the permissions section for your deployments.