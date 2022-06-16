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

## Install  new Python library

If you need custom Python libraries that are not pre-installed in Giskard:

1. Go to `ml-worker/pyproject.toml`
   1. If the library you want to install is written as a comment in the list, just uncomment it
   2. If the library you want to install is not in the list, just add it to the list
2. From the root of the Giskard directory run

```
docker-compose stop backend
docker-compose up --build backend
```
