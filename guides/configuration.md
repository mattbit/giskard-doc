---
description: >-
  How to configure your Giskard application: Python version, Python version,
  email notifications and API tokens
---

# Configuration

## Install additional Python libraries

If you need specific Python libraries that are not pre-installed in Giskard and that are available in PyPI, git, locally etc., you can install them manually in Giskard.&#x20;

To do so, please follow these steps:

1.  Change the file `giskard/giskard-ml-worker/ml-worker.dockerfile`. To do that, here are the steps:

    1. &#x20;From your Giskard repo, type `vim giskard-ml-worker/ml-worker.dockerfile`
    2. Below the line `Add your python dependencies here`, write the following line:  (press `i` to edit in the _vim_ text editor).



    ```bash
    RUN poetry add <YOUR LIBRARY> #With Poetry you can add libraries hosted locally, Github, PyPI, etc. See: https://python-poetry.org/docs/cli/#add etc
    ```



    3\. Save and quit the text editor (`:wq` in the _vim_ editor)
2. Then rebuild your docker images using the following command lines

```bash
docker-compose -f docker-compose.dev.yml -f docker-compose.yml build ml-worker
docker-compose stop ml-worker && docker-compose up ml-worker -d
```

## Install a new Python version

Giskard application is working on Python 3.7, if you use another Python version (3.9 or 3.10 for instance), please follow these steps:

1. Change Python version in `giskard/giskard-ml-worker/ml-worker.dockerfile`. To do that, here are the steps:
   1. &#x20;From your Giskard repo, type `vim giskard-ml-worker/ml-worker.dockerfile`
   2. Replace `Python3.7` in the first line by your Python version (press `i` to edit in the _vim_ text editor). You can find the Python images according to your Python version in this [dockerhub link](https://hub.docker.com/\_/python)
   3. Save and quit the text editor (`:wq` in the _vim_ editor)

2\. Then rebuild your docker images using the following command lines

```bash
docker-compose -f docker-compose.dev.yml -f docker-compose.yml build ml-worker
docker-compose stop ml-worker && docker-compose up ml-worker -d
```

## Email notifications

Giskard can send email notifications about different events like inspector feedbacks or user invitation to the platform.

To configure this feature SMTP server credentials should be provided at startup through environment variables

| Environment variable name | Purpose                                 |
| ------------------------- | --------------------------------------- |
| GISKARD\_MAIL\_HOST       | SMTP server address                     |
| GISKARD\_MAIL\_PORT       | SMTP port, 587 by default               |
| GISKARD\_MAIL\_USERNAME   |                                         |
| GISKARD\_MAIL\_PASSWORD   |                                         |
| GISKARD\_MAIL\_BASEURL    | Publicly available Giskard instance URL |

## Backend JWT secret. Persistent user sessions.

Giskard authentication is based on [JWT tokens](https://jwt.io/). These tokens are issued by Giskard backend based on a JWT secret key.

To reinforce security there's no default value of the secret key, whenever the backend starts it generates one automatically. However it means that users' sessions are invalidated and they have to re-login.&#x20;

For production instances, it's preferred to keep user sessions alive no matter whether the server was rebooted or not. In this case, the JWT secret can be set from the outside by specifying `GISKARD_JWT_SECRET` environment variable. Its value should contain a base64 encoded bytes sequence of at least 128 bytes.

The following script can generate and store a secret key of 256 bytes:

```bash
# for zsh
echo export GISKARD_JWT_SECRET=`openssl rand -base64 256 | tr -d '\n'` >> ~/.zshrc

# for bash
echo export GISKARD_JWT_SECRET=`openssl rand -base64 256 | tr -d '\n'` >> ~/.bashrc
```

## Troubleshooting[​](https://docs.airbyte.com/deploying-airbyte/on-aws-ec2#troubleshooting)

If you encounter any issues, join our [**Discord**](https://discord.gg/fkv7CAr3FE) on our #support channel. Our community will help!&#x20;

## [​](https://docs.airbyte.com/deploying-airbyte/on-aws-ec2#troubleshooting)
