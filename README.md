# Tapfiliate — GTM Server-Side Tag Template

A Google Tag Manager **server-side** tag template for [Tapfiliate](https://tapfiliate.com) affiliate tracking. Creates and updates conversions and customers via the Tapfiliate REST API directly from your server-side GTM container.

## Features

- **Create Conversion** — Record affiliate conversions with amount, currency, and affiliate attribution
- **Update Conversion** — Approve or disapprove existing conversions
- **Create Customer** — Register customers for lifetime/recurring commissions
- **Update Customer** — Update existing customer records
- **Affiliate Attribution** — Support for referral codes, coupon codes, and click IDs
- **Meta Data** — Attach custom JSON metadata to conversions or customers
- **Auto IP/UA** — Automatically forwards User-Agent and client IP from request headers
- **Debug Mode** — Console logging for troubleshooting

## Installation

### Option A: Import from Community Gallery

1. In your **server-side** GTM container, go to **Templates** → **Tag Templates**
2. Click **Search Gallery** and search for "Tapfiliate"
3. Add the template to your container

### Option B: Manual Import

1. Download `template.tpl` from this repository
2. In your server-side GTM container, go to **Templates** → **Tag Templates** → **New**
3. Click the **⋮** menu → **Import** and select the `.tpl` file
4. Click **Save**

## Setup

### 1. Create Conversion Tag

| Setting | Value |
|---|---|
| API Token | Your Tapfiliate API token |
| Event Type | Create conversion |
| Transaction ID | `{{Transaction ID}}` |
| Conversion Value | `{{Purchase Amount}}` |
| Currency | `EUR` |
| Referral Code / Coupon / Click ID | At least one affiliate identifier |
| Trigger | Purchase event |

### 2. Update Conversion Tag (Optional)

Use this to approve or disapprove conversions after validation.

| Setting | Value |
|---|---|
| API Token | Your Tapfiliate API token |
| Event Type | Update conversion |
| Transaction ID | `{{Transaction ID}}` |
| Conversion Status | Approved / Disapproved |

### 3. Create Customer Tag

| Setting | Value |
|---|---|
| API Token | Your Tapfiliate API token |
| Event Type | Create customer |
| Customer ID | `{{User ID}}` |
| Coupon / Referral Code | Affiliate identifier |

## Template Fields

| Field | Required | Shown For | Description |
|---|---|---|---|
| API Token | Yes | All | Your Tapfiliate API token |
| Event Type | Yes | All | The API operation to perform |
| Transaction ID | Yes* | Conversions | Unique order/transaction ID |
| Customer ID | Yes* | Customers | Unique customer identifier |
| Conversion Value | No | Conversions | Monetary value |
| Currency | No | Conversions | ISO 4217 currency code |
| Conversion Status | No | Update conversion | Approved or Disapproved |
| Referral Code | No | All | Affiliate referral code |
| Coupon | No | All | Affiliate coupon code |
| Click ID | No | All | Click tracking ID |
| Meta Data (JSON) | No | All | Custom JSON metadata |

## Affiliate Attribution Priority

When creating conversions or customers, affiliate identifiers are sent in this priority order:
1. **Coupon** (highest priority)
2. **Click ID**
3. **Referral Code**

Only the highest-priority identifier is sent per request.

## Permissions

This template requires:

- **Read Request** — Reads User-Agent and X-Forwarded-For headers for attribution
- **Send HTTP Request** — Sends POST requests to `https://api.tapfiliate.com/1.7/pb/`
- **Logging** — Console logging in debug/preview mode only

## Resources

- [Tapfiliate REST API Documentation](https://tapfiliate.com/docs/rest/)
- [Tapfiliate Integration Guides](https://tapfiliate.com/docs/integrations/)

## Author

Created by [New North Digital](https://newnorth.digital?utm_source=github&utm_medium=gtm-template&utm_campaign=tapfiliate-server-tag)

## License

Apache 2.0 — see [LICENSE](LICENSE).
