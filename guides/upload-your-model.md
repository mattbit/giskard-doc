# Upload your model

## Prerequisites

To upload the model you want to inspect, you need:

* A model. For example, a _scikit-learn, Tensorflow, HuggingFace, catboost_ python functions
* A pandas dataframe composed of the examples you want to inspect. For example, it could be your test dataset or a dataset composed of some wrong predictions of your model
* The Giskard's platform. To install it, check [installation.md](installation.md "mention")

## Steps to upload your model

### 1. Install Giskard library

In order to upload models and datasets to Giskard, you'll need to install the library giskard:

```shell
pip install giskard
```

### 2. Create a new project or load an existing project

To create a new project or load an existing one, run the code below in your Python environment:

```python
from giskard.giskard_client import GiskardClient

url = "http://localhost:19000" #if Giskard is installed locally (for installation, see: https://docs.giskard.ai/start/guides/installation) 
token = "YOUR GENERATED TOKEN" #you can generate your API token in the Admin tab of the Giskard application (for installation, see: https://docs.giskard.ai/start/guides/installation) 
client = GiskardClient(url, token)

project = client.create_project("PROJECT_KEY", "PROJECT_NAME", "DESCRIPTION"). 
#If your project is already created use project = client.get_project("EXISTING_PROJECT_KEY")
```

{% hint style="info" %}
If you want to use an **existing project**, use `project=client.get_project("EXISTING_PROJECT_KEY")`to load the existing project, then use:

* `upload_model` to **upload a new version of the model** you want to inspect/test
* `upload_dataset` to **upload a new dataset** that you want to apply to your existing model

For more details about the arguments of these functions, see our [Github repo](https://github.com/Giskard-AI/giskard-client/blob/main/giskard/project.py).
{% endhint %}

### 3. Upload a model and a dataset

Apply the upload\_model\_and\_df to the project using the following arguments:

| Argument                   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Type                                                                    |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `prediction_function`      | <p>The model you want to predict. It could be <strong>any</strong> Python function with the signature of </p><ul><li><a href="https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html#sklearn.linear_model.LogisticRegression.predict_proba">predict_proba</a> for classification. It returns the classification <strong>probabilities</strong> for all the classification labels</li><li><a href="https://github.com/scikit-learn/scikit-learn/blob/baf828ca1/sklearn/linear_model/_base.py#L348">predict</a> for regression. </li></ul><p>If you have preprocessing steps, <strong>wrap the whole prediction pipeline:</strong> all the preprocessing steps (categorical encoding, scaling, etc.) <strong>+</strong> ML predict_proba function.</p> | <p>Callable[</p><p>[pd.DataFrame], Iterable[Union[str, float, int]]</p> |
| `model_type`               | <ul><li>"classification" for classification model</li><li>"regression" for regression model</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | str                                                                     |
| `df`                       | <p>A <strong>Pandas dataframe</strong> that contains some data examples that might interest you to inspect (test set, train set, production data). Some important remarks:</p><ul><li><code>df</code> can contain more columns than the features of the model such as the <strong>actual ground truth variable,</strong> sample_id, metadata, etc. <strong></strong> </li><li><code>df</code> should be raw data that comes <strong>before</strong> all the preprocessing steps</li></ul>                                                                                                                                                                                                                                                                                                    | Pandas dataframe                                                        |
| `column_types`             | A dictionary of column names and their types (`numeric`, `category` or `text`) for all columns of `df`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Dict\[str, str]                                                         |
| `target`                   | The column name in `df` corresponding to the **actual target variable** (ground truth).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | str                                                                     |
| `feature_names`            | A list of the feature names of the model you uploaded with `prediction_function.` Make sure these features are contained in `df`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | List\[str]                                                              |
| `classification_labels`    | <p>The classification labels of your prediction when <code>prediction_task</code>="classification". Some important remarks:</p><ul><li>If <code>classification_labels</code> <em></em> is a list of <strong>n</strong> elements, make sure <code>prediction_function</code> is also returning <strong>n</strong> probabilities</li><li>Make sure <code>classification_labels</code> returns the labels in the same order as the output of <code>prediction_function</code></li></ul>                                                                                                                                                                                                                                                                                                         | Optional\[List\[str]] = None                                            |
| `classification_threshold` | The probability threshold in the case of a binary classification model. By default, it's equal to 0.5                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Optional\[float] = 0.5                                                  |
| `model_name`               | The name of the model you uploaded                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Optional\[str]                                                          |
| `dataset_name`             | The name of the dataset you uploaded                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Optional\[str]                                                          |

{% hint style="warning" %}
It's better to upload `prediction_function` as a function that **wraps the whole** prediction pipeline: all the preprocessing steps (categorical encoding, etc.) + ML prediction. This is key for a robust and interpretable inspection stage!
{% endhint %}

{% hint style="danger" %}
Make sure that `prediction_function`(`df`\[feature\_names]) gets executed **without an error**. __ This is the only requirement to upload a model on Giskard!
{% endhint %}

## Examples

```python
client = GiskardClient(url, token)
credit_scoring = client.create_project("Credit_scoring", "Credit scoring", "Predict the default probabilities of a credit demand")

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

{% hint style="info" %}
**Example notebooks:**

* You can download an **example notebook** [here](https://github.com/Giskard-AI/giskard/blob/main/backend/demo-notebook/notebook/German\_credit\_scoring\_giskard.ipynb) to execute it in your working environment
* To get started with Giskard as fast as possible we've included a demo python notebook in the platform with all the requirements on [**http://localhost:19000/jupyter**](http://localhost:19000/jupyter) **** (accessible after the [installation.md](installation.md "mention")). Feel free to modify it to adapt it to your case! &#x20;
{% endhint %}

Now you uploaded your model, let's [review-your-model.md](review-your-model.md "mention")
