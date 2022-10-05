---
description: Easily install Giskard in GCP
---

# Installation in GCP

1. Create a project. You can follow the instructions [here](https://cloud.google.com/resource-manager/docs/creating-managing-projects?utm\_source=codelabs\&utm\_medium=et\&utm\_campaign=CDR\_sar\_aiml\_vertexio\_\&utm\_content=-) to create a project in GCP
2. Create the firewall rule:
   1. Go to VPC network
   2. Click “setup firewall rules” on the bottom of the page, and check if the rule does not already exist. If the rule already exists, skip steps 3 and 4 and go to the next section.
3. Start your VM (or notebook), and open a terminal,
4. create the firewall rule with the following command: ​

```jsx
gcloud compute firewall-rules create rule_name --allow tcp:port --source-tags=rule_tag
```

​ for instance, you can create the tensorboard rule, named `tensorboard`, and applied to the tag `tensorboard`, which forwards the TCP port through the port 8008: ​ `gcloud compute firewall-rules create tensorboard —allow tcp:19000 —source-tags=tensorboard`

1. Go to VM instances in Compute Engine and create a VM instances
2. In the configuration of your VM :
   1. In the firewall section, allow http and https traffic
   2. In advanced options, go to networking and add the giskard tag

![](<../../.gitbook/assets/image (1).png>)
