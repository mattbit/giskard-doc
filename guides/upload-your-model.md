# Upload your model

### Prerequisites

To upload the model you want to inspect, you need:

* A model. For example, a scikit-learn predict\_proba function
* A pandas dataframe composed of the examples you want to inspect. For example, it could be your test dataset or a dataset composed of some wrong predictions of your model
* The Giskard's platform. To install it, check [installation.md](installation.md "mention")

{% hint style="info" %}
**Demo notebooks:**

To get started with Giskard as fast as possible we've included a demo python notebook in the platform with all the requirements on [**http://localhost:19000/jupyter**](http://localhost:19000/jupyter) **** (accessible after the [installation.md](installation.md "mention")). Feel free to modify it to adapt it to your case! &#x20;



You can also download a demo notebook [here](https://github.com/Giskard-AI/giskard/blob/main/backend/demo-notebook/notebook/German\_credit\_scoring\_giskard.ipynb) to execute it in your working environment
{% endhint %}

Here are the three steps to inspect your model:

### 1. Load ai-inspector

In order to upload models and datasets to Giskard, you'll need to install the library ai-inspector in your Python **3.7** environment (see the [installation.md](installation.md "mention")):

```python
pip install ai-inspector
```

{% hint style="info" %}
If you have another version of Python, create a [virtual 3.7 Python environment](https://stackoverflow.com/questions/52816156/how-to-create-virtual-environment-for-python-3-7-0).
{% endhint %}

### 2. Create a ModelInpsector object

`ModelInpector` Python class has the following argument

| Argument                   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Type                                                                    |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `prediction_function`      | <p>The model you want to predict. It could be any Python function with the signature of </p><ul><li><a href="https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html#sklearn.linear_model.LogisticRegression.predict_proba">predict_proba</a> for classification</li><li><a href="https://github.com/scikit-learn/scikit-learn/blob/baf828ca1/sklearn/linear_model/_base.py#L348">predict</a> for regression</li></ul> | <p>Callable[</p><p>[pd.DataFrame], Iterable[Union[str, float, int]]</p> |
| `prediction_task`          | <ul><li>"classification" for classification model</li><li>"regression" for regression model</li></ul>                                                                                                                                                                                                                                                                                                                                                         | str                                                                     |
| `input_types`              | A dictionary of feature names with their types:`numeric`, `category` or `text`                                                                                                                                                                                                                                                                                                                                                                                | Dict\[str, str]                                                         |
| `classification_threshold` | The probability threshold in the case of a binary classification model. By default, it's equal to 0.5                                                                                                                                                                                                                                                                                                                                                         | Optional\[float] = 0.5                                                  |
| `classification_labels`    | The classification labels of your target variable in the case of classification task                                                                                                                                                                                                                                                                                                                                                                          | Optional\[List\[str]] = None                                            |

{% hint style="info" %}
It's better to upload `prediction_function` as a function that wraps the **whole** prediction pipeline: all the preprocessing steps (categegorical encoding, etc.) + ML prediction. This is key for a robust and interpretable inspection stage!
{% endhint %}

### 3. Inspect a dataset

To inspect the model, you need to apply it to some data examples that might interest you to inspect. For example, it could be either:

* Your test or train set
* A sub-population of your data
* A dataset composed of errors of your model (false positive, false negatives, etc.)

{% hint style="info" %}
This dataset might contain columns that are even not features of the model! The only requirement is that it should be a pandas dataframe that can be executed as an argument of the `prediction_function.`&#x20;
{% endhint %}

To inspect the model with the dataframe, you need the`inspect` method from the `ModelInpector` class:

![](../.gitbook/assets/widget.jpg)

Then you need to choose,

* **Target column**: it's the target variable in your dataset
* **Giskard UR**L: if Giskard is hosted locally, it should be `http://localhost:19000`
* **Project key**: choose a project name you like. You can upload different model versions and datasets in the same project
* **API token**: you can generate your API token in the Admin tab of Giskard (login: `admin` ;  password: `admin` at `http://localhost:19000` if hosted locally)

{% hint style="info" %}
If you don't want to use the widget or for custom upload, you can use the`upload_model` __ `upload_df`, or `upload_and_df` __ methods from `ModelInpector`_._ For more detail, check the [_ModelInspector_](https://github.com/Giskard-AI/ai-inspector/blob/main/ai\_inspector/inspector.py#L34) __ class
{% endhint %}

## Example

```python
from ai_inspector import ModelInspector

inspector = ModelInspector(
    prediction_function = clf.predict_proba,
    prediction_task = "classification",
    input_types = {
               'account_check_status':"category", 
               'duration_in_month':"numeric",
               'credit_history':"category",
               'purpose':"category",
               'credit_amount':"numeric"
               }
    classification_labels = ["Not default","Default"],
)

inspector.inspect(credit)
```

Now you uploaded your model, let's [review-your-model.md](review-your-model.md "mention")
