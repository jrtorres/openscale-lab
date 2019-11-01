---
description: In this section we will enable and configure several model monitors.
---

# Monitor Model

Model monitors allow Watson OpenScale to capture information about the deployed model, evaluate transaction information and calculate metrics. There are several monitors that can be enabled:

* Fairness monitor scans your deployment for biases, to ensure fair outcomes across different populations.
* Quality monitor \(previously known as the accuracy monitor\) lets you know how well your model predicts outcomes.
* Drift monitor detects when the model drops in accuracy and/or starts receiving data inconsistent with how it was trained.
* Explainability provides transparency in models by allowing you to see what lead the model to make specific predictions.

## Data sets

For many of these monitors, OpenScale will make use of the following data:

* \(Optional\) Training data that was used to train the model.
* Transaction data \(input/request and output/response information\) going to the deployed models which is stored in the payload table of the data mart.
* Feedback data with labeled predictions to measure the effectiveness of predictions and when retraining is needed which is stored in the feedback table of the data mart.

{% hint style="info" %}
For this lab since our model is deployed in Watson Machine Learning, the scoring payload is automatically sent to Watson OpenScale and stored in its data mart when you score the model.
{% endhint %}

{% hint style="info" %}
To emulate the monitoring of a model in production, in addition to making scoring/prediction requests to the actual model, you will also inject historical data into the OpenScale data mart.
{% endhint %}

