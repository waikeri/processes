
How to integrate Shopify and HubSpot using the internal demo application

###

This tutorial was made for iOS development team and the involved stakeholders, who need to understand the basics of automatic data integration between Shopify and HubSpot CRM software. 
Using the information from the tutorial you can save time, spent by manually processing the tedious task of creating a new customer repeatedly, and automate the integration process between two different applications.
The Shopify and HubSpot integration can be added to any newly developed client’s app.

###

1.	General process overview


1.	New customer creates a profile on Shopify
2.	Shopify sends a notification with the packed data to our internal app
3.	The internal app stores the data from the new customer 
4.	The internal app creates a contact on HubSpot using the data received from the customer

###

2.	Prerequisites


2.1.	Shopify setup

Let’s be notified whenever a new customer registers into the specified Shopify account. 
In order to do that, we need to activate a webhook, which will send us a message with the data collected from the new customer. 

Here below you can explore how to set the notification up.

2.1.1.	Subscription for the notification messages

1.	Login to the Applifting (or client) Shopify app account: https://accounts.shopify.com/store-login
2.	From your Shopify app, go to Store > Settings.
3.	Under Store settings, tap Notifications.
4.	Scroll down to the Webhooks section.
5.	Click the Create webhook button. A new window should appear.
6.	Choose the Customer creation option
7.	Choose the JSON format option
8.	Enter the URL: https://intapp.ngrok.io/new-customer. Here the notifications come and are being stored.
9.	Click Add webhook. Your webhook should now appear under the "Webhooks" section.
10.	Test the URL connection. To do this click the send test notification link.

Docs: https://help.shopify.com/en/manual/orders/notifications/webhooks


2.2.	HubSpot setup

Before we can send requests to HubSpot platform, we need to set up the correct authentication credentials. API key is usually used for the authentication process.

2.2.1.	Get the API key

1.	Log in the Applifting’s development account here: https://app.hubspot.com/login
2.	Go to Apps > Get HubSpot API key
3.	Click Show key. Your API key should now appear under the "Example request" section.


The API key is used as API_KEY variable and serves us as an original identification and authorization tool. It provides the access to the HubSpot account in order to create contacts.

Docs: https://knowledge.hubspot.com/integrations/how-do-i-get-my-hubspot-api-key

###

3.	Receive the customer data from Shopify


After the webhook with notifications has been set on Shopify side, we need to collect and store the received data it contains to our internal database.
1.	Go to the internal application development tools.
2.	Create a database, where you’ll store the data received from Shopify notification webhooks.
3.	Create a table to store the customer contacts.
4.	Each customer needs to have defined these default properties to be created:

Id
Email
Firstname
Lastname
Website (not required)
Company
Phone
Address
City
State
ZIP
Create date (Shopify)
Post date (HubSpot)

5.	Next step is an automated transfer that posts our received data to HubSpot CRM.

###

4.	Create a contact in HubSpot


1.	To create the new HubSpot contact (or update an existing one), we need valid API key. 
2.	Use POST method and define the following URL endpoint:
https://api.hubapi.com/contacts/v1/contact/createOrUpdate/email/applifting123@hubspot.com?hapikey= {key}
3.	Instead of {key} place the API key value you’ve generated in the HubSpot developer account
4.	Prepare the data (JSON format). Use the documentation below as an example. 
5.	Every contact needs to have defined its default properties:

Email
Firstname
Lastname
Website (not required)
Company
Phone
Address
City
State
ZIP


6.	From your HubSpot development account, go to > Apps >  Create a test account.
7.	Test the URL connection. The successfull 200 response contains a vid of the updated or created record, and an isNew field that indicates if a new record was created.
8.	Push the customer data from our internal demo application database to HubSpot. Use the API request to the created URL endpoint. 
9.	Create and store the internal log to record that the customer data have been sent to HubSpot and new contact has been created successfully.

Docs: https://developers.hubspot.com/docs/methods/contacts/create_or_update



