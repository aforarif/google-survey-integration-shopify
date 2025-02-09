# Shopify Google Customer Reviews Integration

This repository contains the Liquid script for integrating Google Customer Reviews with a Shopify store.

## How to Use
1. Navigate to your Shopify dashboard then go to `Setting > Checkout`. Scroll all the way down until you find `Additional Scripts`. Paste the `google-survey.liquid` script here then click SAVE.
2. Test the implementation by placing a test order and verifying that the survey email is sent after the specified delay.

## Customizations
- **Replace Merchant Center ID**: 1111111111
- **Replace Estimated Delivery Time**: 604800 (It's been converted days to seconds. Convert days into seconds from Google i.e 7 days = 604800 seconds)
