---
title: Load Data into Excel Online and build a Dataflows Monitoring Report with Power BI
description: How to use the dataflows connector in Power Automate to create a dataflows monitoring report in Power BI
author: miquelladeboer

ms.service: powerquery
ms.reviewer: kvivek
ms.topic: conceptual
ms.date: 12/15/2020
ms.author: mideboer
---

# Load Data into Excel Online and Build a Dataflows Monitoring Report with Power BI

## Introduction

In this step-by-step tutorial, we will show you how to set up your own monitoring dashboard for all of your dataflows:

![example of monitoring dashboard](media/dashboard.PNG)

First, you will download the Excel file and save it in OneDrive for Business or SharePoint. Next, you will create a Power Automate connector which will load metadata from your dataflow into the Excel file in OneDrive for Business or SharePoint. Lastly, you will connect a Power BI file to the Excel file to visualize the metadata and start monitoring the dataflows.

You can use this dashboard to monitor your dataflows' refresh duration and failure count. With this dashboard, you can track any issues with your dataflows performance and share the data with others. 

![overview of loading data through Excel](media/excel.PNG)	


## Prerequisites
* [Microsoft Excel](https://www.microsoft.com/en/microsoft-365/excel)

* [Power BI Desktop](https://www.microsoft.com/download/details.aspx?id=58494).

* A [Premium Power Automate License](https://docs.microsoft.com/power-platform/admin/pricing-billing-skus)

* [OneDrive for Business](https://www.microsoft.com/en/microsoft-365/onedrive/onedrive-for-business).

* A [Power BI dataflow](https://docs.microsoft.com/power-bi/transform-model/dataflows/dataflows-introduction-self-service) or [Power Platform dataflow](https://docs.microsoft.com/powerapps/maker/common-data-service/create-and-use-dataflows).

## Download the .pbit file

First, download the [.pbit file](https://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/excel-template.pbit).

## Download the Excel file and Save to OneDrive

Next, download the [.xlsx file](https://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/dataflow_monitoring.xlsx) and save the file to a location on OneDrive for Business or SharePoint

## Create a dataflow

If you do not already have one, create a dataflow. This can be done in either [Power BI dataflows](https://docs.microsoft.com/power-bi/transform-model/dataflows/dataflows-introduction-self-service) or [Power Apps dataflows](https://docs.microsoft.com/powerapps/maker/common-data-service/create-and-use-dataflows).

## Create a flow in Power Automate 

* Navigate to [Power Automate](https://flow.microsoft.com).

* Search for the template "When a dataflow refresh completes, output status into Excel". If you encounter difficulty, see these [instructions](https://docs.microsoft.com/power-automate/get-started-logic-template).

![example of excel template](media/templateexcel.PNG)

* Customize the flow. Actions that require input from you will automatically be expanded.

  The **Dataflow Refresh** trigger is expanded because you need to enter information on your dataflow:
    * **Group Type**: Select *Environment* when connecting to Power Apps and *Workspace* when connecting to Power BI.
    * **Group**: Select the Power Apps environment or the Power BI workspace your dataflow is in.
    * **Dataflow**: Select your dataflow by name.
  
  The **Add a row into a table** action is expanded because you need to enter the *Location* of the Excel file and the specific *Table* the data loads to.
    * **Location**: Select the location of the Excel file on OneDrive for Business or SharePoint.
    * **Document Library**: Select the library of the Excel file.
    * **File**: Select the file path to the Excel file.
    * **Table**: Select "Dataflow_monitoring".

* Add dynamic values to the required fields.

  For every required field, you need to add a dynamic value. This value is the output of the metadata of the dataflow run.
    * Select the field next to **Dataflow ID** and then select the lightning button.
    
    ![example of lightning button in Excel](media/dynamicexcel.png)

    * Select the Dataflow ID as the dynamic content.

	![example to select dataflow id in Excel](media/dataflowid.png)

    * Repeat this process for all required fields.

  * Save the flow.


## Create a Power BI Report

![An example of folder structure](media/excelcomplete.PNG)  

* Open the `.pbit` file.

* Connect to your Excel file.

In this dashboard, you can monitor, for every dataflow in your specified time interval:
* the dataflow duration
* the dataflow count
* the dataflow failure count

The uniqueID for every dataflow is generated by a merge between the dataflow name and the dataflow start time.