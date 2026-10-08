---
layout: post
title: "Cloudflare's Free Security Audit Skill for Claude Code"
description: "Cloudflare open sourced a free security audit skill that found 7,245 real bugs in its own code. Here is how to install it and run your first audit."
author: ness
categories: [Claude Code, AI Automation]
tags: ["cloudflare security audit skill", "claude code security", "ai code audit", "vibe coding", "claude skills"]
image: assets/images/cloudflare-security-audit-skill-free-header.jpg
featured: false
---

Cloudflare's `security-audit` skill is a free, open source skill that turns Claude Code, OpenAI Codex, or any coding agent with parallel sub-agents into a security auditor for your own repository. One `npx` command installs it, then you ask your agent to audit the codebase: it maps the architecture, sends isolated agents out to hunt for vulnerabilities, and hands every candidate to a fresh agent whose only job is to disprove it. The skill is the single-repo starting point for the internal harness Cloudflare described in June 2026, which compressed roughly 20,799 raw candidates into 7,245 actionable findings across 145 of its own repositories.

If you built your app by vibe coding and have never had the code looked at, this is the closest thing to a real security review you can run tonight.

---

## Get the Free Guide

The guide has the install commands for Claude Code and Codex, the exact prompts I run, what each of the three report files contains, and the sandbox setting that quietly downgrades half your findings if you skip it.

