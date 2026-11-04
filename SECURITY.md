# Security

Threat model, in five lines:

1. **gpu-manager-mcp is read-only by design**: it exposes no tool that writes to,
   overclocks, power-cycles, or terminates anything on the GPU or host.
2. External helpers (`nvidia-smi`, `rocm-smi`) are invoked from a fixed allowlist
   with fixed argv, timeouts, and no shell interpolation — no user input ever
   reaches a command line.
3. The only file the server writes is its own SQLite history store at the
   configured path; treat that path like any local telemetry file.
4. The HTTP transport binds to loopback only; do not expose it — use stdio, or
   put your own auth in front if you deliberately change the bind address.
5. Report vulnerabilities privately via
   [GitHub Security Advisories](https://github.com/quxlzx/gpu-manager-mcp/security/advisories/new);
   expect an ack within 7 days. No public issues for unfixed vulns, please.
