# Zero Vault — Security & Privacy

<p align="center">
  <strong>Security Principles for Personal Financial Data</strong>
</p>

---

## 1. Security Overview

Zero Vault is designed to manage sensitive personal financial information.

Financial records, account information, transaction histories, and external service credentials require careful protection.

Security is therefore a core engineering requirement throughout the application lifecycle.

This document describes the security principles, protection mechanisms, and future security objectives of Zero Vault.

---

## 2. Security Objectives

The security model follows five primary objectives:

| Objective | Description |
|---|---|
| Confidentiality | Prevent unauthorized access to financial information |
| Integrity | Protect financial records against unauthorized modification |
| Availability | Maintain access to stored financial information |
| Authentication | Verify access to connected services |
| Privacy | Minimize unnecessary collection and exposure of personal data |

These objectives guide security-related design and implementation decisions.

---

## 3. Application Security Boundaries

Zero Vault consists of several components with different security responsibilities.

```text
             USER
              |
              v
       FRONTEND APPLICATION
              |
              v
        BACKEND API
              |
       +------+------+
       |             |
       v             v
    DATABASE     EXTERNAL APIs
       |             |
       v             v
  Financial      Authorized
    Records      Integrations
```

### Security Responsibilities

| Component | Security Responsibility |
|---|---|
| Frontend | Avoid exposing sensitive information unnecessarily |
| Backend | Validate requests and enforce application rules |
| Database | Protect stored financial records |
| External integrations | Use authorized and limited access |
| Configuration | Protect secrets and environment-specific settings |

The backend should remain the enforcement boundary for sensitive operations.

---

## 4. Authentication & Authorization

External financial integrations may require authorization before accessing account-related information.

### Gmail Integration

Gmail authorization should use Google's supported OAuth 2.0 mechanisms.

Security requirements include:

- Use an appropriate OAuth consent flow.
- Request only the permissions required.
- Avoid collecting account passwords.
- Protect access and refresh tokens.
- Support authorization revocation.
- Handle expired credentials safely.

The exact OAuth scopes and token-storage implementation must be verified against the private application.

---

## 5. Credential Management

Sensitive credentials should never be embedded directly in application source code.

### Sensitive Information

Examples include:

- OAuth client secrets.
- API keys.
- Access tokens.
- Refresh tokens.
- Database encryption keys.
- External service credentials.

### Recommended Practices

- Store secrets outside source-controlled files.
- Use environment variables or a secure secret store.
- Exclude local configuration files from Git.
- Never publish credentials in screenshots or logs.
- Rotate credentials if exposure is suspected.
- Restrict access to production credentials.

Example `.gitignore` entries:

```gitignore
.env
.env.*
!.env.example

*.db
*.sqlite
*.sqlite3

credentials.json
token.json

secrets/
private/
```

An example configuration file should contain placeholder values only.

---

## 6. Financial Database Protection

Zero Vault uses SQLite as its database technology.

Financial records stored locally should be protected against unauthorized access.

### Protection Requirements

- Restrict filesystem access to the database.
- Avoid publishing database files.
- Exclude real financial records from public repositories.
- Maintain secure backups.
- Validate database operations.
- Protect sensitive exports.

### Additional Protection

For stronger local-data protection, future development may consider:

- Database encryption at rest.
- Operating-system-level file protection.
- Encrypted backups.
- Secure deletion procedures.
- Recovery testing.

SQLite usage alone does not guarantee encryption or access control.

---

## 7. API Security

The backend API should enforce appropriate controls for every sensitive operation.

### Recommended Controls

| Control | Purpose |
|---|---|
| Input validation | Reject malformed requests |
| Authentication | Verify the requesting user |
| Authorization | Restrict access to permitted resources |
| Error handling | Avoid exposing internal implementation details |
| Rate limiting | Reduce abuse of sensitive endpoints |
| CORS configuration | Restrict permitted browser origins |
| HTTPS | Protect data in transit |

These controls should be implemented according to the application's deployment environment and access model.

---

## 8. Data Privacy

Zero Vault follows a data-minimization approach.

Only information required for financial tracking and application functionality should be collected and retained.

### Privacy Principles

- Avoid unnecessary email-content storage.
- Extract relevant transaction information rather than retaining entire messages.
- Do not expose personal financial records in public demonstrations.
- Avoid logging sensitive transaction details.
- Keep credentials separate from transaction data.
- Provide clear handling and retention policies.

Financial data should never be used in public screenshots without appropriate anonymization.

---

## 9. External Integration Security

Future integrations may connect Zero Vault to Japanese banks and payment services.

Potential providers include:

- ゆうちょ銀行
- Rakuten Bank
- SMBC
- Credit card providers
- PayPay
- ICOCA

### Integration Requirements

Each integration must be evaluated independently.

Security considerations include:

1. Prefer official APIs and authorized access methods.
2. Use provider-approved authentication mechanisms.
3. Request the minimum necessary permissions.
4. Protect tokens and connection credentials.
5. Validate externally retrieved information.
6. Provide a way to disconnect integrations.
7. Handle authorization expiration and revocation.

No integration should bypass provider security controls or terms of service.

---

## 10. Public Repository Protection

Zero Vault uses a public showcase strategy while keeping its implementation repository private.

The public repository should contain documentation and approved demonstration materials rather than sensitive implementation assets.

### Public Repository May Contain

- README and project documentation.
- Architecture diagrams.
- Anonymized screenshots.
- Feature descriptions.
- Development roadmap.
- Technology overview.

### Public Repository Must Not Contain

- API keys or OAuth secrets.
- Real transaction records.
- Database files.
- Private configuration files.
- Personal account information.
- Authentication tokens.
- Unreleased proprietary source code.

Before every public release, review the files being committed.

---

## 11. Security Incident Response

If a credential or sensitive financial record is exposed, the response should be immediate.

### Recommended Response

```text
       Security Incident
              |
              v
      Identify Exposure
              |
              v
     Revoke Affected Access
              |
              v
      Rotate Credentials
              |
              v
      Assess Data Exposure
              |
              v
       Remove Public Data
              |
              v
       Review Root Cause
              |
              v
      Apply Preventive Fix
```

Removing an exposed secret from the latest commit is not always sufficient. Previously published Git history, forks, and cached copies may remain accessible.

Affected credentials should be revoked or rotated.

---

## 12. Security Development Roadmap

| Security Improvement | Priority | Status |
|---|---|---|
| Keep credentials out of source code | Critical | Verify implementation |
| Exclude database files from public Git | Critical | Required |
| Protect OAuth tokens | High | Verify implementation |
| Validate backend inputs | High | Verify implementation |
| Restrict API access | High | Verify implementation |
| Secure backup strategy | Medium | Planned |
| Database encryption at rest | Medium | Evaluate |
| Security testing | High | Planned |
| Dependency vulnerability checks | Medium | Planned |

The status column should be updated only after reviewing the actual implementation.

---

## 13. Conclusion

Zero Vault handles information that deserves a high level of privacy and protection.

Its security approach emphasizes credential protection, controlled integrations, database privacy, API validation, and responsible public documentation.

The long-term objective is to establish a secure foundation for centralized personal financial management.

---

<p align="center">
  <strong>ZERO VAULT</strong>
  <br>
  One Vault. Complete Financial Visibility.
</p>