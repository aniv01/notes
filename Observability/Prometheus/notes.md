## Prometheus
---
Prometheus is a server component and you typically run one instance of Prometheus in each environment.

It's cross platform and it runs same way on Windows and Linux.

Prometheus actually runs whole lot of functions inside one server.

- `Scheduler` component which fetches metrics from the systems that you want to monitor. It uses a pull model.
You have to expose metrics from your systems then prometheus will fetch them every min or 30s depending upon your configuration.
- Prometheus stores all those metrics in a `time series` database. Which is also running in the server.
- Prometheus has it's own query language because time series data doesn't really fit well with standard SQL and there is an HTTP api running in the server, which lets you to run those queries.
- There is also a simple `web-ui` running in the server which is there for a basic admin tasks. You can use to check the server configs and check if prometheus can reach the systems that it's configured to monitor.
- Prometheus UI is not a fully featured dashboard so you can't use it to display the overall health of the system.
- Prometheus has advanced alerting system, you can register alerting rules in the normal prometheus server and when the rules trigger there is a separate component which takes action on those alerts (sending emails, pages, creating tickets etc..)

## What makes prometheus so Awesome?
---
Any system that you want to monitor needs to run an exporter, which provides all it's metrics via an HTTP endpoint.
Your prometheus grabs the metrics from those endpoints on a schedule and it stores them. It doesn't care what type of system it is looking at or what the metrics actually mean.

The job of the exporter is to provide metrics that are relavent to that system in a standard promethus format.

**Example prometheus format**
```
# HELP process_cpu_seconds_total Total user and system CPU time
# TYPE process_cpu_seconds_total counter
process_cpu_seconds_total 5.23

# HELP worker_jobs_total Worker jobs handled
# TYPE worker_jobs_total counter
worker_jobs_total{status="processed"} 1000
worker_jobs_total{status="falied"} 200
```

## Metric types in prometheus
---
- A `counter` always increases and it is useful for storing things like number of HTTP reqs or the amount of cpu time used.
```
http_requests_total 1000000
cpu_seconds_total 3000
```
- `Gauges` are snapshot of a changing value, something like the number of HTTP requests being processed. They can go up or down, unlike counter they always increase.
```
http_requests_active 2000
memory_allocated_bytes 4.832e+09
```
- `Summaries` are for recording average size of something, that could be time taken for a calculation or size of a file that was processed.
```
calculation_seconds_count 3
calculation_seconds_sum 15
```
In the example above 3 calculations took 15 mins on an average of 5s for each calculation.
- `Histograms` records data in buckets.
```
calculation_seconds_bucket{le="1"} 0
calculation_seconds_bucket{le="5"} 3
calculation_seconds_bucket{le="10"} 6
calculation_seconds_bucket{le="20"} 9
calculation_seconds_bucket{le="60"} 10
```
