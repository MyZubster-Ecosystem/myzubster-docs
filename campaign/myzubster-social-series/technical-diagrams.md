# MyZubster Technical Diagram Pack

Reference specifications for the project architecture diagrams.

## 01 — Docker + Onion Architecture

Conceptual layers:
- Edge/public layer: reverse proxy, TLS termination, health checks.
- Application layer: API/application services and orchestration.
- Domain layer: marketplace, orders, payments and escrow business rules.
- Infrastructure layer: PostgreSQL, Redis, storage, external payment/network adapters.
- Restricted/admin lane: operational tooling and privileged services.

Container guidance:
- Keep services isolated by responsibility.
- Expose only the edge entrypoint publicly.
- Prefer private container/network paths for databases and internal services.
- Do not place secrets in images; inject them through the deployment secret mechanism.

Architecture status: reference design; validate against the actual deployment before production use.

## 02 — DDoS Mitigation — Defense in Depth

Request path:
Client → DNS/CDN → DDoS protection → WAF → reverse proxy/API gateway → rate limiting → application services → data services.

Controls:
- Absorb volumetric traffic at the edge where supported.
- Apply WAF/request validation rules.
- Rate-limit expensive and authentication-sensitive endpoints.
- Use connection, request-size and timeout limits.
- Keep databases and internal services off the public network.
- Monitor latency, error rate, saturation and unusual traffic patterns.
- Define escalation, blocking and recovery procedures.

No claim is made that a single layer guarantees DDoS protection.

## 03 — Secure Request Flow

Client → CDN/DDoS/WAF → TLS/reverse proxy → authentication → authorization → rate limit → application/domain service → PostgreSQL/Redis/storage.

Restricted lane:
Admin/operator → privileged gateway → authenticated internal service.

Security checkpoints:
1. TLS at the public boundary.
2. Request validation and size limits.
3. Authentication and authorization.
4. Rate limiting and abuse controls.
5. Least-privilege service/database access.
6. Logging and metrics without leaking secrets.
7. Health checks and controlled failure behavior.

Architecture status: reference flow; confirm implementation and deployment-specific controls before production use.
