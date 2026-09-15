# Cost-Aware Engineering

Technical architecture is also a financial decision.

For infrastructure decisions estimate:
- compute baseline and autoscaling cost;
- managed database baseline, storage, IOPS, backups, replicas;
- object storage and bandwidth/egress;
- CDN;
- email/SMS/OTP;
- observability/log ingestion and retention;
- third-party API usage;
- payment processor fees;
- support/operational burden;
- engineering time.

Prefer a simpler service with a slightly higher unit price when it materially reduces operational risk and engineering effort, unless scale makes the economics unfavorable.

Document the usage threshold at which a more complex alternative becomes worthwhile.
