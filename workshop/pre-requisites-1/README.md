---
description: We will be running this lab in the Cloud.
---

# Lab Environment Setup

In this lab, you will be building the credit risk machine learning model in Watson Studio and then deploying that model to the Watson Machine Learning service to get an online scoring endpoint. You will then enable and explore the different model characteristics you can monitor using Watson OpenScale.  

You will work in a Jupyter notebook on Watson studio, which will use clients to interact with the Machine Learning and OpenScale services.

![](../.gitbook/assets/architecture.png)

As you enable and configure different monitoring capabilities, you will also use the Watson OpenScale web interface to visualize metrics being captured/calculated.

{% hint style="info" %}
The topology we are using in this lab is just one approach that is supported.

In this lab we are programmatically interacting with these services. We will be using the python client to interact with Watson OpenScale and Watson Machine Learning. This is not a requirement as these services provide web interface and REST APIs.
{% endhint %}

