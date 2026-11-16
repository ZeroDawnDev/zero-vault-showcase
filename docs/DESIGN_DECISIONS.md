# Zero Vault — Engineering Design Decisions

<p align="center">
  <strong>Technology Choices, Trade-offs & Engineering Rationale</strong>
</p>

---

## 1. Purpose

This document records the major engineering decisions behind Zero Vault.

It explains why particular technologies and development approaches were selected, what alternatives could be considered, and how these decisions influence the project's evolution.

The objective is to make the reasoning behind the implementation transparent and provide a reference for future development.

---

## 2. Frontend — React

**Decision:** React

### Rationale

Zero Vault requires an interactive interface for financial dashboards, transaction management, and data visualization.

React provides a component-based development model that supports reusable interface elements and structured application state.

### Alternatives Considered

| Technology | Consideration |
|---|---|
| React | Component-based ecosystem and flexibility |
| Vue | Alternative component-based framework |
| Angular | More opinionated application framework |
| Vanilla JavaScript | Less framework overhead, but more manual organization |

### Trade-off

React introduces additional dependencies and application complexity, but provides flexibility for developing a larger interactive dashboard.

**Decision Status:** Selected.

---

## 3. Frontend Language — TypeScript

**Decision:** TypeScript

### Rationale

Financial applications work with structured information such as transaction amounts, dates, categories, and account identifiers.

TypeScript provides static type checking that helps identify incompatible data structures during development.

### Benefits

- Better code organization.
- Improved editor support.
- Explicit data structures.
- Reduced type-related mistakes.
- Easier maintenance as the application grows.

### Trade-off

Type definitions require additional development effort, but improve maintainability.

**Decision Status:** Selected.

---

## 4. Backend — Python & FastAPI

**Decision:** Python with FastAPI

### Rationale

Python provides a broad ecosystem for data processing, financial calculations, API development, and future intelligent analysis.

FastAPI provides a structured approach to building backend APIs with request validation and automatic API documentation.

### Alternatives Considered

| Technology | Consideration |
|---|---|
| FastAPI | Lightweight Python API framework |
| Django | Full-featured Python web framework |
| Flask | Minimal Python web framework |
| Node.js | JavaScript-based backend alternative |

### Trade-off

FastAPI requires deliberate decisions about authentication, database management, and application structure rather than providing every feature through a built-in framework.

**Decision Status:** Selected.

---

## 5. Database — SQLite

**Decision:** SQLite

### Rationale

Zero Vault initially targets personal financial management rather than a large multi-user financial platform.

SQLite offers a lightweight relational database that operates without requiring a separate database server.

### Benefits

- Simple local deployment.
- Minimal infrastructure requirements.
- Relational data organization.
- Transaction support.
- Straightforward backups.

### Alternatives Considered

| Database | Consideration |
|---|---|
| SQLite | Lightweight local database |
| PostgreSQL | Advanced relational database for larger deployments |
| MySQL | Established relational database |
| MongoDB | Document-oriented database |

### Trade-off

SQLite is appropriate for the initial application, but concurrent access, remote deployment, and multi-user requirements may eventually justify a server-based database.

**Decision Status:** Selected for the current development stage.

---

## 6. Gmail Integration

**Decision:** Explore Gmail as an initial financial notification source.

### Rationale

Financial institutions and payment providers may send transaction notifications through email.

These notifications can provide a practical starting point for reducing manual transaction entry without requiring a direct integration with every financial institution.

### Trade-off

Email notifications are not guaranteed to represent a complete financial history.

Messages may be delayed, unavailable, duplicated, or formatted differently between providers.

Therefore, email-based extraction should be treated as a supplementary transaction collection method rather than a universal replacement for bank synchronization.

**Decision Status:** Integration implementation requires verification.

---

## 7. Local-First Development Direction

**Decision:** Begin with a lightweight local application.

### Rationale

The initial development target is an individual personal finance environment.

A local-first approach reduces infrastructure requirements and gives the application a straightforward development and testing environment.

### Benefits

- Reduced hosting complexity.
- Direct local database access.
- Lower initial infrastructure costs.
- Greater control over local financial records.

### Trade-off

Local deployment introduces responsibilities around device security, database backups, software updates, and data recovery.

A future hosted version would require a more extensive security and infrastructure model.

**Decision Status:** Current development direction.

---

## 8. Modular Integration Strategy

**Decision:** Design future financial integrations around independent provider-specific modules.

### Rationale

Different financial institutions expose different authentication methods, data formats, and synchronization capabilities.

A provider-specific integration layer can isolate these differences from the central transaction-management system.

### Intended Model

```text
      Financial Providers
               |
       +-------+-------+
       |       |       |
       v       v       v
     Bank   Payment  Email
     Module  Module  Module
       |       |       |
       +-------+-------+
               |
               v
       Common Data Model
               |
               v
       Financial Database
```

### Trade-off

A modular approach introduces additional interfaces and abstractions, but reduces the need to rewrite core application logic whenever a new provider is added.

**Decision Status:** Architectural direction for future integrations.

---

## 9. Private Implementation & Public Showcase

**Decision:** Maintain separate private implementation and public documentation repositories.

### Rationale

The public repository is intended to communicate the project's engineering approach, product direction, and development progress without exposing proprietary implementation details or sensitive configuration.

### Repository Responsibilities

| Repository | Responsibility |
|---|---|
| Private repository | Application source code and internal development |
| Public showcase | Documentation, diagrams, approved screenshots, and project demonstrations |

### Trade-off

Maintaining separate repositories requires documentation to be updated independently of the implementation.

However, this provides a clearer boundary between public project presentation and private development assets.

**Decision Status:** Selected project strategy.

---

## 10. Design Decision Review

Technical decisions are not permanent.

As Zero Vault grows, decisions should be reviewed when requirements change.

| Decision | Reconsider When |
|---|---|
| React | Frontend architecture becomes difficult to maintain |
| TypeScript | Application data structures evolve significantly |
| FastAPI | Backend deployment or performance requirements change |
| SQLite | Multi-user access or concurrency requirements increase |
| Gmail integration | More reliable direct financial data sources become available |
| Local-first approach | Remote access or multi-device synchronization becomes necessary |

---

## 11. Future Engineering Considerations

Potential areas for future evaluation include:

- PostgreSQL for larger deployments.
- Secure cloud synchronization.
- Database encryption at rest.
- Background job processing.
- Automated testing and continuous integration.
- Provider-specific integration adapters.
- Financial data reconciliation.
- Secure backup and restoration.

These are evaluation areas, not commitments to adopt specific technologies.

---

## 12. Conclusion

Zero Vault's technical foundation prioritizes simplicity, maintainability, and incremental development.

The selected technologies provide a practical starting point for building a personal finance application while leaving room for more advanced integrations and deployment models.

Recording these decisions makes the project's engineering direction understandable and provides a basis for evaluating future architectural changes.

---

<p align="center">
  <strong>ZERO VAULT</strong>
  <br>
  One Vault. Complete Financial Visibility.
</p>