⸻

Developer Standard Operating Procedure (SOP)

Purpose

This document defines the engineering standards, development workflows, and operational practices for all projects maintained by this team.

The purpose of this SOP is to:
	•	Ensure consistent engineering practices
	•	Reduce technical debt
	•	Improve code quality and maintainability
	•	Provide clear development workflows
	•	Ensure security, testing, and deployment standards
	•	Align engineering processes with GitLab, Jira, and enterprise security tools

This SOP applies to:
	•	The current application rebuild
	•	All future projects
	•	All developers contributing to team-managed repositories

⸻

1. Engineering Principles

All projects should adhere to the following principles:

Maintainability

Code should be easy to understand, modify, and extend.

Simplicity

Prefer simpler designs over complex abstractions.

Consistency

Follow the established patterns of the project.

Transparency

Code, pipelines, releases, and architecture should be clearly documented.

Traceability

All changes must be traceable from:

Jira Ticket → Git Branch → Merge Request → CI Pipeline → Release → Deployment

Security

Security scanning and safe coding practices are mandatory.

⸻

2. Core Development Tools

Tool	Purpose
GitLab	Source control, CI/CD pipelines, merge governance
Jira	Project planning, backlog, issue tracking
Artifactory	Artifact and container registry
SonarQube	Code quality analysis
Black Duck	Open-source dependency scanning
Prisma Cloud / Twistlock	Container vulnerability scanning
Fortify	Static application security scanning
GitLab Wiki	Project documentation


⸻

3. Repository Structure

Each repository should follow a predictable structure.

Example:

/app
  /src
  /tests
  /scripts
  /deploy
    /helm
    /k8s
/docs
  /architecture
  /decision-log
.gitlab
  /merge_request_templates
.gitlab-ci.yml
README.md
CONTRIBUTING.md
CHANGELOG.md
CODEOWNERS

Documentation Locations

Document	Location
Project overview	README.md
Developer workflow	CONTRIBUTING.md
Release history	CHANGELOG.md
Architecture	Wiki or /docs
Runbooks	Wiki
Technical decisions	docs/decision-log


⸻

4. Branching Strategy

Branch Types

