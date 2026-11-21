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

## Open Source vs Paid

| Category | Open source (free to self-host) | Paid / commercial |
|----------|---------------------------------|-------------------|
| **Logging** | ELK Stack, Grafana Loki, OpenSearch, Graylog, Fluentd / Fluent Bit (collectors) | Splunk, Datadog Logs, Sumo Logic, New Relic Logs |
| **Tracing** | Jaeger, Zipkin, Grafana Tempo, OpenTelemetry (instrumentation standard) | Datadog APM, New Relic, Dynatrace, Honeycomb, AWS X-Ray |
| **Monitoring** | Prometheus, Grafana, Zabbix, Nagios, VictoriaMetrics | Datadog, New Relic, Dynatrace, AppDynamics |

> **Note:** Several open-source tools also sell paid hosted versions or enterprise editions, for example **Elastic Cloud** (ELK) and **Grafana Cloud** (Grafana, Loki, Tempo, Prometheus). The software is free, but managed hosting and support cost money. Some paid tools, such as Splunk and Datadog, have limited free tiers.

## FDE Perspective

A Forward Deployed Engineer (FDE) works inside the customer's environment. The main rule is to **use what the customer already runs** rather than bring in a new stack. Beyond that, FDEs depend on a few extra groups of tools:

| Need | Tool | Open source / Paid | Why an FDE uses it |
|------|------|--------------------|--------------------|
| **Customer's cloud** | AWS CloudWatch + X-Ray | Paid (pay-as-you-go) | Default logs, metrics and traces when the customer runs on AWS. |
| | Azure Monitor / Application Insights | Paid (pay-as-you-go) | Same role for customers on Azure. |
| | Google Cloud Observability | Paid (pay-as-you-go) | Same role for customers on GCP. |
| **Error tracking** | Sentry | Source-available + paid SaaS | Catches exceptions with stack traces and user context. Quick to add during a pilot. |
| **LLM / AI observability** | Langfuse | Open source + paid cloud | Traces prompts, responses, token cost and latency for AI agents and RAG apps. |
| | LangSmith | Paid (free tier) | Tracing and evaluation for LangChain / LangGraph apps. |
| | Arize Phoenix | Open source | Local LLM tracing and evals, built on OpenTelemetry. |
| | Helicone | Open source + paid cloud | Proxy that logs every LLM API call with cost and latency. |
| **Instrumentation** | OpenTelemetry | Open source | Instrument once and send data to whatever backend the customer uses. |
| **API checks** | Postman | Paid (free tier) | Reproduce customer API issues, run collection tests and set up monitors. |
| **On-site debugging** | `kubectl logs`, `jq`, `grep` | Open source | Fast triage when there's no dashboard access yet. |

**FDE takeaways**
- **Plug into the customer's stack first.** If they use Splunk or Datadog, send your data there.
- **Use OpenTelemetry** so the same instrumentation works with any backend.
- **For AI deployments, add LLM observability** (Langfuse, LangSmith or Phoenix). Ordinary APM tools don't show prompt quality, hallucinations or token cost.
- **Build a demo dashboard early.** Showing latency, errors and usage helps prove value during a pilot.

## Typical Stacks

- **Open-source stack:** OpenTelemetry → Prometheus + Grafana (metrics), Loki (logs), Jaeger or Tempo (traces)
- **Enterprise stack:** Splunk, Datadog, Dynatrace or New Relic, often covering several pillars at once

## Salesforce Note

Salesforce's built-in tools are **Event Monitoring**, **Debug Logs** and **Shield**. Their data is often fed into Splunk or Datadog for wider observability.
