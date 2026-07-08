# AGENTS.md — wikis (repo root)

This repo is a collection of **hand-curated Obsidian markdown wikis** (`finance_wiki`,
`autoencoder_wiki`, `ml-hardware_wiki`, `optimal_transport_wiki`). Each wiki has its own
`AGENTS.md` and vault; per-wiki rules and the note-writing contract
(`docs/00-system/vault-contract.md`) take precedence for content edits. Shared authoring rules
and skills live in `.cursor/`.

## Cursor Cloud specific instructions

- **There is no build/test/lint pipeline and no package manifests.** This is markdown only —
  as `autoencoder_wiki/docs/obsidian_setup.md` puts it, "No build step. The `[[wikilinks]]` in
  your notes *are* the graph." Nothing to `npm install` / `pip install`; the startup update
  script is intentionally a no-op.
- **The "application" is Obsidian + the Dataview plugin.** Obsidian (v1.12.7) is pre-installed
  in the VM snapshot at `/opt/Obsidian/obsidian` (installed once during env setup; not in the
  update script since it is a system GUI dependency). Launch it headfully on the desktop:
  `DISPLAY=:1 /opt/Obsidian/obsidian --no-sandbox --disable-gpu &` (the `--no-sandbox` flag is
  required in this container). Then drive/inspect it via the `computerUse` agent.
- **Vault roots differ per wiki:** open the folder that holds `00-system/`, not the repo root —
  `autoencoder_wiki/docs/`, `ml-hardware_wiki/ml-hardware-wiki/`, `optimal_transport_wiki/docs/`,
  and `finance_wiki/Finance-Wiki/`. Choose which vault to open by writing
  `~/.config/obsidian/obsidian.json` (`{"vaults": {"<id>": {"path": "<abs vault path>", "open": true}}}`)
  before launch. The Dataview community plugin is already enabled per-vault via committed
  `community-plugins.json`, so MOC tables render without extra setup.
- **Gotcha — Obsidian mutates the vault on open.** It regenerates a `.obsidian/` config dir and
  can drop stray files (e.g. an `Untitled.base`) into the vault root. These are not part of any
  content change — do **not** commit them; `git checkout`/`rm` them before staging.
- **Headless integrity check.** To validate wikilinks/contract without launching the GUI, a
  small throwaway script that regex-scans `[[links]]` across a vault is enough (resolve targets
  against note filename stems; concepts need ≥2 linked source notes). No such tool ships in the
  repo — keep it out of the repo unless asked.
- **Committing:** per-wiki `AGENTS.md` says "never commit/push unless asked" for interactive use.
  Cloud-agent tasks that were explicitly asked to make a change do commit and open a PR; keep the
  diff limited to the intended content notes.
