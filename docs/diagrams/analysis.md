# System Analysis

LEANDCORE is a loan management and credit evaluation system designed
around Java, layered architecture, DAO, Oracle Database and PL/SQL.

The system covers the process from client registration and credit
simulation through credit evaluation, approval or rejection, loan
disbursement, amortization, installments, payments, delinquency,
auditing and reporting.

## Clients and credit management

### 1. Main domain concepts

The preliminary domain model identifies the following main concepts:

- User and role management.
- Clients and employment information.
- Credit applications and credit types.
- Credit scoring and evaluation results.
- Loans and disbursements.
- Amortization plans and installments.
- Payments and delinquency.
- Biometrics, auditing and notifications.

These concepts correspond to the preliminary entities defined for the
system:

`User`, `Role`, `Permission`, `Client`, `EmploymentData`,
`CreditApplication`, `CreditScore`, `CreditType`, `Loan`,
`AmortizationPlan`, `Installment`, `Payment`, `Disbursement`,
`Delinquency`, `Biometrics`, `Audit` and `Notification`.

### 2. Relationship between credit application, scoring and loan

A client may submit credit applications over time.

A credit application is evaluated through the scoring process. The
scoring result supports the credit decision, and an approved application
may generate a loan.

The main conceptual flow is:

    Client
        |
        v
    CreditApplication
        |
        v
    CreditScore
        |
        v
    Decision
        |
        v
    Loan

A rejected application does not necessarily generate a loan.

## Credit scoring

### 3. Responsibility of CreditScore and ScoringService

`CreditScore` represents the result of the credit evaluation, while
`ScoringService` is responsible for applying the evaluation rules.

The proposed scoring process is rule-based and considers factors such
as:

- Payment capacity.
- Debt level.
- Income.
- Job seniority.
- Internal payment history.
- Requested amount compared with income.
- Requested term.

The scoring result should be explainable and should preserve the factors
used in the evaluation.

### 4. Should scoring logic belong in the domain entity?

The preliminary design keeps the decision logic in `ScoringService`
rather than placing the full evaluation process inside `CreditScore`.

`CreditScore` represents the resulting business information, while
`ScoringService` coordinates the rules required to calculate that result.

This separation keeps the scoring rules independent from persistence and
user interface concerns.

## Financial operations

### 5. Responsibility of FinanceService

`FinanceService` is responsible for financial calculations required by
the loan process.

The proposed responsibilities include:

- Nominal and effective rate conversion.
- Periodic installment calculation.
- Capital and interest calculation.
- Balance calculation.
- Amortization schedule generation.
- Extraordinary payment scenarios.
- Delinquency calculation.

Financial calculations should remain separated from the user interface
and persistence layers so that they can be tested independently.

### 6. Relationship between loan, amortization and installments

A `Loan` may have an associated `AmortizationPlan`.

The amortization plan contains the structure required to generate the
loan installments.

The conceptual relationship is:

    Loan
      |
      v
    AmortizationPlan
      |
      v
    Installment

Installments are also related to payments and may generate delinquency
information when payment obligations are not met according to the
business rules.

## Payments and loan balance

### 7. Responsibility of PaymentService

`PaymentService` coordinates payment registration and the resulting
balance updates.

A payment is associated with an installment, while the loan balance is
updated as part of the payment processing flow.

The service layer should coordinate these operations instead of placing
persistence logic inside the domain classes.

### 8. Extraordinary payments

The system includes support for extraordinary payments.

These operations may affect the loan balance and the amortization
structure according to the rules defined by the financial engine.

The exact recalculation behavior must be validated during detailed
financial design and implementation.

## Biometrics and security

### 9. Responsibility of BiometricsService

`BiometricsService` represents the biometric authentication component
used to reinforce authentication and protect critical operations.

The biometric component should remain decoupled from the rest of the
application so that its implementation can be replaced or tested
independently.

### 10. Should biometric data be stored directly?

The preliminary proposal recommends avoiding the direct storage of raw
biometric images or biometric data when identifiers or templates can be
used instead.

The final storage mechanism depends on the biometric hardware,
library or provider selected during implementation.

A controlled fallback such as `MockBiometricsService` can be used for
testing when real biometric hardware is not available.

## Audit and notifications

### 11. Responsibility of Audit

`Audit` represents relevant events generated by the system.

The audit process is intended to preserve traceability of important
operations, including security-related and business-critical actions.

`AuditService` coordinates the recording of these events while
persistence remains in the DAO layer.

### 12. Responsibility of Notification

`Notification` represents messages generated for clients or internal
users according to the system functionality.

`NotificationService` coordinates notification operations, while
persistence is handled through the corresponding DAO.

## Users, roles and permissions

### 13. Role-based access control

The system defines `User`, `Role`, `Permission` and `RolePermission`
concepts to support role-based access control.

A role can be associated with users and permissions can be assigned
through the role-permission relationship.

The exact permission matrix will be defined during security and
authorization implementation.

### 14. Password security

Passwords must not be stored as plain text.

The security design should use secure password hashing and verification,
while the concrete implementation will be defined in the security
utilities and authentication module.

