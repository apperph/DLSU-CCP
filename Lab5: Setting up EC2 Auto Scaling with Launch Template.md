## Overview:

This lab activity will demonstrate how to create a launch template and integrate it into an auto-scaling group. We will then simulate an unhealthy instance by terminating an EC2 instance and observe how EC2 auto-scaling will react.


## Prerequisite:

Before you start following the instructions below, you will need to have the following:

- VPC with at least 2 public subnets
- A security group without inbound rules and make sure it’s attached to your VPC, to create one go to the VPC console and click on security groups.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session4/Lab15/image15-1.png)


Once you have created the required resources, you can now proceed to the steps below.

## 1. Create a launch template.

1-a. Navigate to the EC2 console then go to Launch Templates.

1-b. Click create launch template.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session4/Lab15/image15-3.png)

1-c. In the Create launch template console, set the name and description of your template. Click the Auto Scaling guidance checkbox.
![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session4/Lab15/image15-4.png)

1-d. Select Amazon Linux 2 AMI ID, for the instance type just use t2.micro, and select Don’t include in launch template for key pair name
![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session4/Lab15/image15-5.png)

1-e. For network settings, choose the security group you created at the start of this lab. Leave subnet to "Do not include in template". Leave the rest of the settings as default, and click on create launch template.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session4/Lab15/image15-6.png)

## 2. Create an auto-scaling group.

2-a. Navigate to auto scaling groups. Click create auto scaling group

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session4/Lab15/image15-9.png)


2-b. Set the name of your auto scaling group, then select your launch template and click next.
![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session4/Lab15/image15-10.png)

2-c. Select Adhere to launch template for the Instance purchase options and select your VPC and public subnets.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session4/Lab15/image15-11.png)

2-d. Leave the advance options as default.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session4/Lab15/image15-12.png)

2-e. Set the following values.

- Desired capacity: 2
- Minimum capacity: 2
- Maximum capacity: 4

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session4/Lab15/image15-13.png)


2-f. Leave the notifications as default

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session4/Lab15/image15-14.png)


2-g. Set the tags, use the key: Name
![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session4/Lab15/image15-15.png)

2-h. Review your configurations and click create autoscaling group

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session4/Lab15/image15-16.png)

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session4/Lab15/image15-17.png)


## 3. Test EC2 autoscaling

Now you have created the autoscaling group, let’s now test if our configuration will work properly.

3-a. Navigate to the EC2 console, and you’ll see that you have 2 running instances.
![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session4/Lab15/image15-18.png)


3-b. To test autoscaling, terminate one of the instances.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session4/Lab15/image15-19.png)

3-c. Wait for at least a minute and you’ll see that a new instance will be created automatically by EC2 auto-scaling.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session4/Lab15/image15-20.png)



Well done!

Please copy and paste the JSON in the textbox found on the left side and supply the necessary information.

```json
{
 "launch_template_name":"",
 "autoscaling_group_name": ""
}
```

**To delete the resources, first delete the autoscaling group the instances created will be automatically terminated.**
