<!--
Sync Impact Report
Version change: template -> 1.0.0
Modified principles:
- [PRINCIPLE_1_NAME] -> I. Training-First Product Scope
- [PRINCIPLE_2_NAME] -> II. Offline-First, Cloud-Ready Architecture
- [PRINCIPLE_3_NAME] -> III. Security Boundaries Are Mandatory
- [PRINCIPLE_4_NAME] -> IV. Story-Level Verification Required
- [PRINCIPLE_5_NAME] -> V. Keep It Simple, Observable, and Reversible
Added sections:
- Implementation Constraints
- Delivery Workflow
Removed sections:
- None
Templates requiring updates:
- ✅ .specify/templates/plan-template.md
- ✅ .specify/templates/spec-template.md
- ✅ .specify/templates/tasks-template.md
- ✅ .specify/templates/constitution-template.md
- ⚠ pending: .specify/templates/commands/*.md (directory not present in this repository)
Follow-up TODOs:
- None
-->

# ContosoDashboard Constitution

## Core Principles

### I. Training-First Product Scope
ContosoDashboard exists for training, not production delivery. Every change MUST preserve the
project's teaching value, keep the implementation understandable to learners, and avoid adding
production-only complexity unless that complexity is the subject of the exercise. Features MUST
work locally with the repository's bundled stack and MUST document any intentional simplifications
or known limitations when they affect behavior. Rationale: this repository is explicitly a training
application, so clarity and approachability outweigh enterprise-grade breadth.

### II. Offline-First, Cloud-Ready Architecture
Features MUST run without external cloud dependencies by default. Infrastructure concerns such as
storage, authentication adapters, and integrations MUST be introduced behind explicit interfaces so
the training implementation can remain local while preserving a clear migration path to Azure or
equivalent services. New persistence or file workflows MUST prefer relative, portable configuration
and MUST not hard-code environment-specific assumptions. Rationale: the repository is designed to
teach proper abstraction while remaining usable in offline training environments.

### III. Security Boundaries Are Mandatory
Authentication, authorization, and data access rules are non-negotiable even in a mock system.
Protected pages and endpoints MUST enforce identity checks, service-layer operations MUST validate
tenant or membership access before returning data, and file or document features MUST store assets
outside public web roots unless an authorized delivery path is implemented. Features handling user
input MUST validate type, size, and ownership constraints before persistence. Rationale: training
code must demonstrate correct security boundaries, especially for IDOR prevention and role-based
access control.

### IV. Story-Level Verification Required
Each specification MUST define independently testable user stories, and each implementation plan
MUST state the concrete verification approach for the touched behavior. Code changes MUST be
validated with the narrowest practical executable check for the modified slice; if automated tests
do not yet exist, the spec, plan, or task artifacts MUST record the required manual verification
steps. Cross-cutting changes that affect authentication, authorization, persistence, or document
handling MUST include regression coverage or an explicit justification for why executable coverage is
not yet feasible. Rationale: the workflow teaches spec-driven delivery, so every slice must be
demonstrable and verifiable in isolation.

### V. Keep It Simple, Observable, and Reversible
Implementations MUST favor the smallest change that satisfies the current story, reuse existing
services and patterns before introducing new abstractions, and avoid speculative generalization.
Behavior that can fail in user-visible ways MUST surface clear feedback, and important state
changes such as uploads, deletes, shares, and access denials SHOULD leave a trace through logging,
notifications, or auditable records appropriate to the feature. Data and file workflows MUST be
ordered to avoid partial failure states when a reversible sequence is available. Rationale: simple,
observable flows are easier to teach, debug, and extend safely.

## Implementation Constraints

- The canonical application stack is ASP.NET Core 10.0 with Blazor Server, Entity Framework Core,
	and SQLite for local development.
- New features MUST fit the existing layered structure of Pages, Services, Models, and Data unless
	the specification explicitly justifies a different boundary.
- Mock authentication remains acceptable for training, but production-only claims in code or docs
	MUST be avoided unless they are clearly labeled as future guidance.
- File storage features MUST use an abstraction such as `IFileStorageService`, store files outside
	`wwwroot`, and generate unique storage paths before saving database metadata.
- User-facing acceptance criteria MUST remain platform-agnostic, while implementation artifacts MAY
	name concrete framework types, services, and pages.

## Delivery Workflow

1. Specifications MUST describe prioritized user stories, edge cases, functional requirements, and
	 measurable success criteria before planning begins.
2. Implementation plans MUST pass the Constitution Check by naming the affected security boundary,
	 the offline-first design decision, the verification approach, and any justified complexity.
3. Tasks MUST be organized by user story so each slice can be implemented and validated
	 independently; foundational tasks may block story work only when they are truly shared
	 prerequisites.
4. Reviews MUST reject changes that bypass service-layer authorization, introduce unexplained
	 infrastructure coupling, or omit verification for behavior that changed.
5. Documentation that changes user workflows, storage behavior, or security assumptions MUST be
	 updated in the same change set.

## Governance

This constitution overrides conflicting local process notes for this repository. Amendments require
the constitution file to be updated together with any affected templates or guidance documents, and
the Sync Impact Report at the top of this file MUST summarize those propagated changes. Compliance
reviews occur during planning, implementation, and review: every plan must satisfy the Constitution
Check, every task list must preserve story independence, and every code review must confirm security
boundaries and verification evidence.

Versioning follows semantic versioning for governance documents. MAJOR versions indicate removed or
redefined principles that require teams to change how they work. MINOR versions add a new principle
or materially expand an existing requirement. PATCH versions clarify wording without changing
expected behavior. This adoption establishes the first concrete constitution for the repository, so
the initial version is 1.0.0.

Operational guidance for day-to-day work lives in README.md, the StakeholderDocs directory, and the
Spec Kit templates under `.specify/templates/`; those artifacts MUST stay aligned with this
constitution.

**Version**: 1.0.0 | **Ratified**: 2026-05-11 | **Last Amended**: 2026-05-11
