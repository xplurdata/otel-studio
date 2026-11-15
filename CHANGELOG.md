# Changelog

All notable changes to OTel Studio will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [2.0.0] - 2026-11-15

### Added
- Bearer token and extra request headers per endpoint, both optional. Stored encrypted, never shown again after saving and never returned by the API, the live state stream or exports.
- Command-line mode switches: `--header`, `--token-env`, `--attr`, `--signals`, `--hosts`, `--providers`, `--regions`, `--cpu`, `--mem`, `--os`, `--rate`, `--error-rate`. The standard `OTEL_EXPORTER_OTLP_ENDPOINT`, `_PROTOCOL` and `_HEADERS` variables are read too.
- Job API (`node dist/api.js`, port 3100): start, list, inspect and stop runs from another application, up to 25 at once, protected by a required `API_TOKEN`.
- Run-wide resource attributes on every resource (for example a tenant or test run id).
- Per-signal switches (traces, logs, metrics).
- Backend verification tool (`verify/`) and contract tests for the vendor presets.
- Container image on GitHub Container Registry: `ghcr.io/xplurdata/otel-studio`, for `linux/amd64` and `linux/arm64`, in two variants: the default image (about 290 MB) and a `-browser` image (about 1.1 GB) that adds Chromium for real-browser RUM. The image holds the build output only: a minified server bundle without source maps, the built web UI and third-party packages.

### Changed
- **No built-in destination.** The image no longer points at `localhost` (which, inside a container, is the container itself). Without `OTEL_ENDPOINT`, nothing is sent until you add an endpoint on the Endpoints page; the Dashboard says so, and Start asks for an endpoint first. The default OTLP protocol is now `http` (protobuf). Command-line mode needs an endpoint from the config file, `--endpoint` or `OTEL_EXPORTER_OTLP_ENDPOINT`.
- OTLP over HTTP now sends protobuf by default (`http`); JSON stays available as `http/json`.
- Vendor presets corrected against current documentation: Dynatrace sends `Authorization: Bearer`, Datadog direct intake points at `https://otlp.datadoghq.com`, Honeycomb Classic sends `x-honeycomb-dataset`.
- The default service name is now `otel-studio` (was `otel-agent`); set `SERVICE_NAME` to keep the old name.
- The container start command is now `node dist/index.js`.
- Endpoint credentials are no longer part of the simulation state sent to the browser or saved in the database.

### Fixed
- The product tour pointed at three sidebar items and the activity stream that no longer existed, so their highlights were missing; it now walks every control and page (15 steps), including Inject Incident, the six simulators, Stats and Settings, and keeps its card inside the window.
- The Dashboard's simulator status showed five of the six simulators; AI Observability is now included.
- The endpoint Test button showed a bare "error:" for an unreachable host; it now says why (for example "connect ECONNREFUSED").
- The Stats page carried a backend-specific example query; it now has a generic cross-check note.
- The endpoint Test button reported a timeout for every real OTLP server; it now tells accepted, credentials refused (401/403), not accepted as OTLP and unreachable apart.
- A URL already ending in `/v1/traces`, `/v1/logs` or `/v1/metrics` was sent to a doubled path.
- Per-service CPU and memory metrics were created for scenarios that were not enabled.
- In command-line mode and the job API, listing scenarios now means "these and no others".

### Security
- The container runs as an unprivileged user (uid 1000) under `tini`, and `docker stop` now flushes pending telemetry and exits cleanly.
- Sign-in is rate limited per user name and address (HTTP 429 after repeated failures); an unknown user takes as long to answer as a wrong password.
- The session cookie is `SameSite=Lax` and `Secure` over HTTPS. Responses carry `X-Content-Type-Options`, `X-Frame-Options`, a `frame-ancestors` policy, `Referrer-Policy` and `Permissions-Policy`, plus `Strict-Transport-Security` over HTTPS. The `X-Powered-By` header is removed and request bodies are limited to 2 MB.
- Dependencies are locked (`package-lock.json`) and installed with `npm ci`. The runtime moved from Node 20 (end of life) to Node 24, SQLite to `better-sqlite3` 12, and the build tools to current versions. `npm audit` reports no high or critical issue; the image scan reports no HIGH or CRITICAL finding and no embedded secret.
- A software bill of materials (CycloneDX) is published with the image. `SECURITY.md` describes how to report a vulnerability.

### Removed
- The Lightstep / ServiceNow Cloud Observability preset: the vendor ended support on 2026-03-01.
### Upgrade notes
- The container no longer runs as root. A bind-mounted `/data` must be writable by uid 1000, and Real System Data needs the Docker socket group or `--user root` (see the documentation).
- The default service name is now `otel-studio` (was `otel-agent`); set `SERVICE_NAME` to keep the old name.
- The container start command is now `node dist/index.js`.

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
[2.0.0]: https://github.com/xplurdata/otel-studio/releases/tag/v2.0.0
