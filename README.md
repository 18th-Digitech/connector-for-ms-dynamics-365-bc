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

👉 [**INSTALL.md**](#/blob/master/INSTALL.md)

------------------------------------------------------------------------

## ⚠️ Important -- Onboarding Required Before Deployment

Before deploying the app, you must manually run:

``` bash
npm run onboard
```

If this step is skipped, the post-deploy script may fail.

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

Developer Console → Events → Commerce Customer Sync → Debug Tracing

### Product / Source Sync Issues

``` bash
aio rt:activation:list
aio rt:activation:log <activationId>
```

------------------------------------------------------------------------

## 📩 Support

For advanced features or enterprise capabilities, contact:
18th Digitech Team: **support@18dapps.com**

