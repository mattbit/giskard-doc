---
description: Easily install Giskard in AWS using our AMI, in 3 steps
---

# Installation in AWS

### 1. Initialize EC2 instance

* In the AWS console, go to the service EC2 and select one of the following zones: N. Virginia (`us-east-1`), Paris (`eu-west-3`), or Singapore (`ap-southeast-1`)
* Launch an EC2 instance

### 2. Configure your EC2 instance

* **Image selection**: In the search bar for AMI, type "Giskard" and select either `giskard-latest` or the specific Giskard version you want
* **Instance type**: We recommend you to choose `t2.large` instance type
* **Key pair**: Choose your usual key pair. If you don't have one, go to the [Amazon document](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/create-key-pairs.html) to create the right one
* **Network settings**: Make sure to tick HTTP to be able to access the application. And SSH too if you need to access the machine.
* **Storage**: Choose a minimum of 30 Gigs of SSD (this will mainly depend on the size of your datasets)

### 3. Launch instance and open Giskard

* **Launch instance**: Click on Launch instance to create the instance
* **Get your IP address**: Click in the ID of the instance you just created and copy its IP address
* Go to **`http://<your IP address>`** in your browser
* The user id is `admin` and the password is `admin`

That's it, you are now ready to use Giskard in AWS! Now you can start [uploading a model](../upload-your-model/)!

{% hint style="warning" %}
If you have an error message when you log in, you may need to wait one or two minutes for the Giskard backend to start!
{% endhint %}

{% hint style="info" %}
You can stop the instance and restart it when you need to save your AWS compute costs. However, note that the **IP address will not necessarily be the same**. So make sure you copy it again from the instance configuration page when it's launched.
{% endhint %}

