## Overview

In this lab, we will **demonstrate how to restore an EBS volume** using an **EC2 instance**.

To begin, we need to **create an EC2 instance**. Follow these guidelines:

- Use the **Amazon Linux 2023 AMI**.
- Select **t2.micro** as the **instance type**.
- Place it in a **public subnet**.
- Ensure **SSH traffic** is allowed in the **security group**.
- Assign the name **EC2-instance-1** to it.
- Keep all other **settings as default**.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab6/image-1.png)

After **creating the EC2 instance**, follow these steps:

## 1. Create an EBS Volume Snapshot

1-a. **SSH** into the **EC2 instance**

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab6/image-2.png)

1-b. **Create a file** and give it any name you prefer. For this demonstration, the file will be named **snapshot-demo.txt**.

- **Create the file** in the **default directory** using the command:
`touch <filename>`
- To **confirm the file** was created, use the command:
`ls` 
This will display the **list of files** in the **current directory**.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab6/image-3.png)

1-c. Navigate to the **EC2 dashboard** and select your instance. Then, go to the **Storage** tab and click on the **Volume ID**.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab6/image-4.png)

1-d. Click **Actions** and select **Create Snapshot**.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab6/image-5.png)

1-e. Assign the name **snapshot-demo** and click **Create Snapshot**.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab6/image-6.png)

1-f. Navigate to the **Snapshots** section and wait until the **status** of your snapshot is marked as **Completed**.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab6/image-7.png)


## 2. Delete your EC2 instance

Before **deleting your EC2 instance**, make sure to **note down the EC2 instance ID**. You will need to submit it in the **JSON document** at the end of this lab.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab6/image-8.png)

2-a. After noting down the **EC2 instance ID**, go to the **EC2 dashboard**, select your **instance**, and then **terminate it**.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab6/image-9.png)

##3. Create a new EC2 instance and detach the EBS volume.

3-a. Create a **new EC2 instance** with the **same configuration** as the previous one, but this time, **change the name**.

For the new EC2 instance, you can name it **EC2-instance-2**.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab6/image-10.png)

3-b. Stop the instance.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab6/image-11.png)

3-c. Go to **Storage** and click on the **EBS volume ID**.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab6/image-12.png)


3-d. Click on actions and detach volume.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab6/image-13.png)



## 4. Restore EBS snapshot & attach to EC2 instance

4-a. Go to **EBS snapshots** and click on **Actions** then **Create Volume**.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab6/image-14.png)

4-b. Select the **Availability Zone** used by your EC2 instance, and set the **name of the EBS volume** in the b section.

If you select an **Availability Zone** that is not used by your EC2 instance, you will **not be able to attach** the volume to your EC2 instance.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab6/image-15.png)

4-c. While on the **EC2 dashboard**, go to **Volumes,** select your **restored EBS volume**, click on **Actions**, and then select **Attach Volume**.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab6/image-16.png)


4-d. Select your **instance**, and for the **mount point** or **device**, set **/dev/xvda**.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab6/image-17.png)

Click **attach**.

4-e. Start the **EC2 instance**.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab6/image-18.png)

4-f. Once the instance is **running**, connect to it via **SSH** and check if the **file** we created is still stored in the **restored volume**.

Once you have **SSH** into the instance, use the command `ls` to list the **files** in the **directory**.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Labs2025/Session2/Lab6/image-19.png)

You have successfully restored an **EBS snapshot!**

**JSON**

Please copy the JSON below and fill in the required AWS resource details before pasting them in the textbox found on the left side.

```
{
  "snapshot_id": "",
  "ec2_instance_1_id": "",
  "ec2_instance_2_id": "",
}
```

**Resource Cleanup**

You can now delete the resources you created for this lab.
