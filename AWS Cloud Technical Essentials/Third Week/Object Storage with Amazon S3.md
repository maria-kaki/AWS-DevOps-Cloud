So we've figured out block storage for our application. Now, we need to figure out where to store our employee photos. A natural question is, why can't we just store these photos in Amazon EBS? Well, there's a few reasons. 
- Number one, most EBS volumes are only connected to one EC2 instance at a time. Multi-attach is not supported by all volume and instance types. Eventually, as my app scales, I'll need to figure out how to access those photos from all of my instances, that's an issue. 
- The second consideration is that an EBS volume has size limitations. That means that eventually, there will be a limit to how many HD 4K photos I store of my employees in one drive. Ideally, I'd store these photos in a more scalable solution. 
So EBS probably isn't the right choice. Fortunately, AWS has a service called Amazon Simple Storage Service or Amazon S3 that was designed to be a standalone storage solution that isn't tied to compute, meaning you don't mount this type of storage onto your EC2 instances. Instead, you can access your data through URLs from anywhere on the web, which gives this service its nickname, storage for the internet. S3 also allows you to store as many objects as you'd like with an individual object size limit of five terabytes. This makes it ideal for our employee photos. Now, let's talk about how we store things in S3. The underlying storage type for S3 is object storage. That means that all of the same characteristics of object storage are also characteristics of S3. So S3 uses a flat structure. It uses unique identifiers to look up objects when requested, you get the idea. S3 is also considered distributed storage, meaning that we store your data across multiple different facilities within one AWS region. 
# __
![[Pasted image 20230706223200.png]]
This is what makes S3 designed for 99.99% availability and gives it 11 nines of durability. Alright, let's learn about some S3 concepts. 
# __
The first concept is a bucket. In S3, you store your objects in a bucket. You can't upload any object, not even a single photo to S3 without creating a bucket first. You then place your objects inside of these buckets. And if you want to organize and arrange those objects, you can also have folders inside of the buckets. Let's create a bucket in the console. 
# __
![[Pasted image 20230706223256.png]]
When you log in, you'll type S3 in the Service search bar. Once you click on it, 
![[Pasted image 20230706223317.png]]
you'll see the S3 dashboard showing you all the available buckets for every region. 
# __
![[Pasted image 20230706223335.png]]
I'll then select Create bucket. 
# __
![[Pasted image 20230706223401.png]]
What I want to point out here is that buckets are region specific, so we can choose where we want to place our bucket. 
# __
![[Pasted image 20230706223420.png]]
In this case, we want to place our bucket close to our infrastructure for our application, which is in the Oregon region, so we'll choose Oregon. 
# __
![[Pasted image 20230706223552.png]]
Next, we have the name of our bucket. Even though our bucket is specific to one region, our bucket name has to be globally unique across all AWS accounts and must be DNS compliant. Once you create your bucket, AWS will construct a URL using this name, so it has to be something that is reachable over HTTP or HTTPS, meaning there can be no special characters, no spaces, et cetera. So for this bucket's name, let's choose employee-photo-bucket-sr-001, which is DNS compliant. 
# __
![[Pasted image 20230706223612.png]]
Now we can leave the rest as defaults. Scroll down and click create. 
# __
![[Pasted image 20230706224338.png]]
To work with this bucket, I'll need to find it in the list and click on its name. 
# __
![[Pasted image 20230706225222.png]]
Here we can start uploading our objects. To do this, I'll click Upload 
![[Pasted image 20230706225246.png]]
and then Add files. Now I can choose any file I want 
![[Pasted image 20230706225306.png]]
and then I'll click Upload. 
# __
![[Pasted image 20230706225425.png]]
So as you can see, the object upload was successful. 
# __
![[Pasted image 20230706225446.png]]
If I click on the name of my object, 
![[Pasted image 20230706225509.png]]
I'll be able to see quite a bit of detail. I can see the owner, region and size, but most importantly, 
![[Pasted image 20230706225538.png]]
we can see the URL of my object. The first part of this URL is simply my bucket URL that AWS created using the bucket name. Then AWS appended the name of my object, also referred to as the object key to the bucket URL. Now, what happens if I click on this URL? 
# __
![[Pasted image 20230706225612.png]]
Hmm, access denied. That's weird, right? 
# __
Well, not really. That access denied message leads us to a bigger question that most people have when they start out on AWS and that's who can access my data. Earlier I mentioned that you can retrieve your data from anywhere on the web and people often think that means that anyone can retrieve that data. By default, it's actually the opposite. Everything in S3 is private by default. This means that all S3 resources such as buckets, folders and objects can only be viewed by the user or AWS account that created that resource. That's why I got an access denied message, because I was acting as an anonymous user on the internet trying to access an S3 object that's private. Now, that's not to say no object or bucket can be open to the world. They absolutely can be if you explicitly choose that option and it's actually kind of a process to make something public. The reason it's difficult to make your objects public is to prevent accidental exposure of your data. Let's try it. 
# __
![[Pasted image 20230706231559.png]]
Okay, so if we want to make the object we created public, we need to do a few things. Normally, from the object detail page, we would be able to click on the object actions dropdown and then select make public using ACL, but it is currently not available for us to select. 
# __
![[Pasted image 20230706231640.png]]
Going to the bucket details page, 
![[Pasted image 20230706231714.png]]
I can select the permissions tab and see that there is a default setting that blocks all public access. From there I can verify that Block public access bucket setting is set to block all public access. 
# __
![[Pasted image 20230706231849.png]]
I'll click Edit, 
![[Pasted image 20230706231905.png]]
then uncheck the top box that blocks all public access and then save the changes. 
# __
![[Pasted image 20230706231945.png]]
I'll type Confirm to make the change and then click Confirm to finalize it. 
# __
![[Pasted image 20230706232024.png]]
From there, I'll go back to the bucket permissions tab and scroll down to the Object Ownership section and click Edit for this pane. 
# __
![[Pasted image 20230706232046.png]]
Instead of the default setting to disable access control lists or ACLs, 
![[Pasted image 20230706232142.png]]
I'll select ACLs enabled, then acknowledge and then save the changes. 
# __
![[Pasted image 20230706232205.png]]
Now I can go back to the object details page 
![[Pasted image 20230706232224.png]]
![[Pasted image 20230706232313.png]]
and select Make public using ACL from the object actions drop down. 
# __
![[Pasted image 20230706232345.png]]
This will allow me to make the object public. 
# __
![[Pasted image 20230706232406.png]]
To view the object, all I need to do is go back to the object details, 
![[Pasted image 20230706232422.png]]
find the URL, 
![[Pasted image 20230706232437.png]]
and click on it to view the photo. 
# __
That's how you make an object public. That being said, most of the time you don't want your permissions to be all or nothing, to where either nobody can see it or everybody can see it. Typically, you want to be more granular about the way you provide access to resources. As far as access control, you can use IAM policies attached to users, groups, and roles to access your S3 content and you can also use a feature called S3 bucket policies. S3 bucket policies are similar to IAM policies in that they're both defined using the same policy language in a JSON format. The difference is IAM policies are attached to users, groups and roles, whereas S3 bucket policies are only attached to buckets. 
# __
![[Pasted image 20230706232610.png]]
S3 bucket policies specify what actions you're allowed or denied on the bucket. For example, you might want to attach an S3 bucket policy to it that allows another AWS account to put objects in that bucket. Or you might want to create a bucket policy that allows read-only permissions to anonymous viewers. S3 bucket policies can be placed on buckets and cannot be used for folders, or objects. However, the policy that is placed on the bucket can apply to every object in that bucket. 
# __
Alright, to recap, S3 uses containers called buckets to store your objects and you have several options to control access to those objects through the use of IAM policies and bucket policies.