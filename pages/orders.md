---
name: orders
assetId: 43757a79-af2f-4cac-a2c6-fb2f7b163973
type: sql
---

SELECT
  *,
  toDate(toInt32(toFloat64(extractAll(assumeNotNull("Order Date"), 'value: ([0-9.]+)')[1])) - 25569) as order_date,
  toDate(toInt32(toFloat64(extractAll(assumeNotNull("Ship Date"), 'value: ([0-9.]+)')[1])) - 25569) as ship_date,
  "State/Province" as state
FROM sample_superstore_orders_qbzztc
ORDER BY order_date