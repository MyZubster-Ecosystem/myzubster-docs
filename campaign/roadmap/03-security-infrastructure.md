# 03 — Security & Infrastructure

```text
Internet
  ↓
CDN / DDoS controls
  ↓
WAF / Reverse Proxy
  ↓
Application network
  ↓
Private data services
```

Focus:
- Docker/container isolation.
- Onion-style application boundaries.
- Secrets management.
- TLS and secure ingress.
- Rate limiting and request validation.
- Logging, metrics and alerting.
- Backups and recovery testing.
- DDoS defense in depth.

Exit criteria: security controls are implemented, tested and documented for the actual production topology.
