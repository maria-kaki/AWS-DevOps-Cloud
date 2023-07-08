Now that you have a better understanding of storage on AWS, it's time for a hands-on exercise. In this exercise, you'll be working with Amazon S3. You'll have the opportunity to create an S3 bucket, upload an object, and create a bucket policy. Let's quickly go through what you'll be doing in the console. 
# __
![[Pasted image 20230706234258.png]]
The first thing you'll need to do is create an S3 bucket. To do this, you'll find Amazon S3 in the search bar and then in the S3 dashboard, 
![[Pasted image 20230706234324.png]]
you'll click Create bucket. 
# __
![[Pasted image 20230706234352.png]]
We'll name this bucket, employee photo bucket and then at the end of the bucket name, we'll append your initials and also a random number. This is to ensure the bucket name is unique across all AWS accounts. We'll also locate this bucket in the Oregon region. 
![[Pasted image 20230706234410.png]]
Once you create a bucket, you can then upload your photos. 
# __
![[Pasted image 20230706234427.png]]
I'll do this by clicking on my bucket name 
![[Pasted image 20230706234444.png]]
and then click Upload.
# __
![[Pasted image 20230706234502.png]]
From here, I'll click Add files, find the object I want to upload, and then Upload once more. 
# __
![[Pasted image 20230706234524.png]]
From there, you should get a message saying, "You successfully uploaded your photo." 
# __
Now, just because you uploaded a photo and S3 doesn't mean your application can read it by default. You'll need to give it permission to do so by creating a bucket policy that allows access from your application. 
# __
![[Pasted image 20230706234604.png]]
The next step is we'll click Exit, which will take us back to our bucket. 
# __
![[Pasted image 20230706234618.png]]
Then we'll click on the Permissions tab. 
# __
![[Pasted image 20230706234628.png]]
From there, we'll scroll down and click Edit Bucket Policy. 
# __
![[Pasted image 20230706234647.png]]
We'll supply you with the correct bucket policy, so you'll just need to copy and paste and then click Save. 
# __
![[Pasted image 20230706234712.png]]
The next thing you'll need to do is modify your application so that it knows which S3 bucket to access. To do this, we'll launch a new EC2 instance, hosting your application and change the user data. 
# __
![[Pasted image 20230706234730.png]]
So, we'll first find the EC2 service. Click on Instances, 
![[Pasted image 20230706234745.png]]
find the instance you launched earlier, 
![[Pasted image 20230706234802.png]]
and then click on Actions, Images, and Templates and then click Launch more like this. 
# __
![[Pasted image 20230706234828.png]]
This will use the exact configuration of your instance that you had before. However, you'll need to modify the user data. Scroll down to the bottom where it shows your user data and then where it shows photos_bucket, you'll type in the name of your bucket. 
# __
![[Pasted image 20230706234853.png]]
Alright, once you're done with that, review and launch. Your application will now use the S3 bucket you created and has access through the bucket policy to your objects. 
# __
![[Pasted image 20230706234913.png]]
That's it for this one.