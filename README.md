# Shopify Google Customer Reviews Integration

This repository contains the Liquid script for integrating Google Customer Reviews with a Shopify store.

## How to Use
1. Add the `google-survey.liquid` script to your Shopify theme's `order.liquid` or `main-order.liquid` file.
2. Navigate to your Shopify dashboard then go to `Setting > Checkout`. Scroll all the way down until you find `Additional Scripts`. Paste the script `google-survey.liquid` here then click SAVE.
3. Ensure the script is placed within the `{% if first_time_accessed %}` block to run only on the first access to the order confirmation page.
4. Test the implementation by placing a test order and verifying that the survey email is sent after the specified delay.

## Script Details
- **Merchant Center ID**: 1111111111
- **Survey Delay**: 7 days after order creation
- **Optional Fields**: Includes product GTINs for better survey relevance.

## License
This project is generated using AI.
