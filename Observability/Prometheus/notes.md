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
