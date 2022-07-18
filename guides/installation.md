# Installation

{% hint style="info" %}
## Requirements

To install Giskard, you need

* `git (`[`download`](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)`)`
* `docker (`[`download`](https://docs.docker.com/get-docker/)`)`
* `docker`-`compose (`[`download`](https://docs.docker.com/compose/install/)`)`
{% endhint %}

Run the following commands to install Giskard in your server

```shell
git clone https://github.com/Giskard-AI/giskard.git
cd giskard
docker-compose up -d --force-recreate
```

once the docker-compose starts all of the modules you'll be able to open Giskard at

{% hint style="info" %}
[**http://localhost:19000/**](http://localhost:19000/)****
{% endhint %}

The default credentials are

{% hint style="info" %}
Login: **`admin`**

Password: **`admin`**
{% endhint %}

You're all set to try Giskard in action, upload your first model by following the [upload-your-model.md](upload-your-model.md "mention") tutorial.

## Upgrade Giskard to the latest version

In order to upgrade Giskard to the latest version, please run the following in your Giskard distribution directory

```shell
git pull
docker-compose down && docker-compose pull && docker-compose up -d --force-recreate
```

## Install additional Python libraries

If you need specific Python libraries that are not pre-installed in Giskard and that are available in PyPI, git, locally etc., you can install them manually in Giskard. To do so, execute the following commands:

1. Go to `giskard/giskard-ml-worker/ml-worker.dockerfile`
2. Below the line `Add your python dependencies here` , write the following line:&#x20;

```bash
RUN poetry add <YOUR LIBRARY> #With Poetry you can add libraries hosted locally, Github, PyPI, etc. See: https://python-poetry.org/docs/cli/#add etc
```

&#x20; 3\. From the root of the Giskard directory run

```bash
docker-compose stop ml-worker
docker-compose -f docker-compose.dev.yml -f docker-compose.yml build ml-worker
docker-compose up ml-worker
```

## Install a new Python version

Giskard application is working on Python 3.7, if you use another Python version (3.9 or 3.10 for instance), please follow these steps:

1. Change Python version in `giskard/giskard-ml-worker/ml-worker.dockerfile`
2. Run the following command lines

```bash
docker-compose -f docker-compose.dev.yml -f docker-compose.yml build ml-worker
docker-compose down ml-worker && docker-compose up ml-worker -d
```

## Troubleshooting[​](https://docs.airbyte.com/deploying-airbyte/on-aws-ec2#troubleshooting)

If you encounter any issues, join our [**Discord**](https://discord.gg/fkv7CAr3FE) on our #support channel. Our community will help!&#x20;
