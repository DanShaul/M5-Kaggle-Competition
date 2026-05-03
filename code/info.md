# M5 Forecasting Dataset Terms Cheat Sheet

## Files Overview

### 1. sales_train_validation.csv / sales_train_evaluation.csv
Main time series data (unit sales per product per day)

Columns:
- id: Unique identifier (item + store + validation/evaluation)
- item_id: Product identifier
- dept_id: Department (subcategory)
- cat_id: Category (e.g., FOOD, HOBBIES, HOUSEHOLD)
- store_id: Store identifier
- state_id: State identifier (CA, TX, WI)
- d_1 ... d_1913: Daily unit sales (number of items sold on that day)

---

### 2. calendar.csv
Maps time index to real dates and events

Columns:
- date: Actual calendar date (YYYY-MM-DD)
- wm_yr_wk: Walmart week number
- weekday: Day of week (e.g., Monday)
- wday: Numeric day of week (1ÃƒÆ’Ã‚Â¢ÃƒÂ¢Ã¢â‚¬Å¡Ã‚Â¬ÃƒÂ¢Ã¢â€šÂ¬Ã…â€œ7)
- month: Month number (1ÃƒÆ’Ã‚Â¢ÃƒÂ¢Ã¢â‚¬Å¡Ã‚Â¬ÃƒÂ¢Ã¢â€šÂ¬Ã…â€œ12)
- year: Year
- d: Day index (matches d_1, d_2, ...)
- event_name_1: Name of primary event/holiday (if exists)
- event_type_1: Type of primary event (e.g., Cultural, National)
- event_name_2: Secondary event (if exists)
- event_type_2: Type of secondary event
- snap_CA: SNAP program active in California (0/1)
- snap_TX: SNAP program active in Texas (0/1)
- snap_WI: SNAP program active in Wisconsin (0/1)

---

### 3. sell_prices.csv
Tracks item prices over time per store

Columns:
- store_id: Store identifier
- item_id: Product identifier
- wm_yr_wk: Walmart week number
- sell_price: Price of the item in that store during that week

---

### 4. sample_submission.csv
Submission format for predictions

Columns:
- id: Matches validation/evaluation ids
- F1 ... F28: Forecasted sales for next 28 days

---

## ÃƒÆ’Ã‚Â°Ãƒâ€¦Ã‚Â¸Ãƒâ€šÃ‚Â§Ãƒâ€šÃ‚Â± Hierarchy Terms

- state_id: Geographic region (CA, TX, WI)
- store_id: Specific store within a state
- cat_id: High-level category (e.g., FOOD)
- dept_id: Subcategory within category
- item_id: Individual product

---

## ÃƒÆ’Ã‚Â°Ãƒâ€¦Ã‚Â¸ÃƒÂ¢Ã¢â€šÂ¬Ã…â€œÃƒâ€¦Ã‚Â  Time Series Terms

- d_x: Day index (e.g., d_1 = first day, d_1913 = last training day)
- F1ÃƒÆ’Ã‚Â¢ÃƒÂ¢Ã¢â‚¬Å¡Ã‚Â¬ÃƒÂ¢Ã¢â€šÂ¬Ã…â€œF28: Forecast horizon (next 28 days to predict)

---

## ÃƒÆ’Ã‚Â°Ãƒâ€¦Ã‚Â¸ÃƒÂ¢Ã¢â€šÂ¬Ã¢â€žÂ¢Ãƒâ€šÃ‚Â¡ Business Context Terms

- sales: Number of units sold (target variable)
- sell_price: Product price (used for demand modeling)
- SNAP: Government food assistance indicator affecting demand
- events: Holidays or special days influencing sales

---

## ÃƒÆ’Ã‚Â¢Ãƒâ€¦Ã‚Â¡ÃƒÂ¢Ã¢â‚¬Å¾Ã‚Â¢ÃƒÆ’Ã‚Â¯Ãƒâ€šÃ‚Â¸Ãƒâ€šÃ‚Â Key Concepts

- Hierarchical Data: Products organized by category, store, and state
- Time Series: Sequential daily sales data
- Intermittent Demand: Many zero-sales days for some products
- Forecast Horizon: Predicting future values (28 days ahead)
- 