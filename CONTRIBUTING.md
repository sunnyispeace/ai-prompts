# Contributing Guide

This document describes how developers should contribute to this
project.

For full engineering standards and development practices refer to:

**Developer SOP**

    docs/DEVELOPER_SOP.md

------------------------------------------------------------------------

# Development Overview

All development must follow the traceable workflow:

Jira Ticket → Branch → Merge Request → CI Pipeline → Release →
Deployment

Every change must be tied to a **Jira ticket**.

------------------------------------------------------------------------

# Development Workflow

## 1. Create or Reference a Jira Ticket

All work must be linked to a Jira issue.

Examples:

-   Feature
-   Bug
-   Technical improvement
-   Refactoring

------------------------------------------------------------------------

## 2. Create a Branch

Branch names must include the Jira ticket ID.

Examples:

    feature/ABC-142-add-payment-validation
    bugfix/ABC-201-fix-timeout
    hotfix/ABC-399-production-null-error

Branches should be created from:

    main

------------------------------------------------------------------------

## 3. Implement Changes

While developing:

-   Follow coding standards from the **Developer SOP**
-   Keep functions small and focused
-   Separate business logic from controllers and infrastructure code
-   Avoid unnecessary abstractions
-   Do not commit secrets or credentials

------------------------------------------------------------------------

## 4. Write Tests

New functionality must include tests.

Testing expectations:

  Change Type          Required Tests
  -------------------- ----------------------
  Business logic       Unit tests
  Integration change   Integration tests
  API change           API / contract tests
  Bug fix              Regression test

------------------------------------------------------------------------

## 5. Run Local Validation (Recommended)

Before opening a Merge Request ensure:

-   code compiles
-   tests pass
-   linting passes
-   no obvious security issues

------------------------------------------------------------------------

## 6. Open a Merge Request

Merge Requests must include:

-   Jira ticket reference
-   explanation of change
-   testing performed
-   potential risks

Use the **Merge Request template** when opening the MR.

------------------------------------------------------------------------

# Code Review Process

Every change requires at least one review.

Reviewers verify:

-   correctness
-   architecture alignment
-   security considerations
-   readability
-   sufficient test coverage

Developers should keep merge requests **small and focused**.

------------------------------------------------------------------------

# Definition of Done

A change is considered complete when:

-   Code is implemented
-   Tests pass
-   Required new tests are added
-   CI pipeline passes
-   Security scans pass
-   Documentation updated if necessary
-   Merge request approved

------------------------------------------------------------------------

# Security and Quality Scans

The CI pipeline runs several security tools:

  Tool                       Purpose
  -------------------------- ----------------------------------
  SonarQube                  Code quality
  Black Duck                 Dependency security
  Fortify                    Static application security
  Prisma Cloud / Twistlock   Container vulnerability scanning

Merge requests may be blocked if severe issues are detected.

------------------------------------------------------------------------

# Releases

Releases follow **semantic versioning**.

    vMAJOR.MINOR.PATCH

Examples:

    v1.0.0
    v1.1.0
    v1.1.1

Release notes are maintained in:

    CHANGELOG.md

------------------------------------------------------------------------

# Documentation

Documentation is maintained in:

-   `README.md` (project overview)
-   `docs/` directory
-   GitLab Wiki

Documentation must be updated when:

-   APIs change
-   architecture changes
-   deployment processes change
-   operational procedures change

------------------------------------------------------------------------

# Questions or Improvements

If you believe the development workflow or standards should change:

1.  Create a Jira ticket
2.  Propose changes through a Merge Request
