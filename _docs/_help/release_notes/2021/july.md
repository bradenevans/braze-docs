--- 
nav_title: July
page_order: 6
no_index: true
page_type: update
description: "This article contains release notes for July 2021."
---

# July 2021

## Transactional Email Campaigns

Transactional emails are those sent to facilitate an agreed-upon transaction between a sender and the recipient. Braze's Transactional email campaign type is purpose-built for sending automated, non-promotional email messages like order confirmations, password resets, billing alerts, or other business-critical notifications. In addition, a corresponding [transactional email endpoint]({{site.baseurl}}/api/endpoints/messaging/send_messages/post_send_transactional_message/) has been created. Transactional emails and the new endpoint are only available as part of select Braze packages. Visit our [documentation]({{site.baseurl}}/api/api_campaigns/transactional_campaigns) to learn more. 

## Nested Object Support for Event Properties

Braze now supports [nested objects]({{site.baseurl}}/user_guide/data_and_analytics/custom_data/nested_object_support/) for custom events and purchase events. Nested objects allow you to send arrays of data as properties of custom events and purchases. This nested data can be used for templating personalized information in API-triggered messages through the use of Liquid and dot notation.

## New HMAC Liquid Filters

New `hmac_sha1` and `hmac_sha256` Liquid encoding filters have been added to the Braze platform. Documentation on these new filters can be found [here]({{site.baseurl}}/user_guide/personalization_and_dynamic_content/liquid/advanced_filters/).

## Purchase Event Page

Curious about the details of purchase events at Braze? Visit our dedicated [purchase event documentation]({{site.baseurl}}/user_guide/data_and_analytics/custom_data/purchase_events/) to learn more.

## New Partners 

### Nexla - Workflow Automation Partner
[Nexla]({{site.baseurl}}/partners/nexla) is the leader in unified data operations and a 2021 Gartner Cool Vendor. Customers that use Currents to send data to data warehouses can leverage Nexla to extract, transform, and load that data to other locations, making data easily accessible across your entire ecosystem. Nexla enables you to use Braze Currents to get data in a custom format delivered to your destination of choice by a simple point and click. 

### Amperity - Customer Data Platform Partner
[Amperity]({{site.baseurl}}/partners/amperity/) is a comprehensive enterprise customer data platform, helping brands get to know their customers, make strategic decisions, and consistently take the right course of action to serve their consumers better. Amperity supports the Braze platform by providing a unified view of your customers across its CDP and Braze allowing you to send valuable Amperity data to Braze.

### Digioh - Survey Partner
[Digioh]({{site.baseurl}}/partners/digioh/) helps you grow your lists, capture first-party data, and put your data to use in your Braze campaigns. The drag-and-drop builder makes it easy to create on-brand forms, pop-ups, preference centers, landing pages, and surveys that connect you with your customers.

### AppsFlyer Audiences - Attribution/Analytics Partner
[AppsFlyer]({{site.baseurl}}/partners/message_orchestration/attribution/appsflyer/) is a mobile marketing analytics and attribution platform that helps you analyze and optimize your apps through marketing analytics mobile attribution, and deep linking. [AppsFlyer Audiences]({{site.baseurl}}/partners/appsflyer_audiences/) allow you to build audience segments and pass these segments directly to Braze to create powerful customer engagement campaigns.

