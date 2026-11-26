---
name: progressive-webui-workflow
description: Organize, build, or review web interfaces using task-centered progressive disclosure, approved project identity, accessible components, and browser verification. Reuse completed design work; do not adopt Automation2App, redesign a brand, or change the stack merely by invoking this workflow.
---

# Progressive WebUI Workflow

Organize interfaces around what people need to accomplish. Use five stages: task triage, visual direction, assembly, static review, and browser verification. Resume at the first stage lacking applicable evidence; a review request does not authorize implementation.

## Context and collaboration

Read the project's instructions, requested scope, existing decisions, stack, and acceptance criteria. Reuse the canonical specification, plan, tracker, and evidence locations. Do not repeat interviews or create a second backlog when the required information already exists.

When another skill owns part of the work, resolve it by name and actual capabilities. Read [skill collaboration](references/skill-collaboration.md) when handing work to or receiving work from Automation2App, design-md, or frontend-design. References identify collaborators, not recursive calls or mandatory dependencies.

If an input is missing, identify the specific gap and continue independent authorized work. Report unavailable skills or tools and the equivalent process used; do not claim to invoke an unavailable auditor, slash command, or browser.

## Stage 1: Task triage

Start with the user's task, relevant decisions, required information, and recovery paths. Then map these to existing operations and settings; do not generate one input for each backend field.

| Task or decision | User need | Placement | Control or presentation | Rationale and operation mapping |
| --- | --- | --- | --- | --- |
| Select source | Identify material to process | Essential | Source selector | Required input for the approved operation |
| Choose output quality | Trade quality against processing time | Contextual | Preset, if meaningful | Maps to documented settings with visible effects |
| Inspect diagnostics | Investigate a failure | Advanced | Details or separate panel | Available when needed, with sensitive data removed |
| Service credential | Authenticate the service | Internal | No distributed client control | Managed through the project's trusted configuration |

Use placements according to need:
- Essential: information and actions needed for the primary task.
- Contextual: relevant choices, modes, or presets; these may appear alongside essential inputs.
- Advanced: less frequent tuning or diagnostics, accessible through an appropriate disclosure.
- Internal: implementation details with no useful user decision; preserve required administrative workflows separately.

For a focused task, aim for one dominant primary action and no more than four additional task controls in its initial view. Count inputs, selectors, disclosure triggers, and each independently actionable option; do not count an entire multi-button group as one. Record navigation and utility controls separately and assess total visible complexity across all tiers. Treat the number as a review heuristic, not a universal pass/fail threshold. Explain exceptions for expert workflows, tables, or tasks requiring more inputs. Read-only views need not acquire a primary CTA.

Numeric fields belong in the primary view when they express the task itself, such as an amount or date. Keep incidental tuning out of that path. Do not invent presets, a drawer, or a three-step wizard if the task does not need them.

Never conceal destinations, material effects, warnings, or required confirmations to meet a control-count target. UI visibility does not grant authority; the trusted backend enforces authorization. If presets affect an operation, expose their meaningful effects and preserve the operation's confirmation rules.

## Stage 2: Visual direction and language

Read the approved DESIGN.md, brand materials, and existing components before proposing tokens. Use design-md for requested capture, definition, validation, or application; do not run its CLI just to read an approved design. Use frontend-design for art direction within those constraints, reusing an existing applicable plan.

When new visual direction is needed, propose palette roles, typography, layout, and a small wireframe or visual sample. One or two type families may be appropriate; preserve approved tokens instead of inventing a mandatory four-to-six-color palette. Review the plan against the actual brief before building. For a new or changed brand identity, keep the proposal separate until the user approves the concrete sample; use design-md to record that decision.

Treat familiar design patterns as prompts for critique, not forbidden styles. A justified or approved cream palette, cards, uppercase treatment, or other pattern may be appropriate. Operational screens do not need a marketing hero.

Use consistent action names and plain language. Explain errors and recovery; distinguish pending, completed, limited, failed, cancelled, and uncertain outcomes using the project's actual contract. Do not present optimistic feedback as verified completion.

## Stage 3: Structural assembly

Only implement within the authorized scope and the project's applicable readiness gates. Reuse the existing stack and components; frontend-ui-engineering may support implementation. Do not install shadcn, change frameworks, or add dark mode solely to satisfy this workflow.

Prefer native semantics and accessible component behavior: associated labels, appropriate field grouping, keyboard operation, visible focus, named overlays, meaningful status announcements, and robust loading/error/empty states where applicable.

For an installed component library, follow its verified version and local API. FieldGroup, data-icon, spacing utilities, and overlay stacking conventions are library-specific recipes, not universal accessibility requirements. Avoid arbitrary stacking fixes; diagnose the actual layering problem. A div or a particular CSS sizing class is not by itself a defect.

Primitives support accessibility but do not prove the assembled interface is accessible. A radiogroup role alone does not implement selection or keyboard behavior; prefer native radio inputs when suitable.

## Stage 4: Static review

Review the implementation against project criteria and relevant current primary guidance. Use a specialized auditor only when available and authorized; otherwise perform the review directly. Do not claim a fixed number of rules was checked without identifying the checklist used.

Check task coverage, disclosure discoverability, approved identity, copy, semantic structure, keyboard/focus behavior, form validation, target sizing, contrast, zoom, reduced motion, and the operation's authorization and result states. Distinguish requirements from preferences and document applicable exceptions. Use the project's accessibility target; if unspecified, propose WCAG 2.2 AA as the baseline and record it as proposed until agreed. APCA measurements do not establish WCAG 2 conformance.

Report concrete findings with file/line and impact when reviewing code. A static check cannot prove runtime behavior, user comprehension, full accessibility conformance, or production readiness.

## Stage 5: Browser verification

Inspect the actual interface in an available supported browser. Report browser, build/version or file hashes, environment, viewport sizes, exercised paths, outcomes, and limitations. For responsive web work, start with 320, 768, 1024, and 1440 CSS pixels, adapting coverage to the agreed deployment context.

- Check layout and content access, including long strings and zoom/reflow. A scrollWidth comparison is a useful signal, not sufficient evidence. Do not use overflow-x: hidden to conceal inaccessible content; horizontally scrollable data regions may be intentional.
- Exercise the primary task and relevant loading, empty, validation, failure, retry/cancel, limited-result, and uncertain-effect paths. Use synthetic data where suitable; external effects require applicable authorization.
- Test keyboard navigation and visible focus. For modal dialogs, check naming, focus management, Escape where appropriate, and focus return. Inline details disclosures do not inherit modal focus-trap or Escape requirements.
- Measure contrast for relevant text, controls, and states against the agreed criteria; visual inspection alone is insufficient. Test reduced motion. Test themes that exist or are explicitly in scope; do not introduce a theme toggle to pass verification.
- Verify actual results through the operation's trusted output, not just a toast or screenshot. Return operational failures to the contract owner.

If browser tooling is unavailable, identify unverified criteria and deliver a bounded documentary/static result. Do not mark browser verification complete.

## Completion and handoff

Report each criterion as passed, failed, not run, blocked, or not applicable, with evidence and reasons. Keep checklists unchecked until verified. UI verification covers the exercised interface and paths; product readiness also depends on operational, security, deployment, and other project requirements.

Return findings to the appropriate owner without restarting completed stages. Preserve approvals within scope; a brand change, new operation, permission change, deployment, or installation requires the applicable authorization. Do not install or publish a skill as a side effect of applying it.
