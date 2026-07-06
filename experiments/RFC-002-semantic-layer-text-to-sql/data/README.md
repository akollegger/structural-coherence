# Data

Once RFC-002 is frozen, document here:

- The source domain/warehouse (preferably derived by normalizing *backward* from a real
  denormalized warehouse, per the RFC's validity-threat mitigation, rather than only
  denormalizing forward from a clean schema).
- The D0–D3 denormalization sweep and the committed denormalization-degree metric
  (redundancy, constraint loss, name opacity weights).
- The schema-volume rungs (~2–128 tables, log-spaced) and the method used to hold the
  answerable-question set fixed while scaling.
- The C0–C4 context documents (opaque / appropriate / consistent / conventional /
  explicit-declaration), authored from a single shared term inventory at constant
  documentation quality — flag here once a blind rater has confirmed each rung differs
  only in its intended mechanism.
- The per-class question inventory (schema linking, multi-fact-table disambiguation,
  snapshot-vs-flow, calculated metrics, sentinel keys, time anchoring).

Keep raw data/warehouse dumps out of git if they exceed a few MB — `.gitignore` them and
note the external location instead.
