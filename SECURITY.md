# Security Policy

## Reporting a Vulnerability

If you discover a security vulnerability in OTel Studio or its published Docker image, please report it privately rather than opening a public issue.

**Email:** bridge@xplurdata.com

Please include:
- A description of the vulnerability
- Steps to reproduce, if applicable
- The image tag/version affected

We aim to acknowledge reports within 5 business days.

## Image Scanning

Every published image at `ghcr.io/xplurdata/otel-studio` is scanned for known CRITICAL and HIGH severity vulnerabilities (Trivy) on a weekly schedule and on every update to the scanning workflow. Results are visible via the badge in the [README](README.md) and the [Actions tab](https://github.com/xplurdata/otel-studio/actions/workflows/security-scan.yml).
