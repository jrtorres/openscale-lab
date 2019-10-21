# Monitor WML Model With Watson OpenScale

In this Code Pattern, we will use German Credit data to train, create, and deploy a machine learning model using [Watson Machine Learning](https://console.bluemix.net/catalog/services/machine-learning). We will create a data mart for this model with [Watson OpenScale](https://www.ibm.com/cloud/watson-openscale/) and configure OpenScale to monitor that deployment, and inject seven days' worth of historical records and measurements for viewing in the OpenScale Insights dashboard.

When the reader has completed this Code Pattern, they will understand how to:

* Create and deploy a machine learning model using the Watson Machine Learning service
* Setup Watson OpenScale Data Mart
* Bind Watson Machine Learning to the Watson OpenScale Data Mart
* Add subscriptions to the Data Mart
* Enable payload logging and performance monitor for subscribed assets
* Enable Quality (Accuracy) monitor
* Enable Fairness monitor
* Score the German credit model using the Watson Machine Learning
* Insert historic payloads, fairness metrics, and quality metrics into the Data Mart
* Use Data Mart to access tables data via subscription

![architecture](doc/source/images/architecture.png)

## Flow

1. The developer creates a Jupyter Notebook on Watson Studio.
2. The Jupyter Notebook is connected to a PostgreSQL database, which is used to store Watson OpenScale data.
3. The notebook is connected to Watson Machine Learning and a model is trained and deployed.
4. Watson OpenScale is used by the notebook to log payload and monitor performance, quality, and fairness.

## Prerequisites

* An [IBM Cloud Account](https://cloud.ibm.com).
* [IBM Cloud CLI](https://cloud.ibm.com/docs/cli/index.html#overview)
* An account on [IBM Watson Studio](https://dataplatform.cloud.ibm.com/).

# Steps

1. [Clone the repository](#1-clone-the-repository)
1. [Use free internal DB or Create a Databases for PostgreSQL DB](#2-use-free-internal-db-or-create-a-databases-for-postgresql-db)
1. [Create a Watson OpenScale service](#3-create-a-watson-openscale-service)
1. [Create a Watson Machine Learning instance](#4-create-a-watson-machine-learning-instance)
1. [Create a notebook in IBM Watson Studio](#5-create-a-notebook-in-ibm-watson-studio)
1. [Run the notebook in IBM Watson Studio](#6-run-the-notebook-in-ibm-watson-studio)
1. [Setup OpenScale to utilize the dashboard](#7-setup-openscale-to-utilize-the-dashboard)


> Note: Services created must be in the same region, and space, as your Watson Studio service.

> NOTE: At this time (3/27/19) you must use an instance of Watson OpenScale deployed in the `Dallas` region. This is currently the only region that sends events about scoring requests to the message hub, which is read by OpenScale to populate the payload logging table.

