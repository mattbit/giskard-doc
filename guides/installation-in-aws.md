# Installation in AWS

You can easily install Giskard in AWS using our AMI. To do that, you can follow these 3 steps:

### 1. Initialize EC2 instance

* Go to the AWS console and select one of the following zones: Virginia, Paris, or Singapore
* Launch an EC2 instance

### 2. Configure your EC2 instance

* **Image selection**: In the search bar for AMI, type "Giskard" and select either `giskard-latest` or the specific Giskard version you want
* **Instance type**: We recommend you to choose `t2.large` instance type
* **Key pair**: Choose your usual key pair. If you don't have one, go to the [Amazon document](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/create-key-pairs.html) to create the right one
* **Network settings**: Click on HTTPS and HTTP
* **Storage**: Choose a minimum of 30 Gigs of SSD (this will mainly depend on the size of your databases)

### 3. Launch instance and open Giskard

* **Launch instance**: Click on Launch instance to create the instance
* **Get your IP address**: Click in the ID of the instance you just created and copy its IP address
* Go to **`http://<your IP address>`**` ``` in your browser
* The user id is `admin` and the password is `admin`

That's it, you are now ready to use Giskard in AWS! Now you can start [uploading a model](upload-your-model.md)!

{% hint style="warning" %}
If you have an error message when you log in, you may need to wait one or two minutes for Giskard backend to start!
{% endhint %}

