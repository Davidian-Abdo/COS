OCOS— Open Construction Operating system

Category: Open-source, AI-native construction operational runtime
Product ambition: Become the Linux of construction operations.

1. Vision
OCOS is an open, adaptable operational foundation that enables construction companies to coordinate projects through a shared operational model, a configurable deterministic kernel, and a hierarchical network of AI agents and human operators.

It does not require every company to adopt the same software, organizational structure, terminology, or work methods. Instead, it provides a universal protocol through which different systems, people, and agents can exchange operational information, coordinate responsibilities, execute authorized actions, and verify outcomes.

Core principle: One interoperable operational state. Many specialized operators. Configurable company rules. Continuously coordinated work. Traceable responsibility. Verified physical outcomes.

2. Problem

Construction operations depend on continuous coordination between labor, equipment, materials, suppliers, subcontractors, engineering, procurement, quality control, finance, and project management.

Operational information is fragmented across spreadsheets, messaging applications, documents, BIM models, scheduling tools, ERP systems, and individual knowledge. Managers must manually reconcile these sources, discover blockers, chase commitments, assign work, resolve conflicts, and determine what actually happened.

Existing digital tools can manage individual disciplines and automate specific workflows, but companies still need to coordinate the overall production process across organizational and software boundaries.

The fundamental problem is the gap between planned work, executable work, actual execution, and verified outcomes.

3. Core innovation

OCOS combines four foundational capabilities:

1. Universal operational input protocol: A common, context-sensitive way to ingest and validate operational information from any supported source.
2. Hierarchical operational agent runtime: A configurable organization of AI agents and human operators that manages responsibilities, missions, dependencies, and exceptions.
3. Deterministic operational kernel: A controlled execution environment that maintains authoritative state transitions, permissions, invariants, and auditable event history.
4. Company adaptation and extensibility: A configuration and domain-pack system that adapts OOF to different companies, trades, contractual structures, and operating procedures without rewriting the kernel.

The product is not merely a shared database, workflow engine, chatbot, or collection of agents. It is a runtime that continuously converts operational information into coordinated, authorized action.

4. Universal Operational Input Protocol

Every supported input must be mapped into a common operational model regardless of its origin: human forms, voice, mobile reports, email, messaging, spreadsheets, BIM, ERP, sensors, APIs, or AI agents.

The protocol defines universal operational primitives:

- Entities: Projects, work packages, activities, people, organizations, resources, materials, locations, contracts, drawings, and other identifiable objects.
- Facts and assertions: Reported or observed conditions with provenance, timestamps, confidence where appropriate, and verification status.
- Requirements: Preconditions, constraints, information requirements, resource requirements, and acceptance criteria.
- Commitments: Promised actions or outcomes, owners, deadlines, and dependencies.
- Missions: Bounded assignments to humans or agents, with authority, deadlines, completion criteria, and escalation policies.
- Evidence: Measurements, photographs, documents, delivery records, inspection results, and other supporting artifacts.
- Decisions: Authorized choices, approvals, rejections, overrides, and their recorded rationale.
- State transitions: Proposed, authorized, executed, verified, or rejected changes to operational entities.
- Exceptions: Missing information, conflicts, blockers, deviations, disputes, and situations outside existing rules.

Each input is interpreted according to its context and mapped to the relevant entities, units, workflow, authority, and validation requirements. The system must preserve the distinction between a reported fact, an AI inference, a verified observation, and an authorized decision.

A universal event envelope is combined with versioned, context-specific information contracts. Required information depends on the operation being performed; users should not be forced to populate irrelevant fields.

Missing information must remain explicitly unknown rather than being silently invented. OCOS should request additional information only when needed to make a decision or execute an operation safely.

5. Deterministic Operational Kernel

The kernel maintains the authoritative OOF operational state and controls consequential transitions.

Responsibilities include:

- Entity identity, relationships, and references.
- Event ingestion, validation, ordering, and reconciliation.
- State machines and permitted transitions.
- Identity, permissions, delegation, and authority checks.
- Requirements, invariants, and mandatory approval gates.
- Mission lifecycle, deadlines, escalation, and completion.
- Idempotent command execution and failure handling.
- Append-only history of consequential actions and corrections.
- Evidence references, provenance, and audit integrity.
- Configuration versioning and compatibility.

The kernel must remain small, stable, testable, and independent of any specific AI model.

Generative AI interprets ambiguous inputs, investigates exceptions, proposes plans, and selects among permitted capabilities. Deterministic mechanisms govern authorization, mandatory constraints, state transitions, and recorded execution.

The system must be able to reconstruct its operational state from recorded events without relying on an LLM to reproduce previous reasoning.

6. Hierarchical Agent Runtime

OCOS organizes agents according to operational responsibility rather than merely dividing software functions into independent bots.

Global Operations Steward

