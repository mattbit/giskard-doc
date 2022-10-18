---
description: Easily execute your model in your Python environement
---

# Execute your model in your environment

If your ML model requires custom ML libraries or versions, you can test and inspect your model directly in your working Python environment. To do that, you will only need to open a secured connection between your working Python environment (notebook, Python IDE, etc) and the Giskard platform you've installed.&#x20;

Here are the steps to open the connection:

### Install Giskard

Run the following commands to install **the dev version** of Giskard on your server:

```bash
git clone https://github.com/Giskard-AI/giskard.git
cd giskard
TAG=dev docker-compose up -d --force-recreateInstall Giskard
```

{% hint style="info" %}
The requirements to execute the above lines (git and docker), can be found [here](./).
{% endhint %}

### Open a connection from your notebook to Giskard

If Giskard has been installed locally, you can open a connection from your notebook by executing

```python
!pip install giskard==1.7.0a3
!giskard worker start -d
```

{% hint style="info" %}
By default, `giskard worker start` opens a connection to the Giskard instance installed on `localhost`. If Giskard **is not installed locally**, please specify the IP address (and a port in case a custom port is used). For example:

`giskard worker start -h 192.158.1.38`
{% endhint %}

### Upload your model to Giskard

To upload your model, you have first to open a project

```
from giskard import GiskardClient

url = "http://localhost:19000" #if Giskard is installed locally (for installation, see: https://docs.giskard.ai/start/guides/installation) 
token = "YOUR GENERATED TOKEN" #you can generate your API token in the Admin tab of the Giskard application (for installation, see: https://docs.giskard.ai/start/guides/installation) 
client = GiskardClient(url, token)

project = client.create_project("project_key", "PROJECT_NAME", "DESCRIPTION") #Choose the arguments you want. But "project_key" should be unique and in lower case
#If your project is already created use project = client.get_project("existing_project_key")!pip install giskard==1.7.0a3
```

Then, you can use the standard `upload_model_and_data` function as described [here](../upload-your-model/#3.-upload-a-model-and-a-dataset).

## Example

Here is an example of the whole process of model upload after the local installation of Giskard

```python
!giskard worker start -d #If your giskard has been installed locally. Otherwise use giskard worker start -d -h 192.158.1.38

from giskard import GiskardClient

client = GiskardClient(url, token)

#If you're creating your project for the first time
credit_scoring = client.create_project("credit_scoring", "Credit scoring project", "Predict the default probabilities of a credit demand")

#If your project is already created use 
#project = client.get_project("credit_scoring")

credit_scoring.upload_model_and_df(
    prediction_function=clf.predict_proba,
    model_type='classification',
    df=test_data,
    column_types={
        'credit_id':'category',
        'credit_amount':'numeric',
        'credit_category':'category',
        'credit_application':'text',
        'Is_default': 'category'
        },
    target = 'Is_default',
    feature_names=['credit_amount','credit_category','credit_application'],
    classification_labels=['Not default','Default']
    )
```
