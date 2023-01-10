---
description: >-
  How to install Giskard on your machine, set up your Python backend and upgrade
  Giskard
---

# Installation & upgrade

{% hint style="success" %}
**Cloud installation:**

* To install Giskard in **AWS**, please go to __ [installation-in-aws.md](installation-in-aws.md "mention")__
* To install Giskard in **GCP**, please go to [installation-in-gcp.md](installation-in-gcp.md "mention")
{% endhint %}

{% hint style="info" %}
## Requirements

To install Giskard, you need a **Linux** or **macOS** machine with:

* `By default Giskard uses 2 TCP ports: 19000 and 40051, make sure they're open on the machine where Giskard is installed`
* `git (`[`download`](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)`)`
*   `docker (`[`download`](https://docs.docker.com/engine/install/debian/)`).`For an easy installation of Docker you can execute:&#x20;

    ```bash
     sudo curl -fsSL https://get.docker.com -o get-docker.sh
     sudo sh get-docker.sh
    ```
{% endhint %}

Run the following commands to install Giskard on your server

```shell
git clone https://github.com/Giskard-AI/giskard.git
cd giskard
docker compose pull && docker compose up -d --force-recreate --no-build
```

{% hint style="warning" %}
* If you have an error because of the rate limit (**`toomanyrequests: Rate exceeded`**), please re-execute the docker-compose command line once again.
* If`compose`is not found, you may have an older version of docker, so you'll need to use**`docker-compose`** instead of `docker compose.`Alternatively, you can also upgrade your docker version
{% endhint %}

Once the docker-compose starts all the modules, you'll be able to open Giskard at [http://localhost:19000/](http://localhost:19000/)

{% hint style="warning" %}
Since the backend container may take some minutes to load, please wait a bit and refresh the webpage [http://localhost:19000/](http://localhost:19000/)
{% endhint %}

To log in, the default credentials are **Login: admin / Password: admin**

You're all set to try Giskard in action. Upload your first model by following the [upload-your-model](../upload-your-model/ "mention") tutorial.

## Upgrade Giskard to the latest version

In order to upgrade Giskard to the latest version, please run the following in your Giskard distribution directory

```shell
git pull
docker compose down && docker compose pull && docker compose up -d --force-recreate --no-build
```

{% hint style="danger" %}
* The browser may keep using an old version of Giskard UI due to caching. If there are issues after running an upgrade try to **hard refresh** Giskard page by pressing\
  `Ctrl + Shift + R` or  `Command + Shift + R`&#x20;
* If you installed in Giskard additional **Python libraries** or a **new Python version**, you will need to reinstall them. Please refer to [configuration](../configuration.md).
{% endhint %}

## Troubleshooting[​](https://docs.airbyte.com/deploying-airbyte/on-aws-ec2#troubleshooting)

If you encounter any issues, join our [**Discord**](https://discord.gg/fkv7CAr3FE) on our #support channel. Our community will help!&#x20;