Maintains the cross-domain operational picture, identifies conflicts and high-impact blockers, prioritizes exceptions, coordinates domain stewards, and proposes or initiates authorized recovery actions.

Domain stewards

Manage defined operational domains such as planning, field execution, procurement, resources, quality, evidence, and commercial obligations.

Work-package coordinators

Coordinate all prerequisites, resources, commitments, participants, and state transitions associated with a particular package of work.

Specialist agents

Perform bounded tasks such as quantity reconciliation, document comparison, delivery tracking, constraint detection, reporting, evidence checks, and schedule-impact analysis.

Human operators

Provide information, execute physical work, resolve exceptions, make decisions, exercise delegated authority, and validate outcomes where required.

Every agent role must declare its scope, responsibilities, triggers, available tools, permissions, output contract, completion conditions, delegation rules, failure policies, and escalation behavior.

The hierarchy is logical, not a requirement for a separate model or process per role. The global steward has cross-domain visibility but cannot override mandatory safety, security, legal, quality, or authority constraints.

7. Mission and Accountability Protocol

Agents must be able to assign real, traceable missions to humans or other agents, not merely issue notifications.

Every mission contains:

- Objective and expected outcome.
- Accountable owner and designated assignee.
- Deadline and operational priority.
- Preconditions and dependencies.
- Permitted actions and authority boundaries.
- Completion criteria and evidence requirements.
- Parent mission and affected operational entities.
- Acknowledgment, progress, blockage, and escalation states.
- Final result and verification status.

Accountability distinguishes five roles: accountable owner, executor, decision authority, verifier, and affected party. These roles may overlap where appropriate but must not be conflated automatically.

For every consequential action, OOF preserves the trigger, source information, interpretation, applicable rules, proposed action, authorization, execution result, evidence, and subsequent outcome.

The audit must include failed actions, rejected proposals, overrides, missed deadlines, corrections, disputes, and unsuccessful interventions.

The system records responsibility and contributing factors without treating an AI inference or temporal correlation as proof of contractual causation.

Audit records should be append-only and tamper-evident, with authenticated actors, stable event identifiers, protected evidence references, and explicit correction events. Integrity mechanisms must not be misrepresented as proof that the original information was true.

8. Construction Production-Control Engine

The initial operational focus is autonomous work-package readiness and constraint resolution.

For each work package, OOF models:

- Scope, quantities, location, method, and production targets.
- Dependencies and preceding work.
- Labor, skills, equipment, materials, and access requirements.
- Drawings, instructions, permits, inspections, and approvals.
- Supplier and subcontractor commitments.
- Quality requirements and acceptance criteria.
- Planned dates, actual progress, remaining quantities, and resource consumption.
- Responsible parties, evidence, risks, and downstream consequences.

OCOS continuously determines whether work is ready, identifies missing prerequisites, assigns constraint-resolution missions, tracks commitments, evaluates feasible alternatives, and coordinates authorized execution.

When an event disrupts production, the system evaluates affected activities, resource conflicts, potential idle time, milestone consequences, and recovery options.

The engine must distinguish hard constraints from preferences, conditional dependencies, uncertain forecasts, and company-specific practices. Local optimization must not violate project-wide dependencies, mandatory quality gates, or authority restrictions.

Reported progress, measured progress, completed work, accepted work, and quantities certified for payment must remain distinct states.

9. Exception Resolution and Controlled Adaptation

Construction operations inevitably encounter conditions that existing workflows do not fully anticipate.

When the system encounters an unknown or contradictory situation, it must:

1. Detect and register the exception.
2. Identify affected entities, dependencies, resources, and commitments.
3. Separate known facts, uncertain information, assumptions, and missing evidence.
4. Assign an appropriate steward to investigate and coordinate resolution.
5. Develop feasible responses and evaluate their consequences and authority requirements.
6. Obtain required human decisions or execute a pre-authorized action.
7. Track the intervention and verify its outcome.
8. Propose improvements to company rules or domain packs when recurring exceptions expose a genuine gap.

AI may propose new rules, workflows, information requirements, and capabilities. Changes affecting operational behavior must be validated, tested, versioned, and approved according to configured governance. The system must never silently expand its own authority.

10. Company Operations Compiler

OCOS must adapt to existing company practices instead of requiring companies to adopt one universal organizational model.

The Company Operations Compiler transforms company materials into a structured, validated runtime configuration.

Inputs may include organizational charts, role descriptions, procedures, forms, spreadsheets, approval matrices, existing software records, terminology, and documented exceptions.

The compiler extracts and proposes:

- Entity mappings and company terminology.
- Role definitions and authority matrices.
- Operational workflows and state transitions.
- Required information and evidence.
- Approval rules and escalation paths.
- Mission templates and completion criteria.
- Integration mappings and validation rules.

Ambiguities, contradictory procedures, missing responsibilities, and unresolved authority conflicts must be surfaced for human resolution.

