# Scaling and Capacity

Scaling starts with workload characteristics, not user-count vanity metrics.

## Estimate

Capture expected registered users, active users, peak concurrent users, average and peak requests per second, read/write ratio, average response size, upload/download volume, data growth per day, retention, and traffic shape.

Average RPS = requests per day / 86,400. Peak RPS should use an explicit peak multiplier or measured data.

## Typical evolution

1. Single deployable application + relational database.
2. CDN/object storage where media requires it.
3. Multiple stateless application instances behind a load balancer.
4. Cache only for demonstrated hot paths/coordination needs.
5. Queue/workers for asynchronous workloads.
6. Database tuning, indexing, connection management, vertical scaling, then read replicas where justified.
7. Partitioning/sharding only when simpler database scaling approaches are insufficient.
8. Service extraction only when boundaries justify the operational complexity.

Define measurable triggers before adding each layer.
