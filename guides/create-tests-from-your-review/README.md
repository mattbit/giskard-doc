---
description: How to get started with Automated Machine Learning testing
---

# Test your ML model

Giskard enables you to create test suites on AI models. It provides presets of tests so that you design and execute your tests in no time. Here are the 3 steps to create and execute tests: \


## 1. Create an automatic test suite

To create tests, you need first to create a test suite, here are the 3 steps:

&#x20;1\. Go to the test suite tab in Giskard and click on the button "create test suite"

![](<../../.gitbook/assets/Screenshot 2022-07-18 at 09.21.16.png>)

2\. Choose the inputs parameters of your test suite:

* **Test suite name**: A test suite name
* **Model**: The model that the test suite will test
* **Actual dataset**: A test dataset used to execute the tests inside the test suite. It could be any datasets that you've uploaded with [#3.-upload-a-model-and-a-dataset](../upload-your-model.md#3.-upload-a-model-and-a-dataset "mention")
* **Reference dataset (optional)**: An optional reference dataset used for the drift testing to assess the changes with the Actual dataset. It could be any datasets that you've uploaded with [#3.-upload-a-model-and-a-dataset](../upload-your-model.md#3.-upload-a-model-and-a-dataset "mention")\


3\. Toggle on "the automatic test" to automatically pre-compute a batch of tests that is preloaded by Giskard according to your case.

## 2. Customize your tests inside your test suite

Giskard proposes 5 families of tests that you can customize:

* **Metamorphic testing:** Test if your model outputs behave as expected before and after input perturbation
* **Heuristics testing**: Test if your model output respect some business rules
* **Performance testing**: Test if your model performance is sufficiently high within some particular data slices
* **Data drift testing**: Test if your features don't drift between the reference and actual dataset
* **Prediction drift testing**: Test the absence of concept drift inside your model

![](<../../.gitbook/assets/Screenshot 2022-07-18 at 10.29.32.png>)

## 3. Read the test results

Once you have run the test you designed, Giskard provides the results (PASS or FAIL) of all your tests. You can then click on the test and further investigate the outputs of the tests to understand the issue.

![](<../../.gitbook/assets/Screenshot 2022-07-18 at 10.23.02.png>)

## Troubleshooting[​](https://docs.airbyte.com/deploying-airbyte/on-aws-ec2#troubleshooting)

If you encounter any issues, join our [**Discord**](https://discord.gg/fkv7CAr3FE) on our #support channel. Our community will help!&#x20;
