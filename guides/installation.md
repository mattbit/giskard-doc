# Installation

{% hint style="info" %}
To install giskard, you need

* ``[`git`](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)``
* ``[`docker`](https://docs.docker.com/get-docker/)``
* ``[`docker`-`compose`](https://docs.docker.com/compose/install/)``
{% endhint %}

## Installation

#### To start Giskard locally run the following commands

```shell
git clone https://github.com/Giskard-AI/giskard.git
cd giskard
docker-compose up -d
```

once the docker-compose starts all of the modules you'll be able to open Giskard at

{% hint style="info" %}
[**http://localhost:19000/**](http://localhost:19000)****
{% endhint %}

The default credentials are

{% hint style="info" %}
Login: **`admin`**

Password: **`admin`**
{% endhint %}

## Update

#### In order to upgrade Giskard to the latest version please run the following in your Giskard distribution directory

```shell
git pull
docker-compose pull && docker-compose up -d
```

You're all set to try Giskard in action, upload your first model by following the [upload-your-model.md](upload-your-model.md "mention") tutorial.
