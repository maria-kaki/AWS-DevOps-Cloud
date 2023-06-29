Infrastructure, like data centers and networking connectivity, still exists as the foundation of every cloud application. In AWS, this physical infrastructure makes up the AWS Global Infrastructure, in the form of Availability Zones and Regions.

## REGIONS

![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/GA-td82sSJ-A1bMhZAK-Kg_76e9d578334d47e6b9f7a74ec2376bf1_Regions.png?expiry=1688169600000&hmac=Ht0hb4CZIq5ZvtysCWt9fifwJY1sXpAlWQOXLprTY2I)

Regions are geographic locations worldwide where AWS hosts its data centers. AWS Regions are named after the location where they reside. For example, in the United States, there is a Region in Northern Virginia called the Northern Virginia Region and a Region in Oregon called the Oregon Region. There are Regions in Asia Pacific, Canada, Europe, the Middle East, and South America, and AWS continues to expand to meet the needs of its customers.Each AWS Region is associated with a geographical name and a Region code.

![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/hDx5s-sZRkGvR_XA-VoZ2A_57b85de84aed4ee9be064082687493f1_image.png?expiry=1688169600000&hmac=3RQiOnvVIjTDvafoP7QwTZnDE11uT5CcyghnkZXztpc)

Here are a few examples of Region codes:

- us-east-1: This is the first Region created in the east of the US. The geographical name for this Region is N. Virginia.
    
- ap-northeast-1: The first Region created in the northeast of Asia Pacific. The geographical name for this Region is Tokyo.
    

AWS Regions are independent from one another. This means that your data is not replicated from one Region to another, without your explicit consent and authorization.

## CHOOSE THE RIGHT AWS REGION

Consider four main aspects when deciding which AWS Region to host your applications and workloads: latency, price, service availability, and compliance.

**Latency.** If your application is sensitive to latency, choose a Region that is close to your user base. This helps prevent long wait times for your customers. Synchronous applications such as gaming, telephony, WebSockets, and IoT are significantly affected by higher latency, but even asynchronous workloads, such as ecommerce applications, can suffer from an impact on user connectivity.

**Price.** Due to the local economy and the physical nature of operating data centers, prices may vary from one Region to another. The pricing in a Region can be impacted by internet connectivity, prices of imported pieces of equipment, customs, real estate, and more. Instead of charging a flat rate worldwide, AWS charges based on the financial factors specific to the location.

**Service availability.** Some services may not be available in some Regions. The AWS documentation provides a table containing the Regions and the available services within each one.

**Data compliance.** Enterprise companies often need to comply with regulations that require customer data to be stored in a specific geographic territory. If applicable, you should choose a Region that meets your compliance requirements.

## AVAILABILITY ZONES

![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/lIc5YSi_SuCX4wI4pGNmsg_b3dde14493c846fdbd18a10956d6b3f1_AZs.png?expiry=1688169600000&hmac=JDdBMKyXSUdHfqs8MPHXQ3Y74w66hNaqqAsOWO_-Hd8)

Inside every Region is a cluster of Availability Zones (AZ). An AZ consists of one or more data centers with redundant power, networking, and connectivity. These data centers operate in discrete facilities with undisclosed locations. They are connected using redundant high-speed and low-latency links.AZs also have a code name. Since they’re located inside Regions, they can be addressed by appending a letter to the end of the Region code name. For example:

- us-east-1a: an AZ in us-east-1 (Northern Virginia Region)
    
- sa-east-1b: an AZ in sa-east-1 (São Paulo Region in South America)
    

If you see that a resource exists in us-east-1c, you know this resource is located in AZ c of the us-east-1 Region.

## SCOPE AWS SERVICES

Depending on the AWS Service you use, your resources are either deployed at the AZ, Region, or Global level. Each service is different, so you need to understand how the scope of a service may affect your application architecture.When you operate a Region-scoped service, you only need to select the Region you want to use. If you are not asked to specify an individual AZ to deploy the service in, this is an indicator that the service operates on a Region-scope level. For region-scoped services, AWS automatically performs actions to increase data durability and availability.On the other hand, some services ask you to specify an AZ. With these services, you are often responsible for increasing the data durability and high availability of these resources.

## MAINTAIN RESILIENCY

To keep your application available, you need to maintain high availability and resiliency. A well-known best practice for cloud architecture is to use Region-scoped, managed services. These services come with availability and resiliency built in.When that is not possible, make sure the workload is replicated across multiple AZs. At a minimum, you should use two AZs. If one entire AZ fails, your application will have infrastructure up and running in at least a second AZ to take over the traffic.

![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/3ToUyNl3TKScMGwOy5hFTA_7273fe75dd8941b8a6f8644d419a16f1_image.png?expiry=1688169600000&hmac=TpeXvx5W3H49J5eLymMjJQvZSEXnHIg5LGjK-uymvVY)
