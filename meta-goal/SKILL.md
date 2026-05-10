---
name: meta-goal
description: Compile a user's rough long-running objective into a high-quality Codex CLI `/goal` command. Use only when the user explicitly invokes $meta-goal, asks to draft/prepare/design/compile a goal for Codex CLI, or wants a paste-ready measurable objective for the official `/goal` command. Do not use to create or update the current thread's goal directly, and do not use for ordinary task planning.
---

# Meta Goal

## Purpose

Turn a rough human intention into one paste-ready Codex CLI `/goal <objective>` command. This skill is a compiler for the official `/goal` command: design the goal text, but do not call goal-management tools and do not modify the active thread goal.

The output must help `/goal` do its real job: keep a long-running Codex thread oriented toward a durable completion contract.

## Workflow

1. Extract the intended outcome, scope, constraints, verification evidence, and stopping conditions from the user's request.
2. If the request is underspecified, make conservative assumptions and include them in the objective when possible. Ask one concise question only when the missing detail would make the goal unsafe or misleading.
3. Classify the desired closure criterion and use the matching blueprint below:
   - `Artifact`: a file, report, PR, export, migration, dashboard, issue set, or script exists.
   - `Behavior`: a feature, test path, bug fix, workflow, deployment, or user-visible interaction works.
   - `Evidence`: an audit, benchmark, validation, review, reproduction, or investigation proves a state.
   - `Decision`: a recommendation is made from cited evidence, options, tradeoffs, and constraints.
4. Produce one primary `/goal` command in a fenced `text` block.
5. Keep the objective concrete, measurable, and durable across a long-running Codex session.
6. Make the objective a completion contract, not a step-by-step plan.
7. Include verification in the goal: tests, lint, build, screenshots, docs, artifacts, metrics, audits, citations, or explicit evidence in the final report.
8. Include a stop condition for risky expansion: ask before unrelated refactors, destructive operations, production changes, credential/security changes, schema/data migrations, or scope changes.
9. Match the user's language unless they ask otherwise.

## Goal Shape

Use this structure by default:

```text
/goal <strong verb> <outcome> for <scope>. Done when <specific completion criterion>, <verification evidence>, and the final report includes <proof>. Stop and ask before <risky expansion or unclear decision>.
```

Use natural verbs such as `Produce`, `Fix`, `Verify`, `Decide`, `Migrate`, `Audit`, `Ship`, or `Diagnose`. Avoid forcing every objective into `Achieve`.

Prefer:

- One objective, not multiple parallel projects.
- Observable completion criteria over vague quality words.
- Repository, module, file, dataset, branch, account, product, or environment scope when known.
- Verification commands, artifact paths, metric thresholds, screenshots, citations, row counts, schemas, or evidence types when known.
- "Done when either..." when the user asks for "try X, otherwise prove why not."
- "Stop and ask before..." for boundary control.
- "If blocked..." language when the useful outcome is a diagnosis or proof rather than a code change.

Avoid:

- Creating the goal directly with tools.
- Changing this skill's invocation policy.
- Naming this skill as `/goal`, `/goals`, or anything that can be confused with the official command.
- Adding token budgets unless the user explicitly asks for a budgeted goal and the current environment supports it.
- Writing long plans, milestone trees, or implementation details inside the goal.
- Promising unattended future work; suggest an automation separately when the user needs scheduling or wake-ups.
- Using soft endings such as "improve X" without saying how completion will be recognized.
- Turning a decision goal into implementation unless the user explicitly asks for both.

## Closure Blueprints

### Artifact

An artifact goal is complete only when the named output exists and its quality can be checked.

Include:

- Artifact type and path, destination, branch, PR, export name, or issue tracker target when known.
- Source inputs and any assumed scope.
- Validation such as schema checks, row counts, rendering, lint/build, test commands, or reviewer-ready acceptance criteria.
- Final proof: artifact path or link, changed files when relevant, source assumptions, validation command output, and known gaps.

Template:

