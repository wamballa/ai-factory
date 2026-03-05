# AI Factory TODO

## Backlog
- [ ] Define minimal agent contract (`input`, `output`, `side effects`, `failure mode`) in docs
- [ ] Add initial `research-agent` scaffold under `projects/`
- [ ] Add initial `builder-agent` scaffold under `projects/`
- [ ] Create a single wrapper script for non-interactive Codex execution (used by n8n and manual runs)
- [ ] Standardize run metadata (`run_id`, `agent`, `task`, `exit_code`, `timestamps`, `artifacts`)
- [ ] Add idempotency key handling pattern for n8n-triggered runs
- [ ] Add lightweight entry template for `memory/` files (timestamp, agent, type, summary)
- [ ] Define append-only rules and a weekly compaction routine into `memory/knowledge.md`
- [ ] Start a `memory/index.md` with links to high-value decisions and knowledge
- [ ] Version control core n8n workflow JSON exports in repo
- [ ] Add failure path in n8n workflow (capture error + write to `memory/inbox.md`)
- [ ] Add one health-check workflow to validate SSH + Codex command execution
- [ ] Split setup guidance into `install`, `operations`, and `troubleshooting`
- [ ] Document the end-to-end run path: trigger -> n8n -> SSH -> Codex -> memory update
- [ ] Add a short architecture decision log for prototype constraints and tradeoffs

## In Progress
- (none)

## Completed
- [x] Verify all setup commands work on Ubuntu 22.04
- [x] Add section explaining Codex CLI authentication
- [x] Document correct n8n -> Codex command
- [x] Add troubleshooting section
- [x] Add diagram of system architecture
- [x] Add example n8n workflow
- [x] Document monorepo GitHub SSH push flow and `publickey` fix
- Updated `setup.md` with Ubuntu 22.04-oriented install flow (Node.js 20 LTS + Codex CLI)
- Added architecture diagram, authentication steps, n8n -> Codex command pattern, troubleshooting, and workflow example
- Updated `setup.md` to use `~/ai-factory` monorepo paths and added GitHub SSH key/push troubleshooting steps
