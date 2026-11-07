# OpenSpec workflow

This repository uses the `html-design` bundle from
[Mission Control](https://github.com/moonrockz/mission-control/tree/main/apps/tools).
New changes produce a proposal, capability specs, a standalone `design.html`
with inline CSS and SVG, and implementation tasks. Existing changes retain their
recorded schema. Follow this repository's contribution and approval rules.

## Bootstrap

Install [mise](https://mise.jdx.dev/), then run `mise install`. OpenSpec is pinned
to 1.14.3. The `mission-control-tools` 0.1.0 binary checks and sets up the
shared workflow. mise installs it from the `tools-v0.1.0` release of
[Mission Control](https://github.com/moonrockz/mission-control/releases/tag/tools-v0.1.0)
and checks each download against its GitHub asset digest and artifact
attestation. Windows on Arm runs the x64 build under emulation. The binary does
not change the project's implementation language, and this repository needs no
other toolchain for the OpenSpec workflow.

Verify the checked-in bundle:

```sh
mise run openspec:verify
```

This runs the bundle check (`mission-control-tools openspec check --bundle`)
and the schema and change validation. An empty spec/change tree reports no items
to validate. CI runs the same checks.

## Propose and implement a change

```sh
mise exec -- openspec new change <change-name>
mise exec -- openspec instructions design --change <change-name>
```

No schema override is needed. The design instructions target `design.html`.
Use the generated core skills to propose, explore, apply, update, sync specs and
archive changes. Skills are checked in for portable/Codex agents, Claude,
Copilot, Cursor, Grok, Gemini and OpenCode. `mise run openspec:setup` regenerates
them using an isolated core profile without changing personal OpenSpec settings.

Keep project-specific context and rules in `openspec/config.yaml` and AGENTS.md.
Existing skills outside the generated OpenSpec set are preserved.

## Update the shared bundle

`openspec/extensions.lock.json` records the tool and version that wrote it
(`moonrockz/mission-control-tools` 0.1.0) and SHA-256 hashes for seven managed
files. Git attributes preserve LF line endings so Windows checkouts keep those
hashes. Keep the schema, templates and notices identical to Mission Control. Do
not patch them locally. `mission-control-tools openspec check --bundle` checks
that each managed file matches the lock and the files in the pinned binary.

To update the bundle, change the `github:moonrockz/mission-control` version in
`mise.toml`, then run:

```sh
mise install
mise exec -- mission-control-tools openspec install
```

Review the diff, then run `mise run openspec:verify`. The installer refuses
edits to owned files before it writes anything. It writes the lock last. A
version change without `install` makes the bundle check fail.

The schema's Apache-2.0 license and upstream OpenSpec MIT notice are retained in
`openspec/schemas/html-design/LICENSE` and `NOTICE`.
