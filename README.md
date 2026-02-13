# Adobe Commerce – Shipsy Rider App

## Overview

The **Adobe Commerce – Shipsy Rider App** integrates Adobe Commerce with **Shipsy** to automate the complete **order-to-delivery workflow** with real-time synchronization.

The app sends new orders from Adobe Commerce to Shipsy for rider assignment, keeps order updates and cancellations in sync, and receives delivery status updates via webhooks to ensure both platforms remain aligned.

---

## Key Features

- Automatic order sync from Adobe Commerce to Shipsy  
- Real-time rider assignment and delivery status tracking  
- Support for order updates and cancellations  
- Webhook-based delivery status synchronization  
- No manual intervention required  

---

## Quick Start

### Prerequisites

- Node.js v18+  
- Adobe I/O CLI v10.3.4 (authenticated)  
- Adobe Commerce API credentials  
- Shipsy API Base URL, Customer Code and Shipsy Api key

---

### Installation

1. Install the **Adobe Commerce – Shipsy Rider App** from Adobe Exchange  
2. Obtain organization admin approval  
3. Select environment (Development / Staging / Production)  
4. Adobe creates an App Builder workspace automatically  

---

### Configuration

Configure the following environment variables in the Adobe App Builder workspace:

```
1- Download the app ZIP package from Adobe Exchange
2- Connect the downloaded code to your Adobe App Builder workspace
3- Add the workspace details to the environment configuration
4- Update the .env file with workspace-specific values
5- Add the workspace JSON configuration to the .aio file

Redeploy the app after configuration.

For more information Please follow the URL: https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration/
---

## How It Works

- **Order Creation** → Shipsy SoftData Upload API  
- **Order Update** → Shipsy SoftData Update API  
- **Order Cancellation** → Shipsy Cancel API  
- **Delivery Tracking** → Shipsy Webhooks  

---

## Sequence Flow

 
Customer
   |
Adobe Commerce
   |
Rider App (App Builder)
   |
Shipsy APIs
   |
Shipsy Rider
   |
Webhook Updates
   |
Adobe Commerce
 

---

## Custom Order Attributes (Optional)

```
{
  "extension_attributes": {
    "delivery_time_slot_start": "2025-07-22 09:00:00",
    "delivery_time_slot_end": "2025-07-22 11:00:00",
    "notes": "Leave at the reception desk",
    "rider_type": "Express"
  }
}
```

---

## Debugging & Monitoring

Use **Debug Trace** in Adobe Developer Console:

```
Events → Commerce Order Sync → Debug Tracing
```

---

## Troubleshooting

- Orders not syncing: verify API credentials  
- No delivery updates: check webhook URL and secret  
- Missing attributes: validate Magento order API  

---

## Support

- Adobe Commerce App Support  
- Shipsy Integration Support  
- 18th Digitech Team: support@18dapps.com
