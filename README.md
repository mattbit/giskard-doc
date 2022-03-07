# 🤓 Giskard

![](.gitbook/assets/logo\_50.jpg)

{% hint style="success" %}
Giskard empowers AI teams to create **better AI models.**\
\
We are building the first <mark style="background-color:orange;">open-source</mark> **Quality Assurance** platform that automates inspection, testing & monitoring of AI models across platforms, from prototype to production.
{% endhint %}

* <mark style="background-color:orange;">**Reduce risks**</mark>: Insuring yourself against business incidents caused by AI bugs
* <mark style="background-color:orange;">**Save time**</mark>: Investing in quality will save you time by reducing waste in AI pipelines
* <mark style="background-color:orange;">**Increase trust**</mark>: Aligning your tech and business stakeholders leads to better outcomes

{% embed url="https://github.com/Giskard-AI/giskard" %}

## Installation

```batch
git clone https://github.com/Giskard-AI/giskard.git
cd giskard
docker-compose build --parallel && docker-compose up -d
```

Yes, that's all!  Then start inspecting some models at [**http://localhost:19000/**](http://localhost:19000)****

{% hint style="info" %}
**login**: admin  **password**: admin
{% endhint %}

## Example

### 1. Collect feedback on your model

![](<.gitbook/assets/Give feedbcack.jpg>)

### 2. Discuss and analyze feedback

![](<.gitbook/assets/Discussion (1).jpg>)

### 3. Turn feedback into tests

![](.gitbook/assets/Test.jpg)

## Guides: Jump right in

Follow our handy guides to get started on the basics as quickly as possible:

{% content-ref url="guides/installation.md" %}
[installation.md](guides/installation.md)
{% endcontent-ref %}

{% content-ref url="guides/upload-your-model.md" %}
[upload-your-model.md](guides/upload-your-model.md)
{% endcontent-ref %}

{% content-ref url="guides/review-your-model.md" %}
[review-your-model.md](guides/review-your-model.md)
{% endcontent-ref %}

{% content-ref url="guides/create-tests-from-your-review.md" %}
[create-tests-from-your-review.md](guides/create-tests-from-your-review.md)
{% endcontent-ref %}

## License

This project is licensed under the terms of the `Apache Software License 2.0` license. See [LICENSE](https://github.com/Giskard-AI/ai-inspector/blob/main/LICENSE) for more details.
