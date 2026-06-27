# NovaMart custom instructions (business rules + gotchas)

Cross-cutting rules the analyst must follow on this dataset. The gotchas also live on the relevant entities
in entities.yaml; this is the one place to scan them.

- **Revenue is completed orders only.** Filter `orders.status = 'completed'`. Cancelled (4,596) and returned
  (2,369) are excluded from revenue; keep all statuses for funnel conversion.
- **Never fan out order totals.** Do not sum an order-level column (e.g. `orders.total_amount`) across an
  `orders -> order_items` join: it multiplies rows and inflates (3.15M correct vs 5.9M fanned). Aggregate
  order-level measures at the order grain.
- **Do not trust `sessions.had_purchase` for Nov-Dec 2024.** 1,089 sessions are wrong (around Black Friday).
  Derive purchase outcome from `events.event_type = 'purchase_complete'` or by joining orders on session_id.
- **Device / app_version.** `events.app_version IS NULL` ~ web; 2.4.0 / 3.2.0 are the mobile app versions.
  `sessions.device` values are web / ios / android (not desktop/mobile/tablet).
