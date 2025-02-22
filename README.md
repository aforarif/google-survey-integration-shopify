# Google Customer Reviews Script for Shopify

This script integrates Google Customer Reviews with your Shopify store. It sends an invitation to customers to provide feedback on their shopping experience after their purchase.

---

## Configuration Instructions

### 1. **Language Setting**
- The script automatically detects the shop's language using `{{ shop.locale.iso_code }}`.
- If the locale is not set, the language defaults to **German** (`'de'`).
- To change the default language, modify the fallback language code:
  - Example: Change `default: 'de'` to `default: 'en'` for English as the fallback.

---

### 2. **Merchant ID**
- Replace `1111111111` with your **Google Merchant Center ID** in the script:
  ```javascript
  "merchant_id": 1111111111, // Your Google Merchant Center ID
  ```

---

### 3. **Estimated Delivery Date**
- The estimated delivery date is set to **5 days** after order creation (432,000 seconds).
- To adjust for your delivery time:
  1. Determine your delivery time in days.
  2. Convert days into seconds using the formula:
     - **1 day = 86400 seconds**
     - Example:
       - If delivery is **3 days**, the calculation would be:  
         `3 days × 86400 seconds = 259200 seconds`.
       - If delivery is **7 days**, the calculation would be:  
         `7 days × 86400 seconds = 604800 seconds`.
  3. Update the `estimated_delivery_date` field with the corresponding value in seconds:
     ```javascript
     "estimated_delivery_date": "{{ order.created_at | date: '%s' | plus: 259200 | date: '%F' }}", // 3 days after order creation
     ```

---

### 4. **GTIN (Barcode)**
- If the products have a GTIN (barcode), they will be sent with the survey request.
- The script checks if a product has a barcode and includes it in the `products` array.
- No changes are needed unless you want to customize which products to include.

---

### 5. **Script Placement**
To add the script to your Shopify store:
1. Go to **Settings > Checkout** in the Shopify admin panel.
2. Scroll to **Order Status Page**.
3. Paste the entire script into the **Additional Scripts** field.
4. Click **Save**.

---

## Notes
- **Google Merchant Center Setup**: Ensure your Google Merchant Center account is set up for collecting customer reviews. Visit [Google Merchant Center](https://merchants.google.com/) for setup instructions.
- **Delivery Time**: Adjust the `estimated_delivery_date` if your delivery time is different from the default 5 days.

---

### How to Convert Days to Seconds
1. Multiply the number of days by **86400** (since 1 day = 86400 seconds).
2. Example:  
   - 1 day = 86400 seconds  
   - 3 days = 3 × 86400 = **259200 seconds**  
   - 7 days = 7 × 86400 = **604800 seconds**  

This should help you adjust the `estimated_delivery_date` properly.

---

## Full Script
Here’s the complete script for reference:

```liquid
{% if first_time_accessed %}
  <!-- BEGIN Google Customer Reviews -->
  <script>
    // Set the language for the survey (default to German if locale is not set)
    window.___gcfg = {
      lang: '{{ shop.locale.iso_code | default: 'de' }}' // Use Shopify locale, fallback to 'de' (German)
    };
  </script>

  <script src="https://apis.google.com/js/platform.js?onload=renderOptIn" async defer></script>
  <script>
    window.renderOptIn = function() {
      // Ensure Google API is loaded
      if (!window.gapi || !window.gapi.surveyoptin) {
        console.error('Google Customer Reviews script failed to load.');
        return;
      }

      window.gapi.load('surveyoptin', function() {
        var surveyConfig = {
          // REQUIRED FIELDS
          "merchant_id": 5348651127, // Your Google Merchant Center ID
          "order_id": "{{ order.order_number }}", // Shopify Order ID
          "email": "{{ order.email }}", // Customer Email
          "delivery_country": "{{ order.shipping_address.country_code }}", // Shipping Country Code
          "estimated_delivery_date": "{{ order.created_at | date: '%s' | plus: 432000 | date: '%F' }}", // 5 days after order creation

          // OPTIONAL FIELDS - Only include products if GTIN exists
          {% assign has_gtin = false %}
          {% for line_item