```text
/goal Produce <artifact> for <scope>. Done when <artifact path or target> exists with <required content/format>, <validation evidence> passes or documented blockers are proven, and the final report includes <path/link>, <source assumptions>, <validation>, and <remaining gaps>. Stop and ask before <scope/data/production changes>.
```

### Behavior

A behavior goal is complete only when the requested workflow works or the blocker is proven.

Include:

- The user-visible behavior, failing path, environment, and affected code area when known.
- Regression coverage: tests, smoke checks, screenshots, logs, build, deploy verification, or exact reproduction evidence.
- Fallback closure: if the behavior depends on external data or credentials, prove the blocker instead of claiming success.
- Final proof: before/after evidence, changed files, commands run, screenshots or logs, deployment status when relevant, and residual risk.

Template:

```text
/goal Fix <behavior> in <scope/environment>. Done when <workflow> works in <target path> or the external blocker is proven, relevant tests/build/smoke checks pass, and the final report includes changed files, before/after evidence, exact verification commands, and remaining risks. Stop and ask before <unrelated refactors/production/security/data changes>.
```

### Evidence

An evidence goal is complete only when the investigation answers the question against explicit evidence.

Include:

- The claim, system, report, commit, incident, benchmark, or dataset being checked.
- A requirement checklist when the user asks "is this really done?"
- Evidence sources: git state, tests, logs, docs, artifacts, metrics, database queries, screenshots, citations, or reproduced failures.
- Final proof: pass/fail or conclusion per requirement, command outputs or references, confidence level, and unresolved unknowns.

Template:

```text
/goal Verify <claim/question> for <scope>. Done when <evidence sources> are inspected against <checklist/criteria>, the conclusion is stated with pass/fail or quantified findings, and the final report includes commands, file/artifact references, evidence gaps, and remaining risks. Stop and ask before changing code, data, production state, or widening the investigation.
```

### Decision

A decision goal is complete only when the recommendation is justified enough for the user to choose a direction.

Include:

- Options to compare and decision criteria such as cost, latency, risk, maintainability, compliance, migration effort, or current official documentation.
- Evidence source expectations: repo inspection, benchmarks, vendor docs, pricing, changelog, issue context, or stakeholder constraints.
- Final proof: recommendation, rejected alternatives, tradeoff matrix or rationale, assumptions, and next action.
- Boundary: do not implement the recommendation unless the user asked for implementation too.

Template:

```text
/goal Decide <question> for <scope>. Done when <options> are compared against <criteria> using <evidence sources>, a recommendation is made with rejected alternatives and assumptions, and the final report includes the decision rationale, evidence links or file references, and next action. Stop and ask before implementing the recommendation or committing to irreversible/vendor/security-sensitive changes.
```

## Rough Prompt Handling

- `make/create/export/write`: usually `Artifact`; require output location, format, validation, and final path/link.
- `fix/ship/make it work/deploy`: usually `Behavior`; require a working path plus regression evidence.
- `check/audit/benchmark/prove/does this really`: usually `Evidence`; require a checklist and cited proof.
- `choose/should we/which is best/decide`: usually `Decision`; require options, criteria, evidence, and a no-implementation boundary.
- `try X; if not, explain why`: use an either/or completion criterion so the goal can close honestly on proven blockage.
- `next goal`: compile a paste-ready command only if the user asks for a goal draft; do not start or update the current active goal.

## Quality Checklist

Before returning the command, mentally check:

- Can Codex know when to stop?
- Can Codex prove completion in the final answer?
- Is the scope bounded enough to avoid wandering?
- Does the goal preserve useful autonomy without hiding risky choices?
- Does the stop boundary cover the main risk in the user's request?
- Would `/goal pause`, `/goal resume`, and `/goal clear` still make sense for this objective?
- If no gold-standard success is possible, does the goal define acceptable evidence of blockage?

## Output Format

Return:

1. A paste-ready command:

```text
/goal <objective>
```

2. Optional short notes only when helpful:
   - `Assumptions:` if important details were inferred.
   - `Enablement:` if the user asks how to enable CLI goals, mention that `/goal` is experimental and requires `features.goals = true` or `/experimental`.
   - `Automation:` if the objective requires Codex to wake up later, say that an automation/heartbeat is needed in addition to the goal.
   - `Why this shape:` if the user asks for rationale, explain the completion criterion, verification, and stop boundary.

