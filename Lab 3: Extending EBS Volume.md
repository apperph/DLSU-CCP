## Overview:

This lab will demonstrate how to **extend an EBS volume** on an **EC2 instance**.

**Prerequisite:**

- **Create an EC2 instance** running on **Amazon Linux 2023 AMI**
- Place the instance in a **public subnet**
- Allow **SSH traffic** in the **security group**
- Ensure you have a copy of the **SSH key-pair**

Once you have created the necessary resources, please proceed with the steps below.

## 1. Extend the EBS Volume.

1-a. Navigate to the **EC2 console**, select your **instance**, go to the b tab, and click on the **EBS volume**.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab7/image-1.png)

1-b. Select your **EBS volume**, click on **Actions > Modify Volume**.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab7/image-2.png)

1-c. Increase the **storage capacity** of the **EBS volume** from **8 GB to 20 GB**.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab7/image-3.png)

- Click **Modify**, and when a prompt appears, click **Yes**.

## 2. Extend the partition

2-a. Use **SSH** or **EC2 Instance Connect** to connect to the **EC2 instance**.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab7/image-4.png)

2-b. To check the current size of the volume, type the command:

`Lsblk`

The entire volume shows a capacity of **20 GB**, but only the initial **8 GB** is usable. This means the partition needs to be extended to utilize the full volume capacity.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab7/image-5.png)

2-c. To extend the partition storage capacity, use the **growpart** command. Notice that there is space between the **device name** and **partition number.**

The command will be:

`sudo growpart <device> <partition_number>`

For example:

`sudo growpart /dev/xvda 1`

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab7/image-6.png)

2-d. Check the partition size again to see if the command successfully extended the partition storage capacity by running:

`lsblk`


![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab7/image-7.png)


## 3. Extend the file system

3-a. Check the file system size by running:

`df -h`

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab7/image-8.png)

We can see that the file system still recognizes 8GB.

3-b. Extend the **file system** by running the command:

`sudo xfs_growfs /dev/xvda1`

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab7/image-9.png)

3-c. Check the file system size again by running:

`df -h`

This will display the updated file system size, showing the new available capacity after extending the file system.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab7/image-10.png)


You have successfully extended the file system from **8 GB** to **20 GB!**


Well done!

**JSON**

Please copy and paste the JSON in the textbox on the left side and supply the necessary information.

```
{
 "ec2_instance_id":"",
 "ebs_volume_id": ""
}
```

**Resource Cleanup**

Kindly delete the resources you created for this lab activity
