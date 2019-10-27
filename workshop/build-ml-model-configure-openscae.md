---
description: >-
  In this section, we will build/deploy a machine learning model that predicts
  credit risk and set up OpenScale to monitor the model.
---

# Build Model & Configure Watson OpenScale

{% hint style="info" %}
Although this lab is showing the end to end process of building, deploying, and monitoring/managing a machine learning model. Models do not have to be built in Watson Studio nor deployed to Watson Machine Learning to be monitored with OpenScale.   Watson OpenScale is an open platform that can manage production models in a variety of environments. See resources in the [Wrap-up section ](wrap-up.md)for examples of other models or deployment environments. 
{% endhint %}

## Model Creation Notebook

The first notebook in the project you imported will create a model and configure OpenScale.

### Open Notebook

In [Watson Studio](https://dataplatform.cloud.ibm.com), select the project that you previously imported and click on the 'Assets' tab on the top of the project page.

![](.gitbook/assets/screen-shot-2019-10-27-at-4.00.26-pm.png)

_**Click**_ on the model creation/configuration notebook \(_notebook name is prefixed with "1-"_ \) and then click on the pencil icon to enable you to edit / run the notebook.

{% hint style="info" %}
_The project may have multiple model creation notebooks that build models using different libraries / algorithms. For this lab, select the Spark model - 1-sparkmlmodel-wos-configuration._
{% endhint %}

![](.gitbook/assets/screen-shot-2019-10-27-at-4.41.07-pm.png)

### Update Credentials

After the notebook environment starts up, scroll down to the section titled _**'Service Credentials'**_.  Copy and Paste the Watson Machine Learning service credentials and the Cloud API Key that you saved to a text editor earlier.

![](.gitbook/assets/screen-shot-2019-10-27-at-5.03.11-pm.png)

### Run Notebook

Go back to the first cell in the notebook and run the notebook. You can run cells individually by clicking on each cell and then click the `Run` button at the top of the notebook. 

{% hint style="info" %}
While the cell is running, an asterisk \(`[*]`\) will show up to the left of the cell. When that cell has finished executing a sequential number will show up. Generally, you want to wait until the cell finished executing before running the subsequent cells.

Alternatively, you can elect to run all the cells by clicking the **'Run All'** option under the **'Cell'** menu
{% endhint %}

## Explore the Watson OpenScale UI

Now that you have created a machine learning model and configured OpenScale, you can utilize the OpenScale dashboard to monitor the model.



