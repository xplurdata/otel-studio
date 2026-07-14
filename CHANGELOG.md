# Changelog

All notable changes to OTel Studio will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [1.0.0] - 2026-07-13

### Added
- 25 realistic service topologies across Web App, Infrastructure, APM, Cloud Native, and Chaos/Stress categories
- Correlated logs and traces — logs share trace IDs with the spans that produced them
- Multi-endpoint fanout with independent TLS/mTLS per endpoint
- Geo/IP simulation (realistic regional ranges or RFC 5737 safe test ranges)
- Synthetic PII generation (RFC 2606 reserved domains only)
- Advanced per-scenario controls: custom attributes, span duration overrides, weighted status codes
- Real System Data mode — real log file tailing and Docker container log/metric collection
- One-click stack presets for 12 popular observability backends
- Sequential mode, anomaly injection, and time-limited quota runs
- Webhook notification on quota expiry

[1.0.0]: https://github.com/xplurdata/otel-studio/releases/tag/v1.0.0
