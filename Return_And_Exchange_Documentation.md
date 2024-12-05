# Return and Exchange Documentation

This document outlines the steps and conditions for displaying and managing the "Exchange" button for customers in our Shopify store. The button will be displayed under specific conditions, and the customer will be redirected to a return and exchange URL if they wish to initiate the process. The logic behind the display of this button, as well as the handling of exchanges and returns, is described below.

### 1. **Exchange Button Visibility Conditions**

The **Exchange** button will be visible to the customer under the following conditions:

- The **product has been delivered** to the customer.
- The **product must be delivered within the last 7 days**.
- For a particular customer with id **6758706741535** the time limit should be **15 days**

**How It Works:**

- Whenever a product is delivered, the **metafield** of the order is updated automatically to reflect this status. The metafield includes details about the product, including its **SKU**, **size**, **delivery date**, and **status** (delivered).

The metafield follows this format:

```json
{
   "id": "gid://shopify/Order/123456789",
   "metafields": [
      {
         "namespace": "order",
         "key": "123456.1", // fullfilment id (order_number.1, order_number.2 ...., order_number.9)
         "value": "[{"sku":"TP1895","size":"XS","date":"10/11/2024","status":"delivered"},{"sku":"DR1382","size":"XS","date":"10/11/2024","status":"delivered"}]",
         "type": "json"
      },
      {
         "namespace": "order",
         "key": "123456.2",
         "value": "[{"sku":"TP1895","size":"XS","date":"10/11/2024","status":"delivered"},{"sku":"DR1382","size":"XS","date":"10/11/2024","status":"delivered"}]",
         "type": "json"
      }
   ]
}
```

- Each delivered product has a `fulfillment_id` (e.g., `order_number.1`, `order_number.2`, etc.).
- The **delivery date** and **status** of the product are stored within the metafield.

**How to Calculate 7 Days from Delivery:**

- Compare the **delivery date** stored in the metafield with the current date.
- If the **current date** is within 7 days of the **delivery date**, the **Exchange** button will be shown.

---

### 2. **Exchange Button Click Behavior**

When the customer clicks the **Exchange** button, they will be redirected to the following URL:

```
https://lbreturns.goodtribe.io??customer=${customerID}&order=${orderID}
```

Where:

- **customerID**: The unique Shopify customer ID.
- **orderID**: The unique Shopify order ID.

This URL will allow the customer to initiate the exchange process on the external returns platform.

---
