# Agent guidance

## OpenSpec

New changes use the shared `html-design` schema and a standalone `design.html`
with inline CSS and SVG. Use the generated OpenSpec skills for proposals,
exploration, implementation, updates, spec sync and archiving. Repository
tracking, contribution and approval rules still apply.

Keep project rules in `openspec/config.yaml`. Do not edit the managed schema,
templates or checker. The ownership lock is `openspec/extensions.lock.json`;
run `mise run openspec:verify` before submitting changes. See
[the OpenSpec guide](docs/openspec.md) for bootstrap and shared bundle updates.
