# BOOTSTRAP-INSTRUCTIONS.md — Claude-executable runbook

**Read by:** Claude, when the user pastes the URL of this repository into a Claude session.

**NOT read by:** the human user. The human reads `README.md`, which tells them to paste the URL into Claude. Claude then fetches this file via WebFetch and follows the runbook.

## Scope

This runbook orchestrates **Stage 0 → Stage 4** of the 4-stage zero-state thinking-living bootstrap (per [`bootstrap-playbook.md`](https://github.com/henrikpz/thinking-living/blob/main/ideas/network-of-thinking-livings/bootstrap-playbook.md) in the upstream design repo). The user has gone through Stage 0 already (someone gave them this URL); this file picks up at Stage 1 and routes them through to Stage 4 where they're live in their own `thinking-living`.

## Stage hand-off via observable system state (Q2a)

The user pastes this URL into Claude every time they want to make progress on the bootstrap. Each invocation: probe what's already done; resume at the first phase that isn't done yet.

```
Probe sequence (run in order; first ✗ determines the resume point):

1. Are we in claude.ai web or Claude Code Desktop?
   - claude.ai web (no filesystem access via Bash) → Stage 1
   - Claude Code Desktop (has Bash tool with `which`, etc.) → continue to step 2

2. `which gh` (or check whether the Bash tool can run gh commands)
   - gh missing → Stage 2 Phase A (toolchain install — see template's bootstrap-mac.md / bootstrap-windows.md)
   - gh present → continue

3. `gh auth status`
   - not authed → Stage 2 Phase B (GitHub auth)
   - authed → continue

4. `gh repo view henrikpz/thinking-living-template --json name`
   - access denied → Stage 2 Phase C (template-access request)
   - access granted → continue

5. `gh repo view <user>/thinking-living --json name`
   - doesn't exist → Stage 3 (fetch template's BOOTSTRAP.md and execute Phases D-J)
   - exists → continue

6. `test -d ~/Develop/thinking-living/.git`
   - missing → Stage 3 Phase F (local checkout)
   - present → continue

7. `cd ~/Develop/thinking-living && grep -cE '\{\{[a-zA-Z][a-zA-Z0-9_-]*\}\}' CLAUDE.md`
   - count > 0 → Stage 3 Phase G (CLAUDE.md user-config Q&A still has placeholders)
   - count == 0 → Stage 4 (live)
```

## Stage 1 — claude.ai web (the user's first Claude session ever)

Triggered when the user is on claude.ai web (no Bash filesystem access) and pastes the URL.

Walk the user through:

**S1.1 — Confirm Claude Pro plan.**

Claude (web) says (paraphrase):

> *"You're on Claude.ai. Quick check: are you on the Pro plan? Claude Code Desktop — the app we'll install in a moment — needs Pro tier or higher. If you're still on Free, upgrade to Pro at [claude.ai/settings/plans](https://claude.ai/settings/plans). It costs a small monthly fee. Tell me when you've confirmed Pro is active."*

Wait for confirmation.

**S1.2 — Install Claude Code Desktop.**

Claude says (paraphrase):

> *"Now install Claude Code Desktop. It's the Claude app for your computer — the one that can read and write files locally and run terminal commands. Download it from [claude.com/code](https://claude.com/code) and install it like any other app. Sign in with the same account you used on claude.ai. Tell me when it's installed and you've signed in."*

Wait for confirmation.

**S1.3 — Hand off to Claude Code Desktop.**

Claude says (paraphrase):

> *"Open Claude Code Desktop and start a fresh conversation. Paste the same URL into it: `https://github.com/henrikpz/thinking-living-start-here`. The Claude there can do things this web Claude can't (read your computer's files, run installers, talk to GitHub) — it'll figure out from your computer's state where to pick up."*

End of Stage 1 from web Claude's side. The user moves to Claude Code Desktop. The next paste of this URL there triggers Stage 2.

## Stage 2 — Claude Code Desktop (zero-state user)

Triggered when the user is in Claude Code Desktop (Bash tool available) AND step 2 of the probe shows toolchain-or-auth is incomplete.

Phase A through Phase C of the bootstrap. The platform-specific commands are in:

- **Mac:** clone `henrikpz/thinking-living-template`'s `.claude/bootstrap/bootstrap-mac.md` and follow it. Or for now, since the user's Claude doesn't yet have template access, fetch it via raw URL: `https://raw.githubusercontent.com/henrikpz/thinking-living-template/main/.claude/bootstrap/bootstrap-mac.md`. **Wait — this only works if `-template` is public OR the user has been added as a collaborator.** Since `-template` is private (per the design), and the user doesn't have access yet (that's what Phase C is requesting), fetching the runbook by URL won't work in v0.1.

  **Workaround for v0.1:** Claude reads the relevant phases of the runbook *from this file's continuation* (see "Stage 2 inline runbook" below). The full Mac runbook in `henrikpz/thinking-living-template/.claude/bootstrap/bootstrap-mac.md` is the source of truth; this file mirrors the v0.1-essential subset for Phases A-C, since they need to run before the user has template access.

- **Windows:** *(not yet authored — bootstrap-windows.md is a v0.X follow-up. Don't proceed on Windows until that file lands.)*

### Stage 2 inline runbook (Mac)

#### Phase A — Toolchain prerequisites

Probe: `which brew gh git python3 jq` (each); install missing tools via `brew install <tool>`. Install Homebrew first if absent (`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`). Set up PATH for Apple Silicon (`/opt/homebrew/bin`) or Intel (`/usr/local/bin`).

Verify all 5 tools (`brew gh git python3 jq`) report a version.

#### Phase B — GitHub account + 2FA + SSH key

Probe: `gh auth status`. If not authed:

1. **Account.** If user has no GitHub account, `open https://github.com/signup` and walk them through signup (~2 min). Wait for confirmation.
2. **2FA.** `open https://github.com/settings/security`. Walk through TOTP setup with an authenticator app (1Password / Google Authenticator / Authy). Save recovery codes safely.
3. **SSH key.** Generate `ssh-keygen -t ed25519 -C "<user-email>" -f ~/.ssh/id_ed25519 -N ""`. Add to ssh-agent (`ssh-add --apple-use-keychain ~/.ssh/id_ed25519`).
4. **Add to GitHub.** Try `gh ssh-key add ~/.ssh/id_ed25519.pub --title "Mac ($(hostname -s))"`; if that fails (gh not authed yet), `pbcopy < ~/.ssh/id_ed25519.pub && open https://github.com/settings/ssh/new` and walk user through pasting.
5. **Login.** `gh auth login --hostname github.com --git-protocol ssh --web`.

Verify: `gh auth status` reports logged in; `ssh -T git@github.com` returns `Hi <user>!`. Capture `<user>` via `gh api user --jq .login` for later phases.

#### Phase C — Template access request

Probe: `gh repo view henrikpz/thinking-living-template --json name`. If denied:

1. `open https://github.com/henrikpz/thinking-living-template`
2. The user sees GitHub's "404 / no access" page with a "Request access" button. Walk them through clicking it.
3. Tell user: *"Henrik will get an email to approve. When he does (could be minutes or hours), paste this start-here URL again in Claude Code Desktop and I'll figure out from your system state where to pick up."*

**Stop here** until the user resumes after access is granted.

When the user returns and pastes the URL again, the probe sequence runs from the top; if step 4 now passes, we proceed to Stage 3.

## Stage 3 — Claude Code Desktop, with template access

Triggered when the probe sequence shows `gh auth ✓` + `template access ✓` + `<user>/thinking-living doesn't exist yet`.

At this point, fetch the template's BOOTSTRAP.md and execute Phases D-J:

```bash
gh repo clone henrikpz/thinking-living-template /tmp/thinking-living-template-temp 2>/dev/null
cat /tmp/thinking-living-template-temp/BOOTSTRAP.md
# Then read /tmp/thinking-living-template-temp/.claude/bootstrap/bootstrap-mac.md
# for the concrete Phase D-J commands
```

**Or simpler:** since the user now has template access via gh, just fetch via raw GitHub URLs:

- `https://raw.githubusercontent.com/henrikpz/thinking-living-template/main/BOOTSTRAP.md`
- `https://raw.githubusercontent.com/henrikpz/thinking-living-template/main/.claude/bootstrap/bootstrap-mac.md`
- `https://raw.githubusercontent.com/henrikpz/thinking-living-template/main/.claude/bootstrap/bootstrap-mac-check.sh`

Read those, execute Phases D-J. The phases summary:

- **D** — `gh repo create <user>/thinking-living --template henrikpz/thinking-living-template --private`
- **E** — `gh project create --owner @me --title "thinking-living"`, discover field IDs via `gh project field-list` + `gh api graphql`
- **F** — `mkdir -p ~/Develop && cd ~/Develop && gh repo clone <user>/thinking-living`
- **G** — interactive Q&A to fill `CLAUDE.md` user-config (one question at a time per F9 empty-his-head-first; use `{{double-curly}}` placeholder probe)
- **I** — `git add CLAUDE.md && git commit -m "config: bootstrap user-config" && git push origin main`
- **J** — render `.claude/features.md` directly (the `/features` skill isn't in v0.1) so user sees the substrate dashboard

After Phase J, the user is in **Stage 4** — live thinking-living. Welcome them; hand off to operating-as-thinking-partner mode.

## Stage 4 — live

User has a working setup. Future sessions read `CLAUDE.md` from their own `<user>/thinking-living` repo and operate as their thinking partner.

This file (`BOOTSTRAP-INSTRUCTIONS.md`) is no longer the entry point — they just talk to Claude in their own repo. The next time they paste the start-here URL is for re-bootstrap (new machine) or out of curiosity.

## Re-bootstrap (recovery)

If the user re-pastes the URL on a different machine or after a wipe, the probe sequence sees:

- `gh auth ✓` + `template access ✓` + `<user>/thinking-living exists` + `~/Develop/thinking-living missing`

→ Resume at Phase F (local checkout). They're not creating their thinking-living again; they're re-cloning their existing one to the new machine.

The `gh repo clone <user>/thinking-living ~/Develop/thinking-living` plus a quick re-read of CLAUDE.md gets them back to Stage 4.

## Convention notes

- Quote-blocks (`> ...`) in this file are **templated user-facing lines** Claude paraphrases, not recites verbatim.
- Idempotency is mandatory at every step. The user may paste the URL many times across the bootstrap (re-opening Claude Code, switching machines, returning after Henrik approves access). Each paste re-runs the probe and resumes correctly.
- Failure handling: surface verbatim, don't bypass safety checks (no `--no-verify`-style flags). If a phase fails, stop and explain to the user; don't paper over.
- Claude operates the user's machine on their behalf, with their consent at each significant step. Privacy-by-narration applies (per F3): explain in plain language what's about to happen before acting on the user's machine or sending content outward.

## What this file references

- `henrikpz/thinking-living-template` — the rock-solid scaffolding (Stage 3 source of truth via `BOOTSTRAP.md` and `.claude/bootstrap/bootstrap-mac.md`)
- `henrikpz/thinking-living-incoming` — contributor staging (not part of the bootstrap; mentioned only for users who want to contribute back later)

## Version

| Date | Version | Notes |
|---|---|---|
| 2026-05-04 | v0.1 | First authoring. Mirrors the design in upstream `thinking-living/ideas/network-of-thinking-livings/bootstrap-playbook.md`. Stage 2 inline runbook covers Phases A-C since the user lacks template access at that point; Stage 3 fetches the full runbook from the now-accessible template repo. |
