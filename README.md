# thinking-living — start here

**Welcome.** Someone you know shared this link with you because they thought you'd benefit from setting up a *thinking-living* of your own.

A thinking-living is a private personal knowledge base — a folder of Markdown files about who you are, who's in your life, and what you're working on — that **Claude reads, edits, and remembers across every conversation**. Each chat builds on the last. Claude drafts your messages in your voice. Suggests things based on what it knows about you. Helps you keep track of the shape of your life without you having to manage anything by hand.

**You don't need to be technical.** The whole setup is driven by Claude. You sit there, answer Claude's questions, and at the end you have a working personal knowledge base.

> **Total time: ~30–60 minutes.** Most of it is waiting for two installations to finish.

---

## What you'll have when this is done

- **A private GitHub repository** under your own account, called `thinking-living`. It contains Markdown files about you. Only you can see it.
- **Claude Code Desktop** installed on your computer, with permission to read and write that repository.
- **A Kanban board** on GitHub for tracking todos.
- **A structured starting point** — empty folders for `identity/`, `relationships/`, `life-spheres/`, `events/`, etc. — that you fill in over time, mostly by talking to Claude rather than typing into files yourself.

---

## Before you start — what you'll need

- [ ] A computer (Mac is fully supported; Windows is in progress)
- [ ] An email address you'll use for your Claude account
- [ ] An email address you'll use for your GitHub account *(can be the same as your Claude one)*
- [ ] About 30–60 minutes of uninterrupted time
- [ ] Willingness to enter your password / approve a couple of system dialogs when prompted (your computer will ask permission to install software)

You do **not** need: any prior coding experience, Homebrew, git, or any developer tools. Claude installs everything for you.

---

## What to do, right now — three steps

### Step 1 — Create a Claude.ai account on the Pro plan

