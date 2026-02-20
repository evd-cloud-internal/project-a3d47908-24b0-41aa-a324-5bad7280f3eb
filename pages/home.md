---
name: Home
assetId: 031aed0f-e9d0-40b0-a204-0b26dd884d45
type: page
---

# Superstore Executive Overview

```sql orders
SELECT
  *,
  toDate(toInt32(toFloat64(extractAll(assumeNotNull("Order Date"), 'value: ([0-9.]+)')[1])) - 25569) as order_date,
  toDate(toInt32(toFloat64(extractAll(assumeNotNull("Ship Date"), 'value: ([0-9.]+)')[1])) - 25569) as ship_date,
  "State/Province" as state
FROM sample_superstore_orders_qbzztc
ORDER BY order_date
```

{% big_value
  data="orders"
  value="sum(Sales)"
  fmt="usd0"
  title="Total Sales"
  width=11
/%}

{% big_value
  data="orders"
  value="sum(Profit)"
  fmt="usd0"
  title="Total Profit"
  width=11
/%}

{% big_value
  data="orders"
  value="sum(Profit) / sum(Sales)"
  fmt="pct1"
  title="Profit Ratio"
  width=11
/%}

{% big_value
  data="orders"
  value="sum(Profit) / count(distinct \"Order ID\")"
  fmt="usd2"
  title="Profit per Order"
  width=11
/%}

{% big_value
  data="orders"
  value="sum(Sales) / count(distinct \"Customer Name\")"
  fmt="usd0"
  title="Sales per Customer"
  width=11
/%}

{% big_value
  data="orders"
  value="avg(Discount)"
  fmt="pct1"
  title="Avg Discount"
  width=11
/%}

{% big_value
  data="orders"
  value="sum(Quantity)"
  fmt="num0"
  title="Quantity"
  width=11
/%}

## Sales by Geography

{% map %}
  {% area_layer
    geography="us_states"
    match_by="name"
    data="orders"
    area_id="state"
    value="sum(Profit) / sum(Sales)"
    value_fmt="pct1"
    color_palette=["#c84a22", "#e8a064", "#cacaca", "#6795ac", "#1c688d", "#00557f"]
    legend_label="Profit Ratio"
  /%}
{% /map %}

{% row %}
  {% area_chart
      data="orders"
      x="order_date"
      y="sum(Sales)"
      series="Segment"
      date_grain="month"
      y_fmt="usd0"
      title="Sales by Segment"
      subtitle="Monthly sales broken down by customer segment"
  /%}

  {% area_chart
      data="orders"
      x="order_date"
      y="sum(Sales)"
      series="Category"
      date_grain="month"
      y_fmt="usd0"
      title="Sales by Category"
      subtitle="Monthly sales broken down by product category"
  /%}
{% /row %}