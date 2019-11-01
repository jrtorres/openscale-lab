---
description: >-
  We can add some data to the OpenScale dashboard to emulate the model being in
  production for some time.
---

# \[Optional\] Load Historical Data

### Run Historical Data

### 1.1 Open Notebook

* In [Watson Studio](https://dataplatform.cloud.ibm.com), select the project that you previously imported and click on the 'Assets' tab on the top of the project page.
* Under the 'Notebooks' section, _**Click**_ on the _**'dataload-queries-monitortriggers'**_ notebook and then click on the pencil icon to enable you to edit / run the notebook.

![](.gitbook/assets/screen-shot-2019-11-01-at-12.00.03-am.png)

### 1.2 Update Credentials

After the notebook environment starts up, scroll down to the section titled _**'Configure Service Credentials'**_.  Copy and Paste the Cloud API Key and Watson Machine Learning credentials that you saved to a text editor earlier.

![](.gitbook/assets/screen-shot-2019-10-28-at-12.30.46-am.png)

### 1.3 Run Notebook

* Go back to the first cell in the notebook and run **just the cells in section 1 and 2 of the notebook**. The other cells in section 3 and 4 are for reference. You can run the cells individually by clicking on each cell and then click the `Run` button at the top of the notebook. 

{% hint style="info" %}
While the cell is running, an asterisk \(`[*]`\) will show up to the left of the cell. When that cell has finished executing a sequential number will show up. Generally, you want to wait until the cell finished executing before running the subsequent cells
{% endhint %}

## Explore the Watson OpenScale UI

Go back to the OpenScale dashboard and you can see the graphs now have data points from the past 7 days. 

* Open the [Watson OpenScale dashboard](https://aiopenscale.cloud.ibm.com). 
* When the dashboard loads, _**Click**_ on the _**'Model Monitors'**_  tab and you will see the one deployment you configured in the previous section.
* Click through the different graphs for fairness, quality, and performance

![](.gitbook/assets/screen-shot-2019-11-01-at-12.45.34-am.png)