Branch	Purpose
main	Production-ready code
feature/*	Feature development
bugfix/*	Non-production bug fixes
hotfix/*	Production-critical fixes
release/*	Optional release stabilization

Branch Naming

Branch names should include Jira ticket IDs.

Example:

feature/ABC-142-add-payment-validation
bugfix/ABC-201-fix-timeout
hotfix/ABC-399-production-null-error

Protected Branch Rules

Protected branches include:

main
release/*

Restrictions:
	•	No direct pushes
	•	Merge requests required
	•	Pipeline must pass
	•	Required approvals

⸻

5. Development Workflow

Standard Development Flow

Jira Ticket Created
       ↓
Branch Created
       ↓
Feature Developed
       ↓
Tests Written
       ↓
Merge Request Opened
       ↓
Pipeline Executes
       ↓
Code Review
       ↓
Merge to main
       ↓
Release / Deployment


⸻

6. Feature Development Process

Each feature must follow the steps below.

1. Create or reference a Jira ticket

Features must be tied to a Jira issue.

2. Design consideration

Medium or large features require a brief design explanation.

Include:
	•	problem being solved
	•	affected systems
	•	API or data changes
	•	rollout strategy
	•	rollback considerations

3. Create branch

Branch from main.

4. Implement feature

Follow coding standards.

5. Write tests

Tests must validate:
	•	business logic
	•	integration points
	•	failure scenarios

6. Open merge request

Include:
	•	Jira reference
	•	change summary
	•	testing evidence
	•	risk considerations

7. Code review

MR must be approved before merge.

⸻

7. Bug Fix Process

Bug fixes must follow a structured process.

Required Steps
	1.	Identify and reproduce issue
	2.	Determine root cause
	3.	Implement fix
	4.	Add regression test
	5.	Verify fix does not affect other flows
	6.	Document in MR

Required MR Details

Include:
	•	root cause
	•	reproduction steps
	•	validation steps
	•	regression test explanation

⸻

8. Coding Standards

Code Structure

Code should follow clear separation of responsibilities.

Examples:

Layer	Responsibility
Controller/API	Request handling
Service/Domain	Business logic
Integration	External APIs
Data access	Database interaction

Guidelines
	•	Keep modules small and focused
	•	Avoid large utility dumping grounds
	•	Avoid hidden business logic in controllers
	•	Prefer explicit configuration over hardcoded values
	•	Centralize integration logic

⸻

9. Code Review Standards

Code review is mandatory for all changes.

Reviewers should check for:
	•	correctness
	•	maintainability
	•	architecture alignment
	•	security concerns
	•	test coverage
	•	readability

MR Best Practices

Merge requests should:
	•	be reasonably sized
	•	include clear descriptions
	•	reference Jira tickets
	•	include testing evidence

⸻

10. Definition of Done

A change is considered complete when:
	•	code implementation is finished
	•	tests pass
	•	new tests added where needed
	•	SonarQube quality gate passes
	•	security scans pass
	•	documentation updated
	•	MR approved
	•	release notes prepared if needed

⸻

11. Testing Strategy

Testing expectations:

Test Type	Purpose
Unit tests	Validate business logic
Integration tests	Validate system interactions
API tests	Validate external contracts
Regression tests	Prevent bug reoccurrence
Smoke tests	Validate deployments

Requirements
	•	new logic requires unit tests
	•	integration changes require integration tests
	•	bug fixes require regression tests

⸻

12. CI/CD Pipeline Structure

The CI/CD pipeline will be implemented using GitLab.

Pipeline Stages

validate
build
scan
test
release
deploy

Stage Descriptions

Validate
	•	linting
	•	formatting
	•	configuration validation

Build
	•	compile code
	•	build container
	•	produce artifacts

Scan
Enterprise security scans:
	•	SonarQube
	•	Black Duck
	•	Fortify
	•	Prisma/Twistlock

Test
	•	unit tests
	•	integration tests
	•	API tests

Release
	•	create semantic version tag
	•	generate GitLab release
	•	update changelog

Deploy
	•	deploy to environments
	•	track deployment status

⸻

13. Security Scanning

Security scans are mandatory.

Tools used:

Tool	Purpose
SonarQube	Code quality
Black Duck	Open-source dependencies
Fortify	Static security scanning
Prisma Cloud / Twistlock	Container security

GitLab pipelines will:
	•	trigger scans
	•	validate results
	•	block merges if severity thresholds are exceeded

⸻

14. Release Management

Releases follow semantic versioning.

Example:

v1.0.0
v1.1.0
v1.1.1

Version Types

Type	Meaning
Major	Breaking change
Minor	New feature
Patch	Bug fix

Release Process
	1.	Code merged to main
	2.	Create version tag
	3.	Generate GitLab release
	4.	Update changelog
	5.	Deploy to environment

⸻

15. Changelog Policy

The project must maintain a changelog.

Example format:

## [1.2.0] - YYYY-MM-DD

### Added
New features

### Changed
Behavior updates

### Fixed
Bug fixes

### Security
Security improvements


⸻

16. Documentation

Project documentation is stored in the GitLab Wiki.

Wiki Structure

Recommended pages:

Home
System Overview
Architecture
Developer Setup
CI/CD Pipeline
Deployment Process
Security Scanning
Runbooks
Migration Notes

Documentation Updates

Documentation must be updated when:
	•	architecture changes
	•	deployment changes
	•	APIs change
	•	operational processes change

⸻

17. Refactoring Policy

Refactoring is allowed under defined scopes.

Small Refactor

Allowed during feature work.

Medium Refactor

Requires review awareness.

Large Refactor

Requires:
	•	Jira ticket
	•	design discussion
	•	phased implementation

⸻

18. Architecture Guardrails

To prevent codebase drift:
	•	business logic should not exist in controllers
	•	database access should be centralized
	•	external integrations should use abstraction layers
	•	configuration must not be hardcoded
	•	secrets must not be stored in repositories

⸻

19. Feature Flags

Feature flags may be used for:
	•	risky changes
	•	gradual rollouts
	•	backward compatibility during migrations

Feature flags must be removed once no longer needed.

⸻

20. Operational Discipline

Developers must consider:
	•	deployment impact
	•	backward compatibility
	•	rollback procedures
	•	configuration changes

Each meaningful change should consider operational impact.

⸻

21. Continuous Improvement

This SOP is a living document.

It should evolve as:
	•	the architecture changes
	•	tooling improves
	•	lessons are learned from incidents

Changes to this SOP should be proposed through merge requests.

⸻
