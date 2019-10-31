---
description: >-
  Watson OpenScale can monitor the model deployments for fairness/bias and
  drift, as well as provide explanations for predictions.
---

# Fairness, Drift and Explainability

## 1. Fairness, Drift and Explainability Configuration

OpenScale helps organizations maintain regulatory compliance by tracing and explaining AI decisions across workflows, and intelligently detect and correct bias to improve outcomes. In this section we will enable the monitors in OpenScale. We could configure these monitors using the Jupyter notebook supplied in the project or through the OpenScale web interface. For this section, we will use the web interface.

{% hint style="info" %}
Feel free to open the notebook '_fairness-drift-explainability-monitors' to see how the monitors can be enabled programmatically._
{% endhint %}

### 1.1 Model Details

Before we configure the monitor, we will confirm the details of our model.

* Open the [Watson OpenScale dashboard](https://aiopenscale.cloud.ibm.com). 
* When the dashboard loads, _**Click**_ on the _**'Model Monitors'**_  tab and you will see the one deployment you configured in the previous section.

![](../.gitbook/assets/screen-shot-2019-10-30-at-9.16.41-pm.png)

* **Click** on **'Configure monitors'**   

![](../.gitbook/assets/screen-shot-2019-10-30-at-9.46.07-pm.png)

* Before we configure the fairness monitor, we will confirm the details of our model. **Click** on '**Model details**' on the left panel and then on the '**Begin**' button \(many of the parameters in the subsequent steps are pre-filled\).

![](../.gitbook/assets/screen-shot-2019-10-31-at-12.19.29-am.png)

* Some of the monitors will use the model training data. We have the option of providing the location of that training data for OpenScale to use or to gather the information needed locally and upload it. Select the '**Manual configure monitors'** tile and click the '**Next**' button.  ![](../.gitbook/assets/screen-shot-2019-10-31-at-12.32.04-am.png) 
* We already have the training data uploaded in a db2 instance and the connection information should be pre-filled. Click the 'Next' button
* On the 'Select your training table' panel, **click** the 'Next' button.   ![](../.gitbook/assets/screen-shot-2019-10-31-at-12.35.03-am.png) 
* On the 'Select the label column from the training data' panel,  'Risk' should be pre-selected as our label. **Click** the 'Next' button  ![](../.gitbook/assets/screen-shot-2019-10-31-at-12.38.22-am.png) 
* On the 'Select the features used to train the AI deployment', the all of the features should be pre-selected. **Click** the 'Next' button  ![](../.gitbook/assets/screen-shot-2019-10-31-at-12.40.48-am.png) 
* On the 'Select the text and categorical features', the non-numeric features should be pre-selected. **Click** the 'Next' button   ![](../.gitbook/assets/screen-shot-2019-10-31-at-12.43.23-am.png) 
* On the 'Select the deployment prediction column', the column where our models prediction is stored \('predictedLabel'\) should be pre-selected. **Click** the 'Next' button   ![](../.gitbook/assets/screen-shot-2019-10-31-at-12.45.45-am.png) 
* On the 'Select the prediction probability column', the column where our models prediction probabilities are stored \('probability'\) should be pre-selected. **Click** the 'Next' button 
* On the 'Select the transaction ID column \(optional\)', we will not be adding a transaction column at this point. **Click** the 'Next' button 
* Finally, on the 'Model details summary' panel, click the 'Save' button.  ![](../.gitbook/assets/screen-shot-2019-10-31-at-12.51.14-am.png) 
* Completing the model details will enable explainability.

### 1.2 Fairness Configuration

The fairness monitor scans the requests sent to your model deployment \(i.e the payload\) to ensure fair outcomes across different populations. In this lab, the credit risk model uses a training dataset that contains 20 attributes about each loan applicants. Two of those attributes - 'Sex' and 'Age' - are the ones we will monitor for bias.

* Continuing from the configure monitors page, **Click** on 'Fairness' on the left panel and then on the 'Begin' button.

![](../.gitbook/assets/screen-shot-2019-10-31-at-1.07.22-am.png)

* The first thing we define when configuring fairness, is what outcome \(i.e. prediction\) is favorable vs unfavorable. In the risk model, a favorable outcome is a 'No Risk' prediction as this prediction may lead to the application receiving a loan, and an unfavorable outcome is a 'Risk' prediction. Go ahead and drag and drop the two label values to the corresponding favorable/unfavorable values, then click the 'Next' button

![](../.gitbook/assets/screen-shot-2019-10-31-at-1.15.58-am.png)

* OpenScale will actually analyze the training data and recommend which feature to monitor for fairness. We want to monitor for fairness for the 'Sex' and 'Age' features, ensure those two tiles are selected and click the 'Next' button.

![](../.gitbook/assets/screen-shot-2019-10-31-at-1.21.56-am.png)

* Next, we want to specify which is the majority group and which the minority group for the 'Sex' feature. In our model, we want to ensure there is no bias towards female loan applicants vs males, and towards younger applicants. OpenScale will recommend the values for you, click the 'Next' button
  * **Majority** groups are values of that feature that we expect to receive a higher percentage of favorable outcomes
  * **Minority** groups are values of that feature that we expect to receive a higher percentage of unfavorable outcomes

![](../.gitbook/assets/screen-shot-2019-10-31-at-1.25.26-am.png)

* Next we configure at what point we want OpenScale to display an alert if the fairness measurement falls below a certain threshold. If the rate at which the minority/protected group receives favorable outcomes relative to the majority/reference group, falls below this threshold an alert will be triggered \(the model is biased\). For the lab, set the threshold to  95%.

![](../.gitbook/assets/screen-shot-2019-10-31-at-1.32.40-am.png)

* Complete the same configuration for the 'Age' feature. For this feature we want 
  * The monitored group is 18 - 25. The majority group is 26 - 75
  * The fairness alert threshold should be 95%
* Finally, we have to specify a minimum number of records \(scoring requests\) that need to be received before calculating fairness. Set it to 200 for the lab.

![](../.gitbook/assets/screen-shot-2019-10-31-at-1.41.01-am.png)

* **Click** the 'Save' button on the summary page.

### 1.3 Drift Configuration

The drift monitor scans the requests sent to your model deployment \(i.e the payload\) to ensure the model is robust and does not drift over time. Drift in model predictions can occur either because the requests sent to the model are requests similar to samples in the training data where the model struggled, or because the requests are becoming inconsistent with the training data the model originally used.

* Continuing from the configure monitors page, **Click** on 'Drift' on the left panel and then on the 'Begin' button.

![](../.gitbook/assets/screen-shot-2019-10-31-at-1.49.28-am.png)

* In order to train this internal drift detection model, OpenScale will use the training data. Since we provided a connection to our training data \(and its under the size limit\), we can have OpenScale train the model. Select the tile on the left and click the 'Next' button.

![](../.gitbook/assets/screen-shot-2019-10-31-at-1.52.48-am.png)

* We next set a threshold as percent of degradation in performance before an alert is triggered. Set the threshold to **10%** and click the 'Next button.
* Finally, we have to specify a minimum number of records \(scoring requests\) that are used to  calculate drift. Set it to **100** for the lab and click the 'Next' button.
* Click the 'Save' button.
* The drift model will take a bit of time to train. While it trains, proceed to the next section of the lab below.

![](../.gitbook/assets/screen-shot-2019-10-31-at-2.00.31-am.png)

## 2. Run Scoring Requests

Now that we have enabled a couple of monitors, we are ready to "use" the model and check if there is any bias or drift. As well as starting to gain transparency by using OpenScale to explain how the model arrived at a prediction. 

To do this, we have a Jupyter notebook that will run enough scoring requests to your deployed model to exceed the monitor thresholds we configured above.

{% hint style="warning" %}
If you are waiting for your drift monitor to finish configuring, you can start executing parts of the notebook. Just ensure you do not execute the cell that makes the scoring calls until the drift model is ready \(state is "Monitor ready"\)
{% endhint %}

### 2.1 Open Notebook

* In [Watson Studio](https://dataplatform.cloud.ibm.com), select the project that you previously imported and click on the 'Assets' tab on the top of the project page.
* Under the 'Notebooks' section, _**Click**_ on the _**'model-scoring-requests'**_ notebook and then click on the pencil icon to enable you to edit / run the notebook.

![](../.gitbook/assets/screen-shot-2019-10-31-at-2.08.35-am.png)

### 2.2 Update Credentials

After the notebook environment starts up, scroll down to the section titled _**'Configure Service Credentials'**_.  Copy and Paste the Watson Machine Learning service credentials you saved to a text editor earlier.

![](../.gitbook/assets/screen-shot-2019-10-27-at-8.47.48-pm.png)

### 2.3 Run Notebook

Go back to the first cell in the notebook and run the notebook. You can run the cells individually by clicking on each cell and then click the `Run` button at the top of the notebook. 

{% hint style="info" %}
While the cell is running, an asterisk \(`[*]`\) will show up to the left of the cell. When that cell has finished executing a sequential number will show up. Generally, you want to wait until the cell finished executing before running the subsequent cells.
{% endhint %}

{% hint style="success" %}
The last cell in the notebook should report that you have received 200 responses for your scoring requests.
{% endhint %}

## 3. Trigger Monitor Checks

The fairness and drift monitors we configured will automatically be checked every hour or three hours \(as long as we have enough payload records stored\). Instead of waiting, we can force the monitors to be calculated.

* Back in the [Watson OpenScale dashboard](https://aiopenscale.cloud.ibm.com). 
* _**Click**_ on the _**'Model Monitors'**_  tab and **Click** will see the one deployment you configured in the previous section. 
* You will see we now have two additional sections in the deployment dashboard \(Fairness and Drift\). 
* Click on 'Sex' under Fairness and then click on the 'Check fairness now link on the right.

![](../.gitbook/assets/screen-shot-2019-10-31-at-2.23.38-am.png)

## 4. Explore the Watson OpenScale UI

### 4.1 Check Model Fairness

Now that we have configured fairness and submitted some scoring requests to our model, we can check if there is bias to either of our protected groups..

* Go back to the [Watson OpenScale dashboard](https://aiopenscale.cloud.ibm.com). 
* When the dashboard loads, _**Click**_ on the _**'Model Monitors'**_  tab and you will see the one deployment you configured in the previous section.

![](../.gitbook/assets/screen-shot-2019-10-26-at-9.11.48-pm.png)

* We see there is an alert that the model is exhibiting bias. In this case, we have gone beyond the threshold we set to specify an acceptable difference between the percentage of Favorable outcomes for the Monitored group as compared to the percentage of Favorable outcomes for the Reference group \(Favorable % for monitored group / Favorable % for reference group \* 100 \)
* _**Click**_ on the tile for the model deployment to view details for the deployment. 

![](../.gitbook/assets/screen-shot-2019-10-26-at-9.14.31-pm.png)

* You can see the fairness threshold is not met for the 'Sex' attribute.  We are monitoring a female group for fairness by comparing it to the male group \(the reference group\)
  * On the right panel, under ‘ fairness score for Sex’. The fairness score is calculated by comparing 'No Risk' predictions for the female group compared to the male group. You can also see when the last evaluation was conducted.
  * On the graph we can see fairness over time \(which is calculated hourly as predictions are made by the model\).

{% hint style="warning" %}
You must exceed the minimum number of records in the payload table for the fairness calculations to run. If there is not enough new payload data, the graph will show metrics from the last successful evaluation.
{% endhint %}

#### 4.1.1 Fairness Alert Details

We can now dive deeper into the fairness alert, move your mouse pointer over the graph to one of the blue points below the red threshold line \(you will see a 'view details' pop up\)

![](../.gitbook/assets/screen-shot-2019-10-31-at-2.33.57-am.png)

**Click** on that point to bring up the details.

![](../.gitbook/assets/screen-shot-2019-10-26-at-9.15.06-pm.png)

* From the details page, we can see that the monitored group is receiving favorable outcomes 73%, while the reference group is at 78%.  The default view has the **'Payload + Perturbed'** radio button selected.
  * This displays the fairness outcomes computed by using the actual payload + perturbed data \(synthesized data obtained by flipping the monitored values, male-to-female and female-to-male\).
* _**Click**_ on the 'Payload' radio button to display the payload data the model received for the selected hour.
* _**Click**_ on the 'Training' radio button to display the records used to train the model
  * In this example, we see that there is more training data for men than there is for women.
* _**Click**_ on the 'Debiased' radio button to display the Payload + Perturbed data set after applying the Watson OpenScale debiasing algorithm. 
  * OpenScale automatically creates a debiased “shadow model”, which predicts when production model is going to generate a biased output. The de-biased model evaluates whether or note data perturbation \(i.e flipping protected value\) changes the prediction 
  * Note that this debiased model has a scoring endpoint that can be put into production and used by clients, but the debiasing of one feature can negatively impact other features.
* _**Click**_ the 'Monitored Feature' drop down and select Age, to view fairness details for different age ranges.

{% hint style="info" %}
In the debiased view, the **after** accuracy is computed by taking feedback data and sending it to the active debiasing API. The **before** accuracy is computed by taking feedback data and sending it to the production model.
{% endhint %}

{% hint style="info" %}
Watson OpenScale supports bias detection for models using structured data in its feature vector. It requires scoring requests to be logged, which is automatic for Watson Machine Learning engines.
{% endhint %}

#### 4.1.2 Transaction Explanation

For both regulatory and business reasons, lenders need to be able to understand why their credit risk models make specific decisions. A powerful feature for OpenScale is the ability to provide an explanation for why a model made a particular prediction.

* You can also explain the transactions associated to the fairness metrics, from the 'Payload + Perturbed' screen, **Click** on the **View transactions** button in the fairness details chart. 

![](../.gitbook/assets/screen-shot-2019-10-31-at-2.38.06-am.png)

We want to explore on the transaction that was considered biased. Click on the 'Biased transactions' radio button and then click on 'Explain' for one of the transactions in the table.

Note that this view can take some time to populate as OpenScale generates the explanations for this transaction.

![](../.gitbook/assets/screen-shot-2019-10-31-at-2.40.46-am.png)

From the transaction explanation page, you can see a breakdown of the features contributing to either "Risk" or "No Risk" outcome. We can also see advanced explanations, which show:

* The minimum set of changes in feature values to generate a different prediction. Each feature value is changed so that it moves towards its median value in the training data.
* The maximum changes that can occur in feature values that will not cause the prediction to change. Each feature value is changed so that it moves towards its median value in the training data.

![](../.gitbook/assets/screen-shot-2019-10-31-at-2.48.30-am.png)

{% hint style="warning" %}
Advanced explanations are not available for regression, image, and unstructured text models.
{% endhint %}

{% hint style="info" %}
You can generate explanations for any transaction by clicking on the 'Explain a transaction' icon on the left panel and enter one of the transaction IDs .
{% endhint %}

### 4.2 Check Model Drift

Over time, the data coming into our model from the initial training data, impacting the both the accuracy of our model and the business processes using the model. Watson OpenScale analyzes transactions to detect drift in model accuracy as well as drift in data. 

{% hint style="info" %}
* Drift in model accuracy happens if there is an increase in transactions that are similar to those that the model did not evaluate correctly in the training data. 
* Drift in data estimates the drop in consistency of the data at runtime as compared to the characteristics of the data at training time.
{% endhint %}

* Go back to the [Watson OpenScale dashboard](https://aiopenscale.cloud.ibm.com). 
* When the dashboard loads, _**Click**_ on the _**'Model Monitors'**_  tab and you will see the one deployment you configured in the previous section.

![](../.gitbook/assets/screen-shot-2019-10-26-at-9.11.48-pm.png)

* _**Click**_ on the _**'Drop in accuracy'**_ option on the left panel to show the model drift visualization.

![](../.gitbook/assets/screen-shot-2019-10-28-at-12.11.48-am.png)

* We can see the model has an estimated drop of 2% and that 12% of the transaction data \(scoring requests\) are inconsistent compared to the training data.
* _**Click**_ on a data point in the 'Drop in accuracy' graph \(blue line in screenshot above\) to view drift details.

{% hint style="info" %}
Note that the screenshots above may not match exactly what you see in your dashboard. The monitors are using the payload \(scoring requests\) that were sent to the model, which were randomly selected. 

In some cases, you may not see a drop in accuracy from model drift. If you do not see anything in your dashboard, you can always submit a new set of requests to the model and trigger the drift evaluation again.
{% endhint %}

![](../.gitbook/assets/screen-shot-2019-10-28-at-12.17.45-am.png)

* From here you can explore the transactions that lead to drift in accuracy as well as drifts in data consistency.

{% hint style="warning" %}
If you explore a transaction, note that it may take some time to generate transaction explanations as OpenScale makes multiple requests to the deployed model.
{% endhint %}

{% hint style="info" %}
Drift is supported for structured data only and regression models only support data drift.
{% endhint %}



