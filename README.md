# One8 Product Page A/B Test

**A/B testing a product page redesign for conversion and revenue impact — synthetic dataset, SQL analysis, and statistical hypothesis testing.**

---

## Business Problem

One8 wants to determine whether a new product-page experience (**Variant B** — enhanced with richer product information, reviews, and size guidance) improves customer conversion and revenue compared with the existing experience (**Variant A**).

## Objective

This project tests whether Variant B produces a statistically significant improvement in:

- **Conversion rate** — % of sessions that result in a purchase
- **Add-to-cart rate** — % of sessions that add a product to cart
- **Revenue per session** — average revenue generated per visitor

## Dataset

- **10,000** simulated website sessions
- Random **A/B assignment** (~50/50 split between Variant A and Variant B)
- **Product categories**: Athleisure Apparel, Performance Footwear, Formal Footwear, Fragrances, Accessories
- **Devices**: Mobile, Desktop, Tablet
- **Prices**, purchase behavior (`added_to_cart`, `purchased`), and resulting **revenue** per session

> **Note:** The dataset is synthetically generated for this portfolio project. Session-level outcomes are simulated; product categories and price bands are grounded in One8's real, publicly listed product lines rather than generic placeholders.

## Tools

```
Python
Pandas
NumPy
SQL / SQLite
SciPy
Matplotlib
Google Colab
```

## Methodology

```
Python
 ↓
Generate experiment data
 ↓
SQL analysis
 ↓
Conversion analysis
 ↓
Statistical testing
 ↓
Revenue analysis
 ↓
Business recommendation
```

## Key Results

```
Conversion:
A = 10.95%
B = 12.70%
p = 0.00684

Revenue/session:
A = ₹377.42
B = ₹425.08
p = 0.1027
```

Conversion and add-to-cart both cleared the 95% confidence threshold (p < 0.05). Revenue per session was directionally higher for Variant B but did not reach statistical significance in this sample.

## Conclusion

**Variant B significantly improved conversion, but the observed revenue increase was not statistically significant.** The recommendation is to ship Variant B — prioritizing mobile users and higher-consideration categories like Formal Footwear, where the lift was strongest — while extending the test window to confirm the revenue impact before treating it as a confirmed gain.

## Project Structure

```
one8-product-page-ab-test/
├── README.md
├── generate_data.py              # builds the synthetic session dataset
├── analysis_queries.sql          # SQL answering each business question
├── analysis.py                   # runs SQL + statistical significance tests
├── one8_ab_test_sessions.csv     # the dataset
├── results/
│   ├── One8_AB_Test_Report.pdf
│   ├── chart_funnel.png
│   ├── chart_device.png
│   └── chart_category.png
└── notebooks/
    └── Statistical_Test_Results.ipynb
```

## How to Run

```bash
pip install pandas numpy scipy
python generate_data.py
python analysis.py
```

---
*This project demonstrates an end-to-end product analytics workflow: experiment design, SQL-based funnel analysis, and hypothesis testing — the same pipeline used for real product A/B tests.*

