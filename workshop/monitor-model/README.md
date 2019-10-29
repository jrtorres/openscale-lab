---
description: In this section we will enable and configure several model monitors.
---

# Monitor Model

Model monitors allow Watson OpenScale to capture information about the deployed model, evaluate transaction information and calculate metrics. There are several monitors that can be enabled:

* Fairness monitor scans your deployment for biases, to ensure fair outcomes across different populations.
* Quality monitor \(previously known as the accuracy monitor\) lets you know how well your model predicts outcomes.
* Drift monitor 
* Explainability

## Data sets

For many of these monitors, OpenScale requires all transactions \(input/request and output/response information\) going to the deployed models to be logged as payload records in the OpenScale data mart.

{% hint style="info" %}
For this lab since our model is deployed in Watson Machine Learning, the scoring payload is automatically sent to Watson OpenScale when you score the model
{% endhint %}

Some monitors also require feedback data. You must upload feedback data to the Watson OpenScale service on a regular basis to ensure that your model takes into account up-to-date data that may indicate changes in the context of your predictive application. 

{% hint style="info" %}
**Note**: We are using the python client to interact with Watson OpenScale. The configuration down below can also be accomplished through the web interface or the REST APIs.
{% endhint %}

