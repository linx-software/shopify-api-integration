# shopify-api-integration

## Description
You can use webhook subscriptions to receive notifications in a Linx Application about particular events in a Shopify store. After you've subscribed to a webhook, you can let your app execute code immediately after specific events occur in shops that have your app installed, instead of having to make API calls periodically to check their status.

For example, you can rely on webhooks to trigger an action in your app when a customer creates a cart, or when a merchant creates a new product in their Shopify admin. By using webhooks subscriptions you can make fewer API calls overall, which makes sure that your apps are more efficient and update quickly.

More details on Shopify Webhooks can be found [here](https://shopify.dev/api/admin/rest/reference/events/webhook).

## Installation

The below steps describe how to host this Solution on your own Linx cloud server environment.

### Create a new private app on Shopify

1. Register a new private app on Shopify (Left menu bar > Apps > Manage private apps >  Create new private app).
2. Complete the basic _App Details_ information. 
1. In the __Admin API__ section, expand the _v Show inactive Admin API permissions_ section.
2. Enable the required scopes.
1. Save your private app.
1. Make note of the **API Key**, **Password** and **Shared Secret** details for later.

### Register for a Linx trial server
This solution runs on a Linx cloud server instance..

1. Register for a Linx trial cloud server [here](https://linx.software/server-buy2/).
2. You will receive an email containing your Linx cloud server and drive space credentials when your trial server has been activated.

### Deploy to your cloud server

1. Log into your cloud server instance and upload the Solution (Top Menu > Server > Upload).
3. Open the Solution's Settings and update the below Setting values to reflect your environment and Shopify App credentials:
   -  LinxServerHostname - value to reflect your server instance name -  for example, if my server is `https://dev1.linx.twenty57.net` then my instance name is `dev1`.
   - ShopifyApiKey - _Generated when registering a private app_.
   - ShopifyPassword - _Generated when registering a private app_.
   - ShopifySharedSecret - _Generated when registering a private app_.
   - ShopifyShopName: I.e. if my admin URL is `https://linx-software.myshopify.com/` then the store name is `linx-software`.
4. Click __Save__.
3. On the Solution's service dashboard page, __start__ the _WebhookReciever_ service. 


## Subscribing to webhooks
In order to start receiving notifications for events on your Shopify store, you first need to "subscribe" to event topics using the API. More details on webhook subscriptions can be found [here](https://shopify.dev/apps/webhooks#1-subscribe-to-a-webhook-topic).

A generic Linx function has been created to subscribe to a chosen topic. To subscribe to a webhook topic:
1. On the Linx Server dashboard, navigate to [Solution] > [Project: Shopify] > [Folder: Webhooks] > [Folder: Subscribe] >  [Function: SubscribeToWebhook]
2. Click on __RUN FUNCTION__.
3. Enter in the topic you would like to subscribe to i.e. "products/create".
4. Click on __RUN FUNCTION__.

Your app should now be subscribed to that topic.


## Receiving webhooks event notifications
The Linx Solution is built to receive all the event notifications on a single endpoint "/shopify/webhooks" hosted on a Linx API. Any webhook event that you have subscribed will be sent to this endpoint. The endpoint is setup generically to receive a request body containing a single field `id`. This is so that the same endpoint can be used for all the webhooks, the raw data of the request body will be available inside the operation.




## Verifying webhooks

Webhooks can be verified by calculating a digital signature. Each webhook request includes a base64-encoded X-Shopify-Hmac-SHA256 header, which is generated using the app's shared secret along with the data sent in the request. More details can be found [here](https://shopify.dev/apps/webhooks#verify-the-request-is-from-shopify).

The webhook is automatically verified by a custom Linx function which achieves the above logic. If the request is invalid, then an error is thrown.


## Accessing the webhook event data

Like mentioned above, this generic endpoint is designed to receive any and all webhooks that you have subscribed to.

However, each event will have different data structures. Therefore if you would like to serialize the data for the different calls, you will need to check the `X-Shopify-Topic` header for an indication of what event was sent.

A generic 'LogActivity' function is used to write the area i.e. "products", the event i.e. "create" and the ID of the event entity to a CSV file on the server.

From this you can then use custom logic to de-serialize the data into a custom type using the data passed into the operation in the `$.Parameters.Data.HttpContext.Body` property. An demonstration of this can be found in the 'LogActivity' function.



## Contributing

For questions please ask the [Linx community](https://linx/software/community) or use the [Slack channel](https://linxsoftware.slack.com/archives/C01FLBC1XNX). 

## License

[MIT](https://github.com/linx-software/template-repo/blob/main/LICENSE.txt)