**[Get the free Cloudflare Security Audit Playbook →](https://hub.digicuratoragency.com/freebie?kw=audit)**

---

<div style="max-width: 315px; margin: 2rem auto;">
  <div style="position: relative; padding-bottom: 177.78%; height: 0; overflow: hidden; border-radius: 10px;">
    <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
      src="https://www.youtube.com/embed/CRW955ZSVyM"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen></iframe>
  </div>
</div>

## What Is Cloudflare's Security Audit Skill?

It is a folder of markdown instructions plus two Node.js validators that teach a coding agent how to run a disciplined security audit instead of a quick skim. Cloudflare published it at [github.com/cloudflare/security-audit-skill](https://github.com/cloudflare/security-audit-skill) under the MIT license, and it had passed 26,000 GitHub stars as of October 2026.

Inside the repo you get `SKILL.md` for setup and core principles, phase files such as `RECONNAISSANCE.md`, `HUNTING.md` and `VALIDATION-AND-REPORTING.md`, about a dozen domain-specific hunting guides, `report-schema.json`, and `validate-findings.cjs` plus `validate-coverage-ledger.cjs` so the agent's own output gets checked against a schema.

There is no scanner in there. No rule database and no CVE list. The model does the finding, and the skill is the process that keeps it honest about what it found.

## How Does the Six-Phase Audit Work?

The audit runs in six phases, and each phase has to read the file the previous one wrote, which is what stops the agent from improvising.

| Phase | What happens | Files written |
|---|---|---|
| 1. Reconnaissance | Maps architecture, trust boundaries, input surfaces and prior evidence | `architecture.md`, `coverage-ledger.json` |
| 2. Coverage-led hunting | Isolated hunters take units off the ledger, record their checks, and coverage critics look for gaps | ledger updates |
| 3. Candidate validation | Every unique candidate goes to a fresh verifier that tries to disprove it | none |
| 4. Structured output | Writes `confirmed`, `needs_validation` and `rejected` records | `findings.json` |
| 5. Record verification | New agents re-check the source claims behind the final records | `findings.json` updates |
| 6. Reporting | Derives a target-neutral write-up from verified records | `REPORT.md`, `FINDINGS-DETAIL.md`, `NEEDS-VALIDATION.md` |

The coverage ledger is the piece doing the real work. Left alone, an agent wanders, re-reads the three files it already understands, and tells you the app looks fine. The ledger gives it a list of units it is accountable for, and a critic whose job is to say what got skipped. If you want the background on why an agent needs that kind of scaffolding at all, I broke down [how the LLM brain and the harness around it split the work](https://blog.digicuratoragency.com/ai-agents-llm-brain-harness-system/).

## Why Does It Produce Fewer False Positives?

Because the agent that finds a bug is never the agent that checks it. That single rule is the reason the report is short enough to act on.

Findings land in one of three verdicts, and they are deliberately unequal:

1. **`confirmed`** needs a complete source trace and a bounded observed result. No trace, no confirmation.
2. **`needs_validation`** records the exact unresolved fact that blocked the check and gets no severity at all.
3. **`rejected`** keeps the disproved candidate on file so a later run does not hand it back to you.

Cloudflare also draws a line most tools do not: a defense-in-depth gap is a hardening note, not a vulnerability. If layer A already stops the attack, a missing layer B is not a finding. On their internal harness, the independent validation rejection rate dropped from 40% to 11% once this structure was in place, and high-integrity findings went from 35% to 58%.

One honest limit, straight from the repo: in Cloudflare's test runs a single pass found roughly half the vulnerabilities that repeated passes found in total. Runs are additive, so the second and third audit are worth the tokens.

## How Do You Install and Run It?

Installation is one command through the Skills CLI, and it works with any agent that CLI supports.

1. Install it into the current project:

```bash
npx skills add https://github.com/cloudflare/security-audit-skill \
  --skill security-audit
```

2. Or install it once for every project with `--global`:

```bash
npx skills add https://github.com/cloudflare/security-audit-skill \
  --skill security-audit \
  --global
```

3. Make sure Node.js is on your machine. The two validators need it, and they have zero dependencies.
4. Start your agent inside the repo you want audited, or point it at one.
5. Ask for the audit in plain language: `security audit this codebase`, `find security vulnerabilities in ./src`, or `do a security review, output to ~/audits/my-project`.

The skill triggers itself on requests like those. A direct audit or pen-test request gets full audit mode; a general security question gets guidance mode instead unless you ask for the report files. If you do not name an output directory, full audit mode writes to `~/security-audit-skill/<repo-name>/run-<N>`, and it only writes inside your repo if you pick a path that version control ignores.

The one setting people skip: the skill wants an OS-enforced sandbox before it will run target-controlled builds, tests, browsers or fuzzers, with external networking off, a sanitized environment and writes limited to assigned scratch paths. Without that, the audit does not execute suspicious code. It parks the lead as `needs_validation`, which is honest, and also why some first reports look thin.

## What Does It Check in a Vibe Coded App?

The hunting guides split by target type, so a Next.js app with an AI feature gets different prompts than a native binary. These are the ones that fire for most vibe coded projects:

- `WEB-PROTOCOL-AND-AUTH.md` for HTTP request framing, cache behaviour and authentication protocol flaws
- `CLIENT-SIDE.md` for DOM injection, messaging trust, UI redress and prototype pollution
- `AI-AND-LLM.md` for prompt injection, agent and tool abuse, and unsafe output handling
- `SUPPLY-CHAIN-AND-RELEASE.md` for dependencies, CI, signing and update paths
- `CLOUD-AND-DEPLOYMENT.md` for IAM, infrastructure as code, containers, serverless and ingress
- `DATA-ISOLATION-AND-LIFECYCLE.md` for tenant isolation, exports, backups and deletion
- `ATTACK-CLASSES.md` for the core set plus wildcards and the obvious things everyone forgets

`AI-AND-LLM.md` is the one I would not skip. Plenty of small apps pipe user text straight into a model and then act on the answer, and almost nobody checks that path. If you want more free skills to sit alongside this one, start with the [Claude skill packs organised by department](https://blog.digicuratoragency.com/claude-skill-packs-every-department/) or the [ECC repo that installs agents and skills in one command](https://blog.digicuratoragency.com/ecc-claude-code-repo-agents-skills/).

## FAQ

### Is Cloudflare's security audit skill free?

Yes. It is MIT licensed and public on GitHub, so there is no fee and no account. You only pay your coding agent's normal token costs for the run.

### Does it work with Codex, or only Claude Code?

It works with any coding agent whose model supports tool use and parallel sub-agents, which covers Claude Code and OpenAI Codex. Run `npx skills --help` for the agent-selection and non-interactive options.

### How many bugs did it actually find at Cloudflare?

The harness this skill seeded produced 7,245 actionable findings for engineering teams out of roughly 20,799 raw candidates, across 145 repositories. Cloudflare published those numbers on 18 June 2026.

### Will it fix the vulnerabilities it finds?

The report gives you the verified finding with its source trace and a remediation write-up in `FINDINGS-DETAIL.md`, and your agent can apply the fix from there. The audit phases themselves only read and verify, they do not patch.

### Do I need a sandbox to run the audit?

You can run it without one, but anything that needs target code executed stays as `needs_validation` instead of becoming a confirmed finding. For a small app that is usually fine. For anything with real users, set up the sandbox.

## Start With One Repo

Pick your messiest project, install the skill, and run `security audit this codebase` tonight. Then run it a second time, because the repo tells you plainly that one pass finds about half of what two or three passes find. A free audit that reports fewer, verified bugs beats a paid scanner that hands you 400 maybes.

If you want the full set of AI systems I run my business on, come [Join the Vibe Coding Build →](https://hub.digicuratoragency.com/about).

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Is Cloudflare's security audit skill free?",
      "acceptedAnswer": { "@type": "Answer", "text": "Yes. It is MIT licensed and public on GitHub, so there is no fee and no account. You only pay your coding agent's normal token costs for the run." }
    },
    {
      "@type": "Question",
      "name": "Does it work with Codex, or only Claude Code?",
      "acceptedAnswer": { "@type": "Answer", "text": "It works with any coding agent whose model supports tool use and parallel sub-agents, which covers Claude Code and OpenAI Codex. Run npx skills --help for the agent-selection and non-interactive options." }
    },
    {
      "@type": "Question",
      "name": "How many bugs did it actually find at Cloudflare?",
      "acceptedAnswer": { "@type": "Answer", "text": "The harness this skill seeded produced 7,245 actionable findings for engineering teams out of roughly 20,799 raw candidates, across 145 repositories. Cloudflare published those numbers on 18 June 2026." }
    },
    {
      "@type": "Question",
      "name": "Will it fix the vulnerabilities it finds?",
      "acceptedAnswer": { "@type": "Answer", "text": "The report gives you the verified finding with its source trace and a remediation write-up in FINDINGS-DETAIL.md, and your agent can apply the fix from there. The audit phases themselves only read and verify, they do not patch." }
    },
    {
      "@type": "Question",
      "name": "Do I need a sandbox to run the audit?",
      "acceptedAnswer": { "@type": "Answer", "text": "You can run it without one, but anything that needs target code executed stays as needs_validation instead of becoming a confirmed finding. For a small app that is usually fine. For anything with real users, set up the sandbox." }
    }
  ]
}
</script>
