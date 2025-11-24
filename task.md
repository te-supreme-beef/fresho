# Product Order Suggestion Accuracy Improvement

## Problem Statement

Fresho is a B2B fresh food marketplace that connects buyers with suppliers. When buyers place orders, they often use informal or natural language product names (e.g., "Tomato" vs "Tomatoes", "gluten-free pork sausage" vs "GLUTEN FREE PORK SAUSAGE", "Stew Pack" vs "Root Veg / Stew Mix Extra large diced 25mm"). The system must map these buyer requests to standardized product catalog items with correct quantities and units.

Currently, the product suggestion system attempts to predict the correct product match for each buyer request. Your goal is to **improve the accuracy** of these predictions by analyzing the data and building a better matching model.

## Objective

Build a model that predicts the correct product match (product name, product ID, quantity, and quantity type) for each buyer request.

**Success metric:** Accuracy of `is_prediction_correct` (all fields must match: product ID, quantity, and quantity type ID)

**Constraints:**
- Predictions must be constrained to products available in `supplier_inventory.jsonl` (the complete catalog for October 2025)
- You may use external data, models, embeddings, or LLMs as part of your solution
- Note: If using LLMs, be mindful of API costs when processing large datasets (723k records)

**Deliverable:** A notebook or script demonstrating your approach, analysis, and model performance

## Data Files

### `predictions.jsonl` (723,421 records)
Contains one month of prediction data (October 2025) with buyer requests, system suggestions, and ground truth confirmations.

**Columns:**
- `ds` — Date
- `selling_company_id` — ID of the supplier
- `buying_company_id` — ID of the company placing the order
- `order_request_id` — Unique identifier for the buyer request
- `order_created_at` — Timestamp when order was created
- `product_order_suggestion_id` — Unique identifier for the suggestion
- `extracted_product_name` — Raw product name from buyer request 
- `extracted_quantity_type_name` — Raw unit of measure from buyer request
- `extracted_quantity` — Raw quantity from buyer request
- `suggested_product_name` — System's suggested standardized product name
- `suggested_quantity_type_name` — Suggested unit of measure
- `suggested_quantity` — Suggested quantity
- `suggested_product_id` — ID of the suggested product
- `suggested_quantity_type_id` — ID of the suggested quantity type
- `is_prediction_correct` — Boolean indicating if suggestion matched confirmation
- `confirmed_product_name` — Product name actually selected by buyer (ground truth)
- `confirmed_quantity_type_name` — Unit of measure actually selected by buyer (ground truth)
- `confirmed_quantity` — Quantity actually selected by buyer (ground truth)
- `confirmed_product_id` — ID of the confirmed product (ground truth)
- `confirmed_quantity_type_id` — ID of the confirmed quantity type (ground truth)

### `supplier_inventory.jsonl` (189,676 records)
Current product inventory as of October 31, 2025. Can be used as a reference for the product catalog.

**Columns:**
- `id` — Unique identifier for the inventory record
- `selling_company_id` — ID of the supplier
- `product_id` — ID of the product
- `product_name` — Standardized product name
- `product_code` — Product code
- `quantity_type_name` — Unit of measure
- `quantity_type_id` — ID of the quantity type
- `created_at` — Timestamp when record was created
- `updated_at` — Timestamp when record was last updated
- `ds` — Date
