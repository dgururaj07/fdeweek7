# Observability Tools: Logging, Tracing & Monitoring

## Logging
*Collecting, storing and searching log events.*

| # | Tool | Type | Key points |
|---|------|------|------------|
| 1 | **ELK Stack** (Elasticsearch, Logstash, Kibana) | Open source | Logstash/Beats collect and parse logs, Elasticsearch stores and indexes them, Kibana is where you search and view them. |
| 2 | **Splunk** | Commercial | Common in large enterprises (especially finance). Powerful query language (SPL), alerting, security analytics. |
| 3 | **Grafana Loki** | Open source | Lightweight and lower cost. Indexes only labels, not full text. Works closely with Grafana. |

## Tracing
*Following one request as it passes through many services.*

| # | Tool | Type | Key points |
|---|------|------|------------|
| 1 | **Jaeger** | Open source (CNCF) | Built by Uber. Good for spotting where requests slow down between microservices. |
| 2 | **Zipkin** | Open source | Older tracer from Twitter. Simple; works well with Spring Boot / Java apps. |
| 3 | **OpenTelemetry** | Open standard (CNCF) | Vendor-neutral SDKs and standard for producing traces, metrics and logs. Doesn't store data itself; sends it to Jaeger, Zipkin, Datadog, Grafana Tempo, etc. The default way to add tracing to code. |

## Monitoring
*Metrics, dashboards and alerts.*

| # | Tool | Type | Key points |
|---|------|------|------------|
| 1 | **Prometheus** | Open source (CNCF) | Pulls metrics from services on a schedule and stores them as time series. Queried with PromQL. Built-in alerting via Alertmanager. |
| 2 | **Grafana** | Open source | Dashboards on top of Prometheus, Loki, Tempo and many other sources. Often paired with Prometheus. |
| 3 | **Datadog** | Commercial SaaS | All-in-one: metrics, APM/tracing, logs and synthetic tests in one place. |

## Typical Stacks

- **Open-source stack:** OpenTelemetry → Prometheus + Grafana (metrics), Loki (logs), Jaeger or Tempo (traces)
- **Enterprise stack:** Splunk, Datadog, Dynatrace or New Relic, often covering several pillars at once

## Salesforce Note

Salesforce's built-in tools are **Event Monitoring**, **Debug Logs** and **Shield**. Their data is often fed into Splunk or Datadog for wider observability.
