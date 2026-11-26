# Collaboration with product and design skills

Use this reference only when the current work crosses a skill boundary. Resolve skills by name and capability, without assuming a global path or host command. The entry point of the current request remains responsible for continuity; collaborators do not recursively invoke each other.

| Owner | Inputs received | Outputs returned | Boundary |
| --- | --- | --- | --- |
| Automation2App, when adopted | UI feasibility issues and verified interface evidence | Approved capability, user journey, operation contract, authorization, states, readiness, acceptance criteria | No automatic adoption for an unrelated UI task; runtime integration waits for its applicable readiness gates |
| Progressive WebUI Workflow | Task, approved constraints, identity, stack | Task/control mapping, disclosure rationale, interaction findings, verification evidence | Does not redefine operations, permissions, brand, or stack |
| design-md | Existing brand evidence or concrete visual proposals | Approved DESIGN.md, brand profile, draft decisions, relevant validation/export results | Does not own operational behavior; CLI lint does not prove visual or runtime quality |
| frontend-design | Brief, task layout constraints, approved identity, open visual decisions | Art direction, sample, copy, composition and visual critique | Creative proposals remain proposals until approved when brand identity changes |
| frontend-ui-engineering, if used | Authorized interaction and visual decisions | Implemented components and implementation findings | Reuses the actual stack and APIs; does not silently add dependencies |

## Entry paths

- From Automation2App: reuse the approved capability and contract. Triage and static design preparation may identify gaps before readiness; do not connect runtime operations prematurely. Report gaps to the existing specification/tracker without creating another plan.
- From an ordinary UI request: use this workflow without adopting Automation2App. Suggest it only if conversion of an automation is actually relevant and requested or agreed.
- With an approved DESIGN.md: read and apply it. Do not restart brand capture or ask again for identity approval within the authorized task.
- Without an approved identity: frontend-design can propose a small sample; design-md distinguishes observed, inferred, proposed, and confirmed values, then records the approved design. These are complementary steps, not competing token sources.
- From design-md or frontend-design: return interaction constraints and verification findings for the requested screens only. Do not turn a small visual fix into a whole-app workflow.

## Resolution and return

User instructions and applicable project rules govern scope. Within that scope, operational effects and authority come from the trusted operation contract, visual rules from the approved design, and interaction acceptance from the project criteria. Creative preference cannot override a permission check or an approved brand.

If these sources conflict materially, describe the conflict and prepare a concrete resolution for the appropriate decision; do not silently select a new authority. For example, an inaccessible brand color requires an accessible variant proposal, not an unapproved brand rewrite or a false conformance claim. Continue unrelated authorized work.

Use existing project artifacts: specification for behavior and decisions, DESIGN.md for visual rules, brand-profile.md for provenance, existing plan/tracker for work, designated evidence for checks. Keep one source per decision and refer to it rather than copying it into every skill.

For each return, state the capability/screen, relevant version or hashes, decision/evidence reused, gap or finding, requested owner action, affected criteria, and pending authorization if any. Re-enter only the affected stage. No state label or successful check grants permission for another action.
