# Shopify integration

## Description
Integration template between Linx and the Shopify API.

## Installation
### Create a new private app on Shopify

1. Register a new private app on Shopify.
1. Enable the OAuth 2.0 settings.
   1. Select the scopes:
      - `Customers - Read and write access`
      - `Products - Read and write access`
1. Save your private app.
1. Make note of the **API Key**, **Password** and **Example URL** details for later.

### Configure the Solution's $.Settings:

1. Open the sample Solution in your Linx Designer.
1. Edit the $.Setting values:

   - `shopify_apiKey`: Your private app's **API Key**.
   - `shopify_password`: Your **password**.
   - `shopify_shopName`: Your shop's name or hostname.
   - `shopify_api_version`: Current version of the API, at the time of writing it is `2021-01`, and may change at a later stage.

1. Save the Solution.

## Usage
### Customers

Location: [Solution] > [Project: Shopify] > [Folder: Customers]


#### GetCustomers

Makes a `GET` request to the `/customers` endpoint. The response is returned as a structured list of customers from the call.


### Products

Location: [Solution] > [Project: Shopify] > [Folder: Products]

#### CreateProduct

Makes a `POST` request to the `/products` endpoint, creating a new Product using the data passed in with the function's input parameters. The response is returned as a structured object from the call.


## Contributing

For questions please ask the [Linx community](https://linx/software/community) or use the [Slack channel](https://linxsoftware.slack.com/archives/C01FLBC1XNX). 

## License

[MIT](https://github.com/linx-software/template-repo/blob/main/LICENSE.txt)



