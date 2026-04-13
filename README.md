# Connector for Microsoft Dynamics 365 Business Central

The **Connector for Microsoft Dynamics 365 Business Central** integrates Adobe Commerce with Microsoft Dynamics 365 Business Central using Adobe
App Builder.

This integration enables structured and controlled synchronization of products, inventory sources, customers updates between both systems.

The connector provides Full Sync, Delta Sync, and Specific Sync options via the Admin UI, along with scheduled automation and detailed logging
for enterprise-level operations.

------------------------------------------------------------------------

## 🚀 Features

### 🔹 Product Synchronization

-   Full Product Sync (runs once daily)
-   Delta Sync (runs every 15 minutes)
-   Specific Product Sync (on demand)
-   Bulk API & Batch Processing for high performance

### 🔹 Inventory Source Management

-   On-demand Full Inventory Sources Sync
-   Specific Inventory Sources Sync
-   Daily Delta Inventory Source Sync
-   Multi-source inventory consistency

### 🔹 Customer Update

-   Event-driven sync when customer updates data in **My Account**
-   Sync occurs only if the customer exists in Business Central


## 📦 Installation

Please follow the detailed installation instructions in:

👉 [**INSTALL.md**](https://github.com/18th-Digitech/connector-for-ms-dynamics-365-bc/blob/master/INSTALL.md)

## ✅ Prerequisites

- Node.js v18 or later
- Adobe App Builder
- Adobe I/O CLI v10 or later
- Adobe Admin UI SDK 3.0.0 or later

------------------------------------------------------------------------

## ⚠️ Important -- Product Attribute Configuration

     
PRODUCT_ATTRIBUTE_CODE = <attribute_code>$<attribute_name>$<attribute_type>,

Each entry consists of three components: the unique attribute code (which serves as the system identifier), the display name as shown in the Admin interface, and the attribute type. The attribute types can include text (for text input), decimal (for numeric values with decimals), boolean (for yes or no options), option (for a single-select dropdown), or multiselect (for multiple selectable options). For example, the format would be: PRODUCT_ATTRIBUTE_CODE=uom$UOM$option


## ⚠️ Important -- Onboarding Required Before Deployment

Before deploying the app, you must manually run:

``` bash
npm run onboard
```

If this step is skipped, the post-deploy script may fail.

### Configure Cron Job Schedule
 
  You have the flexibility to set the cron job schedule time in the `src/commerce-backend-ui-1/ext.config.yaml` file to suit your needs perfectly. If you'd like to ensure that the instructions for the cron job schedule in the help guide are up-to-date, you can easily make those updates at the specified path

 ```bash
 web-src/src/components/UserGuideTab.js
 ```



After onboarding, deploy the application using:

``` bash
aio app deploy
```

------------------------------------------------------------------------

## 🧪 Testing Checklist

-   Run Full Product Sync → Entire catalog updates
-   Execute Delta Sync → Recently modified products update
-   Perform Specific Sync → Selected products sync
-   Run Source Sync → Inventory sources update
-   Update customer in My Account → Customer sync triggers


------------------------------------------------------------------------

## 🛠 Debugging & Monitoring

### Customer Sync Issues

[**Developer Console**](https://developer.adobe.com/developer-console/) → Events → Commerce Customer Sync → Debug Tracing


### Product / Source Sync Issues

``` bash
aio rt:activation:list
aio rt:activation:log <activationId>
```

------------------------------------------------------------------------

## 📩 Support

For advanced features or enterprise capabilities, contact:
18th Digitech Pvt Ltd Team: **support@18dapps.com**