- [ ] Open **[claude.ai](https://claude.ai)** in your browser.
- [ ] Sign up (or log in if you already have an account).
- [ ] Make sure you're on the **Pro plan**. The Free plan won't work for what comes next — it doesn't include Claude Code Desktop. Check / upgrade at [claude.ai/settings/plans](https://claude.ai/settings/plans).

> **Why Pro?** The next steps need a version of Claude that can install software and read files on your computer (Claude Code Desktop). That feature is Pro-only. The cost is around 200 DKK / 20 USD per month.

### Step 2 — Paste this URL into a fresh Claude conversation

- [ ] In Claude.ai, start a **new conversation** (any blank chat).
- [ ] Copy this URL:

  ```
  https://github.com/henrikpz/thinking-living-start-here
  ```

- [ ] Paste it into the chat box, **send**, and wait.

That's it. Claude will read this repository, figure out what you need to do next, and tell you in plain language. You don't need to read any documentation or remember commands. Claude does that part.

### Step 3 — Answer Claude's questions as they come

Claude will guide you through:

1. **Installing Claude Code Desktop** — a separate app on your Mac (or PC). Claude tells you where to download it from and walks you through signing in.
2. **Opening Claude Code Desktop and pasting the same URL there.** The Claude in the desktop app can do things browser-Claude can't (read your files, install software, talk to GitHub).
3. **Setting up GitHub** if you don't already have an account. Claude walks you through signup, two-factor auth, and the SSH-key thing — with no jargon required from you. Just click "yes" when Claude tells you to.
4. **Asking the person who shared this URL** to grant you access to the template that becomes your `thinking-living`. They'll get an email; they approve. You wait a few minutes.
5. **A quick personalisation Q&A** — your name, your email, your phone, your preferred sign-off style, etc. Claude asks one question at a time. You type the answer. Claude writes it into the right place.
6. **You're done.** Claude shows you what you have and you can start using it.

That's the whole thing. The complexity is hidden inside Claude's instructions — you just need to keep saying "yes" and answering questions.

---

## What is thinking-living, really?

It's a way of thinking *with* Claude that goes beyond a single conversation. Most people interact with Claude as if every conversation is its own island — they re-explain themselves every time. **thinking-living changes that.**

The Markdown files in the repository become Claude's persistent context: who you are, who's in your life, what you're working on, how you communicate. Each conversation builds on the last. Claude can:

- Draft messages in your voice (knowing your sign-off, language preference, recipient styles)
- Remember decisions you've made and why
- Surface things from weeks ago that are relevant now
- Help you think through life decisions with the same context across sessions
- Keep a structured record of your life that you can edit yourself anytime

It's not a product. It's a **personal practice**. It works because the structure is yours — your repository, your data, on your computer, in plain readable Markdown that you can edit yourself anytime.

---

## Frequently asked questions

<details>
<summary><strong>Is my data safe? Who can see it?</strong></summary>

- Your `thinking-living` repository is **private** by default. No one but you can see it.
- Your account, your computer, your control. Claude operates inside the boundaries you set.
- Claude **never sends content outside your machine** without telling you first in plain language. If something is about to go on the internet (a posted message, an email, a search query), Claude says so before acting and waits for your "yes."
- The setup is reversible. You can delete the repository anytime; there's no lock-in or proprietary format. Markdown files are readable by any text editor.

</details>

<details>
<summary><strong>What if I'm not technical at all?</strong></summary>

Then this is for you. The whole flow is designed so you don't have to be.

- You don't need to know what GitHub is. Claude explains as you go.
- You don't need to install developer tools yourself. Claude installs them.
- You don't need to remember commands. Claude runs them.
- You answer questions in plain language; Claude does the technical part.

If something feels confusing, just tell Claude. The setup is collaborative, not a wizard you have to pass on your own.

</details>

<details>
<summary><strong>What does it cost?</strong></summary>

- **Claude Pro**: ~200 DKK / 20 USD per month (or yearly equivalent).
- **GitHub**: Free (private repos are free for individual accounts).
- **Total**: just the Claude Pro subscription.

No additional costs. No purchases inside Claude. No "premium" thinking-living features.

</details>

<details>
<summary><strong>What if I already have a Claude account or GitHub account?</strong></summary>

Great — Claude detects that and skips ahead.

- Already have Claude Pro? Step 1 is done.
- Already have GitHub? Claude verifies and uses your existing account.
- Already have Claude Code Desktop installed? Skip the install, go straight to pasting the URL.

Claude probes your computer and asks you only the questions it can't answer for itself.

</details>

<details>
<summary><strong>What if I get stuck or something breaks?</strong></summary>

Tell Claude. The setup is collaborative; if a step fails or something looks weird, Claude surfaces what happened in plain language and walks you through the next move.

If you're really stuck, message the person who shared this URL with you. They've been through the setup themselves and can help.

</details>

<details>
<summary><strong>Why does Claude ask me to install Claude Code Desktop separately? Isn't claude.ai enough?</strong></summary>

Browser-Claude (claude.ai web) can read web pages and have conversations, but it can't install software on your computer or read your local files. Claude Code Desktop can. Both are the same Claude — they share your account and conversation history — but Desktop has powers the browser version doesn't.

The bootstrap uses both: browser-Claude walks you through Pro signup and Claude Code Desktop installation. Then the rest happens in Claude Code Desktop.

</details>

<details>
<summary><strong>What's GitHub and why do I need an account there?</strong></summary>

GitHub is a service where files are stored online (originally for software code, but it works for any text content). Your `thinking-living` Markdown files live in a GitHub repository so:

- They're backed up automatically (your computer breaking doesn't lose them)
- You can use them from any computer (just sign in to your GitHub from there)
- Your Claude(s) on different surfaces (Desktop, web, iOS) can all read the same content

Your GitHub repository is **private** — invisible to everyone except you (and anyone you explicitly invite, which by default is no one).

</details>

<details>
<summary><strong>What if I want to stop using thinking-living later?</strong></summary>

Delete the repository (one-click in GitHub settings) and uninstall Claude Code Desktop. Done. No data is held hostage; no proprietary lock-in. The Markdown files you created are just text files — you can take them with you, edit them in any program, or throw them away.

</details>

---

## For Claude (not for human readers)

If you're a Claude session reading this URL because the user pasted it in: read [BOOTSTRAP-INSTRUCTIONS.md](BOOTSTRAP-INSTRUCTIONS.md) for the executable runbook. That file contains the actual probe-and-act logic for the 4-stage bootstrap.

The user reading the rendered README on github.com sees this section as a note and ignores it. That's intended. The instructions for you are deliberately not in the human-facing README.

---

*If you have questions before you start, ask the person who shared this URL with you. They'll know.*