Configurations must be versioned, testable, and independently deployable. Company-specific behavior must not require forking the kernel. Mandatory safety, security, and applicable legal constraints cannot be disabled through ordinary configuration.

11. Open Ecosystem and Interoperability

OOF is designed as an open, extensible foundation with documented protocols, stable interfaces, domain packs, and independently developed adapters.

The ecosystem includes:

- Core kernel: Operational state, permissions, missions, event history, and execution controls.
- Protocol implementations: Typed schemas, event contracts, information requirements, and compatibility rules.
- Company configurations: Organization structures, workflows, responsibilities, and approval policies.
- Domain packs: Construction-specific work methods, resource models, quality gates, production logic, and operational capabilities.
- Adapters: IFC, BCF, IDS, scheduling tools, BIM applications, ERP, procurement, spreadsheets, email, messaging, sensors, and APIs where supported.
- Operator interfaces: Mobile reporting, voice input, dashboards, exception queues, approvals, and machine interfaces.
- Capability exchange: Versioned, tested, documented and governed contributions from engineering firms, software developers, consultants, and domain specialists.

OCOS must coexist with existing systems and remain useful without Beam-stack products. External systems remain authoritative for records they own unless a separate, explicit agreement establishes otherwise.

Beam-stack integrations are first-class: Planitor contributes planning intent and quantities; Chantier Manager contributes site execution and validated operational records; additional products contribute their respective domain data.

Interoperability must preserve source authority, data provenance, permissions, version compatibility, and explicit handling of stale or conflicting information.

12. Human Authority, Safety, and Trust

OOF is designed for progressively increasing autonomy, not unrestricted AI control.

Autonomous actions must be bounded by explicit permissions, validated preconditions, operational constraints, and configured risk levels.

Examples of potentially permitted autonomous actions include gathering information, reconciling records, sending authorized requests, assigning routine missions, tracking commitments, preparing reports, and proposing alternative sequences.

Actions such as physical execution, safety-critical decisions, contractual commitments, purchasing beyond delegated limits, financial approvals, quality acceptance, and consequential resource changes require the authorization appropriate to the operation.

No digital record alone proves that physical work occurred. Evidence must be evaluated according to the operation and required assurance level.

OOF must expose uncertainty, preserve conflicting evidence, recognize unavailable integrations, and escalate situations that cannot be resolved within its authority.

13. Initial Product Scope

The first release focuses on one high-value workflow: work-package readiness and constraint resolution on a real construction project.

Minimum scope:

1. Import planning, quantities, resource assignments, procurement records, and field reports from a small number of existing sources.
2. Build the operational graph and identify missing prerequisites, commitments, and affected work packages.
3. Assign and track human or agent missions to resolve constraints.
4. Follow up on commitments and escalate overdue or unresolved issues.
5. Propose feasible recovery actions with explicit downstream consequences.
6. Require authorization for consequential changes.
7. Reconcile execution evidence and update the operational state.
8. Preserve a complete trace of the issue, responsibility, decisions, actions, and verified outcome.
9. Operate initially in shadow mode before enabling bounded autonomous actions.

The first deployment should target a contractor and work type where production quantities, dependencies, resources, and recurring coordination problems can be measured.

14. Success Criteria

OCOS must demonstrate measurable improvement in real operations, not merely more complete digital records or more sophisticated agents.

Key metrics include:

- Proportion of upcoming work packages genuinely ready for execution.
- Time from detecting a blocker to resolving it.
- Planned versus actual production and milestone reliability.
- Avoidable labor and equipment idle hours.
- Material-related disruptions and missed commitments.
- Rework, rejected quantities, and quality deviations.
- Human coordination effort per work package.
- Accuracy of detected constraints and downstream-impact predictions.
- Incorrect actions, missed prerequisites, and unnecessary escalations.
- Completeness and integrity of accountability records.
- Operational overhead compared with measurable benefits.

Baseline measurements must be established before deployment, and improvements must be evaluated against actual project evidence.

15. Long-Term Vision
OCOS evolves from a constraint-resolution engine into a universal construction operational runtime capable of coordinating increasingly complex workflows across contractors, subcontractors, suppliers, engineering firms, project owners, and software systems.

Its long-term objective is to progressively automate the discovery of operational problems, resolution of routine constraints, assignment of work, coordination of resources, verification of outcomes, and improvement of company procedures while preserving appropriate human authority.

The platform becomes more capable through reusable domain packs, company configurations, operational evidence, and independently developed integrations—not by requiring every company to use the same applications or management structure.

16. Guiding Principle

Any company can describe how it operates. Any authorized participant can contribute operational information. Any human or agent can be assigned a bounded responsibility. Every consequential action is traceable. Every verified outcome updates the shared operational state
OCOS is not simply software that understands construction.

It is an open operational foundation that turns construction information into controlled, coordinated, accountable action.
