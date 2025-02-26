# Google Customer Reviews Script for Shopify

This script integrates **Google Customer Reviews** into Shopify. It dynamically configures the survey language and estimated delivery time based on the shipping country.

## Configuration Instructions

### 1. Update Your Google Merchant Center ID
Replace the placeholder Merchant ID in the script with your actual **Google Merchant Center ID**.

```liquid
"merchant_id": 5348651127, // Your Google Merchant Center ID

2. Configure Language Based on Shipping Country

The script automatically sets the survey language based on the shipping country code.
You can modify the country-language mapping in this section:

var countryLanguageMap = {
  'DE': 'de', // Germany - German
  'FR': 'fr', // France - French
  'ES': 'es', // Spain - Spanish
  'IT': 'it', // Italy - Italian
  'NL': 'nl', // Netherlands - Dutch
  'PL': 'pl', // Poland - Polish
  'US': 'en', // United States - English
  'GB': 'en', // United Kingdom - English
  'CA': 'en', // Canada - English
  'AU': 'en', // Australia - English
  'IN': 'en', // India - English
  'JP': 'ja', // Japan - Japanese
  'CN': 'zh-CN' // China - Simplified Chinese
};

If your store ships to additional countries, you can add more language mappings to this list.

3. Configure Estimated Delivery Date

The script automatically sets the estimated delivery date based on whether the order is domestic (Germany) or international:
	•	Domestic (Germany orders) → 7 days (604,800 seconds)
	•	International orders → 12 days (1,036,800 seconds)

"estimated_delivery_date": "{{ order.created_at | date: '%s' | plus: {{ order.shipping_address.country_code == 'DE' | ternary: 604800, 1036800 }} | date: '%F' }}",

If you need different delivery estimates, update the number of seconds:
	•	1 day = 86,400 seconds
	•	7 days = 604,800 seconds
	•	12 days = 1,036,800 seconds

To adjust the estimated delivery, modify these values accordingly.

4. Add Script to Shopify Checkout

To enable Google Customer Reviews in Shopify, follow these steps:
	1.	Go to Shopify Admin Panel
	2.	Navigate to Settings → Checkout
	3.	Find the “Order status page” section
	4.	Paste the script into the Additional scripts box
	5.	Save the changes

Google will automatically send a review request to customers after the estimated delivery time.

✅ Features & Benefits

✔️ Automatic language selection based on the shipping country
✔️ Flexible delivery estimates for domestic and international orders
✔️ Fully compatible with Shopify’s checkout scripts
✔️ Only includes products with valid GTIN (barcode) when available

This setup ensures a smooth Google Customer Reviews experience for both domestic and international customers. 🚀

Need Help?

For any issues, refer to Google’s Customer Reviews documentation or contact support.
