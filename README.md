# Shopify integeration

## Overview

The provided sample includes:

- Connecting to the Shopify API
- Interacting with the following objects:
  - Customers
  - Products

---

### Additional resources

- [Shopify-Linx integration guide](https://community.linx.software/community/t/shopify-integration/506)
- [Shopify API reference documentation](https://shopify.dev/docs/admin-api/rest/reference)

---

### Pre-requisites

- Linx Designer
- Shopify account

---

### Dependencies

#### Linx Designer

This solution was developed in the Linx Designer `v5.20.2.0`

#### Shopify API

The version of the Shopify API at the time of writing is `2021-01`.

---

---

## Setting up the sample

Create a new private app on Shopify

1. Register a new private app on Shopify.
1. Enable the OAuth 2.0 settings.
   1. Select the scopes:
      - `Customers - Read and write access`
      - `Products - Read and write access`
1. Save your private app.
1. Make note of the **API Key**, **Password** and **Example URL** details for later.

Configure the Solution's $.Settings:

1. Open the [sample Solution](Solution.lsoz) in your Linx Designer.
1. Edit the $.Setting values:

   - `shopify_apiKey`: Your private app's **API Key**.
   - `shopify_password`: Your **password**.
   - `shopify_shopName`: Your shop's name or hostname.
   - `shopify_api_version`: Current version of the API, at the time of writing it is `2021-01`, and may change at a later stage.

1. Save the Solution.

---

---

## Using the sample

### Authentication

Requests are authenticated via the HTTP Basic security scheme. Your Shopify API Key is used as the `username` and your Shopify password is used as the `password` when making the requests.

### Making requests

Requests are made to a custom URL which is built up from your identifiers. This base URL is stored as a dynamic Setting value of the application (`$.Settings.shopify_baseUrl`). At runtime this value will use the identifiers in the other $.Settings values.

---

## Template HTTP requests

The following custom functions wrap the different types of HTTP calls into their own re-usable functions which can be thought of as 'custom Shopify connectors'.

---

### Customers

Location: [Solution] > [Project: Shopify] > [Folder: Customers]

---

#### GetCustomers

Makes a `GET` request to the `/customers` endpoint. The response is returned as a structured list of customers from the call.

---

### Products

Location: [Solution] > [Project: Shopify] > [Folder: Products]

---

#### CreateProduct

Makes a `POST` request to the `/products` endpoint, creating a new Product using the data passed in with the function's input parameters. The response is returned as a structured object from the call.

---
