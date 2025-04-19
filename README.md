# Pricing_Engine_Implimentation
Write a Python script that:

1. **Reads Data from Two CSV Files:**
    - **`products.csv`** – Contains the product catalog with pricing, cost, and stock information.
    - **`sales.csv`** – Contains the recent sales data (for the last 30 days).
2. **Applies Pricing Rules:**
Process each product according to the rules detailed below to compute a new price, then output an updated pricing CSV file: **`updated_prices.csv`**.
3. **Outputs Result:**
The final output CSV should contain the product SKU, the old price, and the new price along with appropriate units.
### Input Files

### File 1: products.csv

| sku | name | current_price | cost_price | stock |
| --- | --- | --- | --- | --- |
| A123 | Item A | 649.99 | 500.00 | 150 |
| B456 | Item B | 699.00 | 550.00 | 15 |
| C789 | Item C | 999.00 | 500.00 | 250 |

### File 2: sales.csv

| sku | quantity_sold |
| --- | --- |
| A123 | 10 |
| B456 | 35 |
| C789 | 0 |

[products.csv](attachment:b0400fc7-eb48-4c8f-ad18-0de3304a8f53:products.csv)

[sales.csv](attachment:326dd521-11d1-4735-be92-8368f3a44806:sales.csv)
### Pricing Rules (Apply in the Given Precedence Order)

Evaluate the rules in the following order for each product. **Only the first applicable rule among Rules 1, 2, and 3 is applied.** After that, always apply Rule 4 to ensure the minimum profit margin.

1. **Rule 1 – Low Stock, High Demand (Highest Priority):**
    - **Condition:** If `stock < 20` **and** `quantity_sold > 30`.
    - **Action:** Increase the current price by 15%.
2. **Rule 2 – Dead Stock (Second Priority):**
    - **Condition:** If `stock > 200` **and** `quantity_sold == 0`.
    - **Action:** Decrease the current price by 30%.
3. **Rule 3 – Overstocked Inventory (Third Priority):**
    - **Condition:** If `stock > 100` **and** `quantity_sold < 20`.
    - **Action:** Decrease the current price by 10%.
4. **Rule 4 – Minimum Profit Constraint (Always Applied Last):**
    - **Condition:** Ensure that the computed new price is at least 20% above the `cost_price`.
        - If the computed price is below `cost_price * 1.2`, reset the new price to `cost_price * 1.2`.
    - **Action:** Finalize the price, rounding it to 2 decimal places.
5. **Final Rounding**
    - Round the final price to 2 decimal places.
    - ### Example Calculation

**For SKU A123:**

- **Data:** `current_price` = 649.99, `cost_price` = 500.00, `stock` = 150, `quantity_sold` = 10.
- **Rule Applied:** Rule 3 applies (Overstocked Inventory: stock > 100 and quantity_sold < 20).
    - New price is computed as: 649.99 * 0.9 = 584.99.
- **Minimum Profit Check:** 500.00 * 1.2 = 600.00.
    - Since 584.99 is less than 600.00, the final price is reset to 600.00.
- **Final Price:** 600.00
