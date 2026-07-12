<p align="center">
  <img src="site/assets/favicon.svg" alt="OTel Studio" width="64">
</p>

<h1 align="center">OTel Studio</h1>

<p align="center">
  A UI-driven, topology-aware OpenTelemetry data generator.<br>
  Realistic correlated traces, logs, and metrics — against any OTel-compatible backend, no app deployment required.
</p>

<p align="center">
  <a href="https://otel-studio.xplurdata.com">Live Site</a> ·
  <a href="https://otel-studio.xplurdata.com/documentation.html">Documentation</a> ·
  <a href="https://xplurdata.com">XplurData</a>
</p>

<p align="center">
  <img alt="License" src="https://img.shields.io/badge/license-MIT-blue.svg">
  <img alt="Docker" src="https://img.shields.io/badge/docker-ready-2496ED.svg?logo=docker&logoColor=white">
  <img alt="OpenTelemetry" src="https://img.shields.io/badge/OpenTelemetry-native-f5a800.svg">
</p>

---

## Why OTel Studio

Most observability teams can't test their pipelines realistically because they don't have good data generators.

| Tool | Limitation |
|---|---|
| `telemetrygen` | CLI-only, random data, no service topology, no UI |
| hotrod / astronomy-shop | Full demo apps — heavy to deploy, not configurable |
| k6 / Gatling | Load-testing tools, not observability-focused — no trace/log/metric correlation |
| Hand-written scripts | Every team reinvents the same wheel |

OTel Studio sits between "too simple" and "too heavy": drop in a Docker image, point it at your collector, and get realistic correlated traces + logs + metrics in under 60 seconds.

## Features

- **25 realistic service topologies** — actual parent-child request chains across Web App, Infrastructure, APM, Cloud Native, and Chaos/Stress categories, not random noise
- **Correlated signals** — logs share trace IDs with the spans that produced them
- **Chaos scenarios** — dedicated error-storm, cardinality-burst, and latency-spike modes for testing alerting and dashboards
- **Multi-endpoint fanout** — send to two or more OTel backends (e.g. Grafana + Elastic) simultaneously, with independent TLS/mTLS per endpoint
- **Geo / IP simulation** — tag generated telemetry with realistic regional IP ranges and GeoIP-resolvable attributes, or safe RFC 5737 test ranges
- **Synthetic PII** — opt-in, per-scenario synthetic user data (RFC 2606 reserved domains only) for testing redaction/DLP pipelines
- **Advanced scenario controls** — custom attributes, span duration overrides, weighted status codes
- **Real system data** — optionally tail real log files and Docker container logs/metrics alongside simulated traffic
- **One-click stack presets** — Grafana Alloy, OpenTelemetry Collector, Elastic APM, Honeycomb, Jaeger, SigNoz, OpenObserve, Datadog, New Relic, Dynatrace, Lightstep

## Quick Start

```bash
docker run -d --name otel-studio -p 3002:3002 \
  -e OTEL_ENDPOINT="http://your-collector:4317" \
  -e OTEL_PROTOCOL="grpc" \
  -e ADMIN_PASS="change-me" \
  otel-studio:latest
```

Open `http://localhost:3002`, log in, pick a scenario, hit Start.

Full setup, environment variables, and every feature documented at **[otel-studio.xplurdata.com/documentation.html](https://otel-studio.xplurdata.com/documentation.html)**.


## License

MIT — see [LICENSE](LICENSE).

---

<p align="center">
  Built by <a href="https://xplurdata.com"><img src="https://xplurdata.com/XplurData.svg" alt="XplurData" height="14" valign="middle"> XplurData</a>
</p>
