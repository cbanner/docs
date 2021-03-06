---
title: Dynamic Custom Fields
sidebar: cyclr_sidebar
permalink: dynamic-custom-fields
tags: [connector-creation]
---
Dynamic Custom Fields
---------------------------

Dynamic Custom Fields can be automatically generated by Cyclr for authenticated connectors. This removes the need to manually add Custom Fields for each connector installation. Cyclr is able to generate custom fields by either parsing an example response or by reading an object metadata definition.

To enable Dynamic Custom Fields you only need to set the **Custom Fields Lookup Method** on the appropriate Request/Response Format, the method used in **Custom Fields Lookup Method** must be able to be called without any field or parameter values being set.

![](./images/custom-fields-lookup-method.png)

Basic - Parsed
---------------------------

Cyclr generates Basic Dynamic Custom Fields by parsing an example response that is retrieved by calling a method. For this to work you should set the **Custom Fields Lookup Method** to a method that will get the response in the same structure as the Request/Response Format custom fields will be added to.

Cyclr will attempt to determine the correct Display Name and Data Type of the fields found in the response object, for more control of the custom fields generated you will need to make use of Enhanced Dynamic Custom Fields.

Enhanced - Defined
---------------------------

Cyclr generates Enhanced Dynamic Custom Fields from a metadata definition of the object retrieved by calling the third party API. For this to work the **Custom Fields Lookup Method** must be set to a method that has been setup for Enhanced Custom Field Discovery, see below.

Enhanced Custom Field Lookup Method
---------------------------

Before you can use Enhanced Dynamic Custom Fields you need to create a method in the connector that will retrieve the metadata for the object and check the **For Enhanced Custom Fields** option in the method or Cyclr will attempt to parse it as an example object.

![](./images/for-enhanced-custom-fields.png)

<br/><br/>
The response for this method must be an array and each item in the array must represent a single field in the object, you must also define the response fields with the below **System Fields** so that Cyclr can read the metadata correctly. You can use the scripting to alter the response from the third party API where required.

System Field | Required | Description
--- | --- | ---
cyclr_field_location | Yes | Identifies the location of the custom field, e.g. [items].custom_field
cyclr_data_type |   | The data type of the custom field, Use Cyclr data types as below
cyclr_data_type_format |   | Custom data type format for the custom field
cyclr_default_value |   | The default value to use for the custom field
cyclr_description |   | The description of the custom field
cyclr_display_name |   | The name to display the custom field as
cyclr_is_optional |   | Indicates if the custom field is optional when part of a request
cyclr_is_readonly |   | Indicates if the custom field is read-only, if it is it won't be added to any requests

Data Type | Value
--- | ---
Not Defined | 0
Text | 1
Integer | 2
Float | 3
Boolean | 4
Date Time | 5

[View the Custom Connector References](./custom-connector-reference)
