# Instream 1.0.0: Hackney 4 compatibility

Vendored from the Hex `instream` 1.0.0 release (Apache-2.0; see LICENSE).
This keeps the application's existing Instream series, connection, pooling and
UDP writer behavior. Upstream 2.2.1 still requires Hackney 1.x, which carries
known vulnerabilities, so upgrading upstream alone is not a remediation.

Local changes:

- Require Hackney `~> 4.12` instead of `~> 1.1`.
- Read the response body directly from Hackney's normal request/post result
  in QueryRunner and the HTTP line writer. Hackney 3+ no longer returns a
  client reference for those requests. No dependency override is used.
- Match the InfluxDB version response header case-insensitively, since
  Hackney 4 normalizes response header names.

Regression coverage lives in
`apps/proxy_web/test/lib/proxy_web/metrics/instream_hackney_test.exs` and exercises
HTTP reads/writes, authentication, HEAD operations, errors/timeouts and UDP.
Reconcile/remove this copy when upstream supports the patched Hackney API.
