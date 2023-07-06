One of the main reasons why EC2 provides so much value is the fact that you can provision new EC2 instances on demand, and just as easily, you can get rid of instances that you no longer need. In most cases, you only get charged for instances that are currently running.
![[Pasted image 20230701130016.png]]
EC2 allows you to stop and start instances at will, which enables you to treat your fleet of EC two instances as elastic, scaling them in or out. Then at the end of the billing cycle, you only pay for what you use. We are building up to the idea of scaling your fleet of EC2 instances in and out to serve demand.
# __
But before we get there, it's important to understand some of the more basic things about EC2. Let's talk about the EC2 instance lifecycle.
# __
![[Pasted image 20230701130702.png]]
An Amazon EC2 instance transitions through different states from the moment you launch it through to its termination. You launch an EC2 instance from an AMI, and as you learned in a previous lesson, once the EC2 instance is launched, it enters a pending state. This state is essentially your VM booting up. Once the instance is ready for use, it enters the running state. In the running state, you will be charged for the EC2 instance. From running, you have a couple of different options. You can reboot the instance, which is similar to rebooting, say, your laptop. It turns off, then it turns back on again. Pretty straightforward. You can also choose to stop your instance. It will enter a stopping phase, then enter the stopped phase. Stopping an instance is like powering down your laptop. You can always turn it back on and it will go through its usual boot sequence, moving through the pending state and back to the running state. The other option, which is similar to stop, is to stop-hibernate your instance.
# __
This also enters the stopping phase and then the stopped phase. You can compare this to how you lock your laptop and shut the lid, but when you open it back up, everything is still in place where you left it. No boot sequences required. You are back up and running after a couple of seconds of the computer waking up. Since the state of the machine was written to memory when you stopped it, the state of the machine can be drawn from memory and put back into place. Then, you're back up and running.
# __
![[Pasted image 20230701131011.png]]
Now, the last option depicted here is the terminate option. When you terminate an instance, it enters the shutting down phase then the terminated phase.
# __
Terminating an EC2 instance is like taking your laptop out for a long boat right off the coast and throwing it into the ocean, getting rid of it forever. It's now lost in the great blue sea. There is no hope of finding your laptop on an island, shipwrecked one day, having been saved after spelling SOS in the sand.
# __
![[Pasted image 20230701131219.png]]
Anyways, I hope you had any data or state stored on that instance backed up because once you terminate an instance, it's gone. That being said, there is a feature called termination protection that you can enable if you're worried about instances being terminated accidentally. You also will learn about persistent storage and EC2 in future lessons, so don't fret. We will show you ways you can make sure your data sticks around, even if the EC2 instance doesn't.
# __
So that is the EC2 instance lifecycle. It's definitely a good idea to remember how all of this works if you plan on using EC2 to host your applications. And don't think of terminating instances as a bad thing.
# __
![[Pasted image 20230701131407.png]]
If your EC2 instances is having technical trouble for one reason or another, maybe it needs an update or a patch, instead of logging into the instance to fix it or install software, you can launch a new one with the new changes in its place and then you could terminate the old instance, having a new instance take that place. You of course can do in place updates as well, but just know that you have the option to decide how to handle these sorts of tasks.
# __
You can launch or terminate EC2 instances to meet demand. So as demand for your application increases, you can launch more instances and as it decreases, you can terminate instances. This keeps your EC2 instance fleet in line with demand. So again, terminating an instance isn't a bad thing and shouldn't be feared. Now, let's discuss the cost aspect of this. You only get charged for an EC2 instance if you're in the running state or if you are in the stopping state when preparing to hibernate. This means that you can stop instances when they aren't in use, say if you have applications that are only used during the work week. Run them when your employees are clocked in and then stop them when they aren't. Remember, you can always start from a stop state, allowing them to resume working when necessary.
# __
