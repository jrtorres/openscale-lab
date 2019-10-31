---
description: We will be running this lab in the Cloud.
---

# Lab Environment Setup

In this lab, you will be deploying the credit risk machine learning model from Watson Studio to the Watson Machine Learning service to get an online scoring endpoint. You will then enable and explore the different model characteristics you can monitor using Watson OpenScale.  

![](../.gitbook/assets/architecture.png)

You will work in a Jupyter notebook on Watson studio to interact with the Machine Learning and OpenScale services.

As you enable and configure different monitoring capabilities, you will also use the Watson OpenScale web interface to visualize metrics being captured/calculated.

{% hint style="info" %}
The topology we are using in this lab is just one approach that is supported. See the [Wrap-up section](../wrap-up.md) for resources on other deployment options.
{% endhint %}

{% hint style="info" %}
In this lab we are programmatically interacting with with Watson OpenScale and Watson Machine Learning through python client SDKs. This is not a requirement as these services provide web interface and REST APIs.
{% endhint %}

