# Remediation — SQL Injection (practical fixes)

This document lists practical remediation steps and best practices to prevent SQL Injection (SQLi) vulnerabilities.

## 1. Use Prepared Statements / Parameterized Queries
Always separate SQL code from user data. Use parameterized queries / prepared statements in your language or DB driver so user input is passed as a parameter, not concatenated into the SQL string.

**Examples**
- Python (sqlite3/psycopg2): `cursor.execute("SELECT * FROM users WHERE id = %s", (user_id,))`
- PHP (PDO): `$stmt = $pdo->prepare('SELECT * FROM users WHERE id = ?'); $stmt->execute([$id]);`
- C# (ADO.NET): use `SqlParameter` instead of string concatenation.

**Why:** prevents user input from changing SQL structure.

## 2. Input Validation (Allow-listing)
Validate inputs at the boundary. Prefer allow-lists over deny-lists: accept only expected formats (eg. email, username regex, numeric id range). Reject or canonicalize unexpected inputs before they reach the DB layer.

**Why:** reduces attack surface and avoids expensive DB-side checks.

## 3. Escaping / Encoding (only when necessary)
If you cannot use parameterized queries (legacy code), ensure proper escaping of special characters for the target DB. Use the API’s escape helpers — do not write your own ad-hoc escaping unless absolutely necessary.

**Why:** prevents input from closing strings or injecting SQL tokens.

## 4. Principle of Least Privilege
Use database accounts with minimal permissions required for the task. Applications that only read data should not use accounts with write or schema modification privileges.

**Why:** limits damage if an injection is successful.

## 5. Use Stored Procedures & Safe ORMs (with parameters)
Use stored procedures or ORMs that support parameterized queries. Ensure stored procedures themselves do not concatenate SQL with untrusted inputs.

**Why:** encapsulation + parameterization reduces injection opportunities.

## 6. Web Application Firewall (WAF) & Runtime Defenses
Deploy a WAF to catch common injection patterns and block suspicious requests. Use rate limiting, request validation, and anomaly detection to slow/stop automated attacks.

**Why:** provides defense-in-depth and can block exploitation attempts while fixes are deployed.

## 7. Secure Error Handling & Output Encoding
Do not leak database errors to users — use generic error messages and log the detailed error server-side. Encode or escape data before including it in HTML/JS to avoid cross-site injection issues.

**Why:** verbose DB errors give attackers reconnaissance info.

## 8. Logging, Monitoring & Alerts
Log failed input validation, parameter errors, and suspicious query patterns. Create alerts for spikes in errors or slow queries (time-based SQLi usage).

**Why:** early detection short-circuits active exploitation.

## 9. Automated Testing & CI Checks
Add SAST/DAST checks and automated tests (unit + integration) that assert parameterization and sanitized inputs. Include regression tests for known payloads used during pentests.

**Why:** prevents reintroduction of vulnerabilities.

## 10. Patch & Dependency Management
Keep DB drivers, ORMs, and frameworks up to date. Review third-party libraries for security advisories.

---

**Quick remediation checklist for devs**
- Replace string-concatenated SQL with parameterized queries.
- Validate and canonicalize all user input.
- Use least-privilege DB accounts.
- Add logging/monitoring and WAF.
- Add automated tests that include known payloads.
