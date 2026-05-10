# meta-goal

Compile rough long-running intentions into paste-ready Codex CLI `/goal` commands.

`meta-goal` is a small Codex skill that turns fuzzy objectives into measurable completion contracts for the official experimental `/goal` command. It helps you specify what Codex should achieve, how it should prove progress, when it should stop, and where it should ask before widening scope.

## Install

Ask Codex to install this skill:

```text
$skill-installer install https://github.com/jaimerp89/codex-meta-goal-skill/tree/main/meta-goal
```

Or install manually by copying the `meta-goal` folder into:

```text
~/.codex/skills/meta-goal
```

Restart Codex after installation so the skill is picked up.

## Use

Invoke the skill explicitly:

```text
$meta-goal finish the migration and keep tests green
```

It returns one paste-ready command:

```text
/goal Finish the active migration in this repository. Done when migration-related code paths are updated, all relevant tests and build checks pass locally or documented blockers are proven, and the final report includes changed files, exact verification commands, and remaining risks. Stop and ask before widening scope beyond the migration or making destructive data changes.
```

## Why

The official `/goal` command works best when it has a clear durable objective, verification evidence, and a stopping condition. This skill gives you a repeatable way to draft that contract before you start a long-running Codex session.

## Security

This is a prompt-only Codex skill. It contains no scripts, binaries, MCP servers, shell commands, network calls, or credential handling.

The skill is designed to output text for the official `/goal` command, not to execute the goal or update your active thread directly. It also includes safety rules for secrets, destructive operations, exfiltration, production changes, and privileged actions.