Do not output multiple competing commands unless the user asks for options.

## Examples

Artifact rough request:

```text
turn this customer-research dump into a PRD and tickets
```

Output:

```text
/goal Produce a PRD and implementation-ready ticket breakdown from the current customer-research dump. Done when the PRD and ticket draft exist at agreed project locations with assumptions and open questions called out, any available formatting or lint checks pass, and the final report includes artifact paths, source inputs used, validation performed, and remaining gaps. Stop and ask before publishing tickets, changing product scope, or inventing requirements not supported by the source material.
```

Artifact rough request:

```text
export all customers missing tax IDs into a clean CSV
```

Output:

```text
/goal Produce a validated CSV export of customers missing tax IDs from the current dataset. Done when the CSV exists at the agreed output path with stable columns, row count and filter criteria are verified against the source data, and the final report includes the export path, validation command or query, assumptions, and data-quality caveats. Stop and ask before modifying source data, sending the export externally, or broadening the filter criteria.
```

Behavior rough request:

```text
finish migration and keep tests green
```

Output:

```text
/goal Finish the active migration in this repository. Done when migration-related code paths are updated, all relevant tests and build checks pass locally or documented blockers are proven, and the final report includes changed files, exact verification commands, and remaining risks. Stop and ask before widening scope beyond the migration or making destructive data changes.
```

Behavior rough request:

```text
the dashboard is empty this week, fix it but only deploy if verified
```

Output:

```text
/goal Restore accurate current-week data display in the dashboard. Done when the root cause is fixed or an upstream data blocker is proven, relevant tests/build/smoke checks pass, dashboard evidence confirms the current-week state, and the final report includes changed files, before/after evidence, exact verification commands, and deploy status. Stop and ask before publishing without verification, changing dashboard data semantics, or touching unrelated views.
```

Evidence rough request:

```text
prove whether Claude really finished the goal it claimed was done
```

Output:

```text
/goal Verify whether the reported Claude completion satisfies the stated goal. Done when git state, tests, docs, artifacts, dashboard or deployment evidence, and any named outputs are inspected against a requirement checklist; the conclusion is stated per requirement as pass, fail, or unverified; and the final report includes commands run, file/artifact references, evidence gaps, and remaining risks. Stop and ask before changing code, deploying, or widening the audit beyond the stated goal.
```

Evidence rough request:

```text
promote gold observations if possible; if not, show exactly where the evidence funnel breaks
```

Output:

```text
/goal Advance the evidence funnel toward new promoted gold observations in the current repository. Done when either at least one valid new gold observation is promoted with full supporting evidence, or the highest-yield funnel blocker is proven with updated audit/export evidence; required verification passes and the final report includes before/after metrics, artifact paths, changed files, and the exact criterion used to close the goal. Stop and ask before weakening QA guards, fabricating evidence, changing unrelated infrastructure, or making destructive data changes.
```

Decision rough request:

```text
should we keep Postgres or move this prototype to D1?
```

Output:

```text
/goal Decide whether this prototype should stay on Postgres or move to D1. Done when both options are compared against current project requirements, migration effort, operational risk, local development needs, cost, and relevant documentation; a recommendation is made with rejected alternatives and assumptions; and the final report includes the decision rationale, evidence links or file references, and next action. Stop and ask before implementing the migration, changing production data, or committing to vendor-specific architecture.
```

Decision rough request:

```text
which OpenAI model should we upgrade the support bot to?
```

Output:

```text
/goal Decide which OpenAI model the support bot should upgrade to. Done when current official model documentation, support-bot requirements, quality constraints, latency, cost, tooling compatibility, and rollout risk are compared; a recommendation is made with rejected alternatives and assumptions; and the final report includes evidence links, decision rationale, and a safe rollout next step. Stop and ask before changing production configuration, increasing spend materially, or deploying the recommendation.
```
