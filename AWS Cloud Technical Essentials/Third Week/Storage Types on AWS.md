The next thing we need to configure for our employee directory app is the storage. Our application requires several types of storage for its data. For one, we need to store the operating system, software, and system files of our app. We also need to store static assets, like photos for the employee headshots, and then we have more structured data, such as the name, title, and location of each employee, as well. All of that needs a home. The structured data usually requires a database, which we'll talk about later this week, so for now we'll focus on storing the application files as well as the static content. 
# __
![[Pasted image 20230706221305.png]]
There are two main types of storage that we can use to store this data, block and object. Here's the difference. Let's say that I have a one gigabyte file with text in it. If I'm storing this in block storage, what happens is that this file is split into fixed size chunks of data and then stored. Object storage, on the other hand, treats each file like a single unit of data. This might seem like a small difference, but it can change how you access and work with your data. Let's say I want to change one character out of that one gigabyte file. If my file is stored in block storage, changing that one character is simple, mainly because we can change the block, or the piece of the file that the character is in, and leave the rest of the file alone. 
# __
![[Pasted image 20230706221335.png]]
In object storage, if I want to change that one character, I instead have to update the entire file. 
# __
Let's take these two types of storage and access patterns and try to apply them to the data we want to store. 
# __
![[Pasted image 20230706221412.png]]
For example, our static data, like the employee photos, will most likely be accessed often, but modified rarely. Therefore, storing in object storage is fine. For more frequently updated data or data that has high transaction rates, like our application or system files, block storage will perform better. 
# __
In this section of the course, we'll discuss both block and object AWS storage services and how they'll interact with our employee directory application. Before we do that, take a look at the notes to get a refresher of the different types of storage. That way you can easily match the storage type to the AWS storage service that we talk about.