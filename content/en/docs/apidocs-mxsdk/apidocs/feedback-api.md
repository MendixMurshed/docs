---
title: "Feedback API – Version 1"
linktitle: "Feedback API v1"
url: /apidocs-mxsdk/apidocs/feedback-api/
description: "Presents details for using this API to build on top of the feedback management functionality of the Mendix Platform and to connect your own feedback gathering tool."
weight: 60
deprecated: true
---

{{% alert color="warning" %}}
Feedback API v1 is deprecated, and it will be turned off completely on September 30, 2024.

To ensure a seamless transition, Mendix strongly recommends migrating to [Feedback API v2](/apidocs-mxsdk/apidocs/feedback-api-v2/) for all your feedback-related operations, including retrieval, creation, and updates.
{{% /alert %}}

## 1 Introduction

The Mendix Feedback API allows you to retrieve, add, and manage feedback for your Mendix apps.

To use the API, you need to set up a **Consumed Web Service** using the WDSL for this service, available here: [Get WSDL](/attachments/apidocs-mxsdk/apidocs/feedback-api/19398864.wsdl). You can find out how to do this in [How to Consume a Complex Web Service](/howto/integration/consume-a-complex-web-service/).

The actions in the feedback API can then be called in a microflow using the **Call web service** action. This is described in the *Studio Pro Guide* here: [Call Web Service Action](/refguide/call-web-service-action/).

{{% alert color="info" %}}

Each call also requires the parameters 'username' and 'password'. These are the public credentials you will find below; actual authentication of requests is done through API keys.

* username: PlatformAPIUser
* password: PlatformAPIPassword

{{% /alert %}}

## 2 API Calls

### 2.1 AcceptFeedback

This call **accepts** the specified feedback item. This means that the app team has accepted the feedback and added this feedback as a story to the Sprint.

| Parameter Name | Parameter Type | Description |
| --- | --- | --- |
| ApiKey | String | The ApiKey the application uses to access the Feedback API for this app.
| FeedbackItemID | Integer/Long | The ID of the Feedback item to be accepted 
| appID | String |  The ID of the app

* Return value – Boolean

### 2.2 AddFeedback

This call **adds a new feedback item** to the app and returns the ID of the new feedback item.

| Parameter Name | Parameter Type | Description |
| --- | --- | --- |
| ApiKey | String | The ApiKey the application uses to access the Feedback API for this app. 
| Description | String | Description of the feedback item. (Optional) 
| IssueType | Enumeration IssueType | Type of the feedback item (Question/Idea/Problem) 
| ProjectID | String | The ID of the app. 
| Shortname | String | The name of the feedback item. 
| UserEmail | String | Email address of the user who created the feedback item. 
| Username | String | Name of the user who created the feedback item.

* Return value – Integer/Long

### 2.3 CloseFeedback

This call **closes** the specified feedback item.

| Parameter Name | Parameter Type | Description |
| --- | --- | --- |
| ApiKey | String | The ApiKey the application uses to access the Feedback API for this app.
| FeedbackItemID | Integer/Long | The id of the feedback item being closed. 
| ProjectID | String | The ID of the app. 
| Reason | String | Reason why the feedback item is being closed (Optional)

* Return value – Enumeration IssueState (see below for possible values)

### 2.4 DeleteFeedback

This call **deletes** the specified feedback item.

| Parameter Name | Parameter Type | Description |
| --- | --- | --- |
| ApiKey | String | The ApiKey the application uses to access the Feedback API for this app.
| FeedbackItemID | Integer/Long | The ID of the Feedback item to be deleted 
| ProjectID | String | The ID of the app.

* Return value – Boolean

### 2.5 GetFeedbackItems

This call **retrieves a list of all feedback items** for the app which satisfy the IssueState filter.

| Parameter Name | Parameter Type | Description |
| --- | --- | --- |
| ApiKey | String | The ApiKey the application uses to access the Feedback API for this app. |
| IssueStateFilter | Enumeration IssueState | State of the Feedback items to be retrieved (Open, Under_review, Accepted, Scheduled, Solved, Rejected; empty returns all feedback for the app). |
| ProjectID | String | The ID of the app. |

* Return value – List of Issue

### 2.6 GetSingleFeedbackItem

This call **retrieves a single feedback item** by ID.

| Parameter Name | Parameter Type | Description |
| --- | --- | --- |
| ApiKey | String | The ApiKey the application uses to access the Feedback API for this app.
| FeedbackItemID | Integer/Long | The ID of the Feedback item to be retrieved 
| ProjectID | String | The ID of the app.

* Return value – Issue
