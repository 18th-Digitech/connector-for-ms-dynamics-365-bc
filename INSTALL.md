# Installation Guide
Adobe Commerce – Shipsy Rider App

This document provides step-by-step instructions to install, configure, and deploy the Adobe Commerce – Shipsy Rider App using Adobe App Builder.

---

## 1. Prerequisites

### System Requirements
- Node.js v18+
- Adobe I/O CLI v10+ (installed and authenticated)

### Access Requirements
- Adobe App Builder
- Adobe Developer Console
- Adobe Commerce Admin

### Credentials Required
- Shipsy API Base URL
- Shipsy API Auth Token / API Key

---

## 2. Installation Overview

1. Download the app ZIP from Adobe Exchange
2. Connect the code to your Adobe App Builder workspace
3. Configure required services and environment variables
4. Deploy the app and subscribe to Commerce events

---

## 3. Install the App from Adobe Exchange

1. Acquire the Rider App from Adobe Exchange
2. Obtain organization admin approval
3. Select environment (Development / Staging / Production)
4. Create workspace using the guide:
   https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration/

---

## 4. Configure Required Services

Add the following services to your App Builder workspace:
- I/O Events
- I/O Management API
- Adobe I/O Events for Adobe Commerce
- Configure the Commerce Admin Integration with Adobe ID

---

## 5. Environment Configuration

### 5.1 Create .env File

```bash
cp .env.dist .env
```

Run this command in the project root directory.

---

### 5.2 Adobe Commerce Configuration

```env
COMMERCE_BASE_URL=https://<your-commerce-url>/rest/
COMMERCE_CONSUMER_KEY=
COMMERCE_CONSUMER_SECRET=
COMMERCE_ACCESS_TOKEN=
COMMERCE_ACCESS_TOKEN_SECRET=
```

---

### 5.3 Shipsy Configuration

```env
SHIPSY_API_BASE_URL=https://<shipsy-api-url>
SHIPSY_API_AUTH_TOKEN=
CUSTOMER_CODE=
```

---

### 5.4 Adobe App Builder (IMS OAuth – SaaS)

```env
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
OAUTH_SCOPES=['…']
OAUTH_HOST=https://ims-na1.adobelogin.com
```

---

### 5.5 Workspace Identifiers

Copy from Developer Console → Project → Workspace:

```env
IO_CONSUMER_ID=
IO_PROJECT_ID=
IO_WORKSPACE_ID=
```

---

### 5.6 Webhook & Logging

```env
SHIPSY_WEBHOOK_URL=
SHIPSY_WEBHOOK_SECRET=
LOG_STORAGE_PATH=
EVENT_PREFIX=test_app
```

---

## 6. Authentication: PaaS vs SaaS

### Base URL Differences

- PaaS: https://<env>.magentosite.cloud/rest/
- SaaS: https://na1-sandbox.api.commerce.adobe.com/<tenant-id>/

### Authentication Precedence

- OAuth1 (PaaS) is used if COMMERCE_* variables are set
- IMS OAuth (SaaS) is used if COMMERCE_* variables are empty

---

## 7. Obtain Credentials

### Adobe Commerce (PaaS)
- System → Extensions → Integrations → Add New Integration
- Grant API access and activate integration

### Shipsy
- Log in to Shipsy
- Request API credentials from Shipsy support if required

### Adobe App Builder
- Developer Console → Project → Workspace → OAuth Server-to-Server

---

## 8. Initialize & Deploy

```bash
npm install
aio login
aio console org select
aio console project select
aio console workspace select
aio app use --merge
aio app deploy
```

---

## 9. Event Subscription

### Event Used
- sales_order_save_commit_after

### Subscribe Manually (if needed)

```bash
npm run commerce-event-subscribe
```

Event subscriptions are automatically created during deployment.

---

## 10. Custom Order Attributes (Optional)

```json
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

## 11. Testing

- Place an order → Sent to Shipsy
- Update order → Shipsy updated
- Cancel order → Shipsy cancelled
- Verify webhook delivery updates

---

## 12. Debugging & Monitoring

Developer Console → Events → Commerce Order Sync → Debug Tracing

More details:
https://developer.adobe.com/commerce/extensibility/app-development/best-practices/logging-troubleshooting/#event-logs

---

## 13. Troubleshooting

- Orders not syncing: Verify Commerce and Shipsy credentials
- No delivery updates: Check webhook URL and secret
- Missing attributes: Validate extension attributes

---

## 14. References

- https://developer.adobe.com/app-builder/docs/
- https://developer.adobe.com/commerce/extensibility/starter-kit/integration/
- https://developer.adobe.com/events/docs/support/tracing
- https://experienceleague.adobe.com/en/docs/commerce-admin/start/admin/ims/adobe-ims-config#
We have secured our webhook using the require-whisk-auth key. This key can be found in webhook → actions.config.yaml. When you register our webhook (which is implemented as a web action in App Builder), you must include this key in the request headers. Please pass the key using the following header to access the webhook: X-Require-Whisk-Auth
