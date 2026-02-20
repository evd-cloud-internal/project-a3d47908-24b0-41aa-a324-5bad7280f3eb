---
name: segments
assetId: 005d8b42-2229-4537-8708-b5ba06bc6200
type: partial
---

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