## Layered architecture

### 15. Classes per layer

The system is organized using the following architectural layers:

- **ui**: Java Swing interfaces used to interact with the user.
- **controller**: coordinates actions coming from the user interface.
- **service**: contains business rules and coordinates operations.
- **persistence**: contains DAO classes responsible for database access.
- **model**: contains the domain entities of the system.
- **util**: contains shared technical utilities.
- **database**: Oracle Database and PL/SQL objects.

The architectural flow is:

    ui
     |
     v
    controller
     |
     v
    service
     |
     v
    persistence
     |
     v
    model
     |
     v
    Oracle Database

The proposal defines View, Controller, Service, DAO, Model/Entity and
Util as the principal application layers.

### 16. Responsibility of the model layer

The `model` layer represents business concepts such as clients,
applications, loans, payments and other domain entities.

Model classes should contain domain data and behavior that belongs
directly to the represented concept.

Persistence logic should not be placed inside the domain classes.

### 17. Responsibility of the persistence layer

The `persistence` layer provides DAO classes responsible for reading
and writing system information in Oracle Database.

DAO classes isolate database access from business logic.

This separation allows changes in persistence implementation without
requiring domain classes to manage database operations directly.

### 18. Responsibility of the service layer

The `service` layer contains business rules and coordinates operations
between the domain and persistence layers.

Important services identified in the preliminary design include:

- `UserService`
- `ClientService`
- `CreditApplicationService`
- `ScoringService`
- `FinanceService`
- `LoanService`
- `PaymentService`
- `DisbursementService`
- `BiometricsService`
- `AuditService`
- `NotificationService`

### 19. Responsibility of the controller layer

The `controller` layer coordinates application operations initiated by
the user interface.

Controllers delegate business decisions to services instead of
implementing the main business rules themselves.

### 20. Responsibility of the UI layer

The `ui` layer provides the Java Swing interface used by the actors of
the system.

The interface collects information and displays results, while the
business rules remain in the service layer.

## Dependencies between layers

### 21. Allowed dependencies

Dependencies should follow the direction of the architecture:

    ui → controller
    controller → service
    service → persistence
    service → model
    persistence → model
    persistence → util
    service → util

The main domain concepts should remain independent from the user
interface and persistence implementation.

### 22. Forbidden dependencies

The following dependencies should be avoided:

- `model → service`
- `model → persistence`
- `model → controller`
- `model → ui`
- `ui → persistence`
- `ui → database`

This keeps the domain isolated and prevents interface or storage
changes from propagating directly into the business model.

## Business flow

### 23. Main system flow

The proposed system flow is:

    Client registration
            |
            v
        Simulation
            |
            v
        Application
            |
            v
         Scoring
            |
            v
         Decision
          /     \
         /       \
    Rejected    Approved
                   |
                   v
              Disbursement
                   |
                   v
            Amortization
                   |
                   v
             Installments
                   |
                   v
                Payments
                   |
                   v
             Balance update
                   |
                   v
          Audit and reports

This flow represents the main business process described for LEANDCORE.

## Database and PL/SQL

### 24. Responsibility of Oracle Database

Oracle Database is the persistence platform of the project.

The database design is expected to include relational tables,
constraints, sequences, indexes, views and other objects required by
the system.

### 25. Responsibility of PL/SQL

PL/SQL will be used for database-side operations such as:

- Procedures for disbursements and payments.
- Functions for financial calculations and balances.
- Triggers for auditing and state updates.
- Views for reporting and controlled data access.

Transactions and integrity constraints will be used to preserve
consistency during critical operations.

## Object-oriented design decisions

### 26. Inheritance hierarchy

The current preliminary domain analysis does not define inheritance
hierarchies between the principal business entities such as `Client`,
`Loan`, `Payment` or `CreditApplication`.

These classes represent different business concepts and are primarily
related through associations.

A separate implementation hierarchy is identified for biometric
authentication:

    BiometricsService
            ^
            |
    MockBiometricsService

`MockBiometricsService` provides an alternative implementation intended
for testing.

### 27. Association instead of inheritance

Relationships between clients, credit applications, scoring, loans,
installments and payments are modeled as associations because these
classes represent different concepts in the lending process.

For example, a `Loan` is not a specialized form of `Client`, and a
`Payment` is not a specialized form of `Loan`.

Therefore, inheritance is not appropriate for these relationships.

## Final analysis criteria

### 28. Main design principles

The preliminary architecture follows these principles:

- Separation of responsibilities between layers.
- Encapsulation of domain information.
- Separation of business rules from persistence.
- DAO-based database access.
- Centralization of financial rules in the financial service.
- Centralization of credit evaluation rules in the scoring service.
- Decoupling of biometric authentication.
- Secure handling of authentication information.
- Auditability of relevant operations.
- Validation and transaction control for critical operations.

## Analysis status

**Status:** Preliminary system analysis.

The analysis will be refined during implementation as the concrete Java
classes, Oracle schema, financial rules, security mechanisms and
biometric integration are defined.

The class diagram, hierarchy diagram and layers diagram are based on
the decisions documented in this analysis.