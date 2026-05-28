# Crack the Paper

A [Claude skill](https://support.anthropic.com/) that turns paper reading from passive consumption into active interrogation.

**Philosophy:** A paper is not a truth etched in stone. It is one team's argument, made with selected evidence, framed in their preferred light. Reading well means following the figures, pushing back on the claims, asking what the field decided afterward — not just absorbing the abstract.

## What You Get

Upload a paper to Claude (PDF, arXiv link, pasted text). Claude will ask whether you want:

* **A guided walkthrough** — section by section, asking you the right questions as you go, so you learn how to read papers, not just what this one says
* **A structured note** — a markdown file you can save and refer back to, written for *your* background

The structured note walks figure by figure through the paper's evidence, articulates why the authors sequenced their figures that way, pushes back critically on the claims, searches the web for follow-up work and field reception, and connects the paper to your own research, courses, and ongoing projects.

## How It's Different from "Summarize This Paper"

Most paper summarizers give you a polished version of the abstract. This skill does the opposite:

* **Figures lead, prose follows.** The "Key results" section walks through every figure and table in the order the paper presents them, and articulates *what each one is doing in the argument*. The sequencing of figures is itself a rhetorical choice; you'll see it.
* **Critique is the default, not an afterthought.** Every claim gets pushed on: alternative explanations, methodology limits, generalization concerns, missing baselines. For ML/AI papers, common failure modes (suggestive-not-causal interpretability evidence, cherry-picked baselines, single-seed results) are checked by default.
* **The story doesn't end with the paper.** For papers older than ~6 months, the skill searches for follow-up work, replications, criticisms, and real-world adoption. Sometimes the most important fact about a paper is what the field did or didn't do with it.
* **Notes are written for you.** The skill calibrates vocabulary, math depth, and tone to your background (subfield expertise specifically, not general technical level), using what Claude knows about you from memory and conversation.

## Philosophy in 11 Steps

Based on Carey, Steiner, and Petri (2020) "[Ten simple rules for reading a scientific paper](https://doi.org/10.1371/journal.pcbi.1008032)" (PLOS Computational Biology), with one addition.

1. Pick a reading goal — what you want determines how you read
2. Understand the author's goal — what kind of paper is this?
3. Ask six questions — motivation, approach, context, results, interpretation, next steps
4. Unpack each figure and table — the data is the paper
5. Read sections for what they are — Discussion is opinion, Results is data
6. Be critical — published papers in top venues are not truths etched in stone
7. Be kind — authors are human; separate cosmetic flaws from substantive ones
8. Go the extra mile — look up the terms, read the cited references
9. Talk about it — explaining solidifies understanding
10. Build on it — connect to your own work, your other reading
11. **Track what happened after** — follow-ups, criticisms, adoption *(new in this skill)*

The 11th step is what most paper-reading advice misses. A paper from 2020 means something different in 2026 — sometimes the field embraced it, sometimes it quietly died, sometimes the authors themselves published a follow-up admitting the limits. That context belongs in the notes.

## Install

1. Download [`read-paper.skill`](./read-paper.skill)
2. In Claude.ai, go to Settings → Capabilities → Skills, and upload the file
3. Upload a paper to Claude and it will trigger automatically

You can also clone the repo and use the raw `SKILL.md` directly with Claude Code or any agent that supports skills.

## Repository structure

```
crack-the-paper/
├── README.md
├── read-paper.skill          # Packaged skill, ready to install
└── read-paper/
    └── SKILL.md              # The skill source — workflow, templates, prompts
```

## Built With

* [skill-creator](https://github.com/anthropics/skills) — Anthropic's official scaffolding for building Claude skills
* The original [Ten Simple Rules](https://doi.org/10.1371/journal.pcbi.1008032) paper by Carey, Steiner, and Petri (2020)

## Contributing

Feedback, issues, and PRs welcome. If you use this skill on a paper and feel the notes missed something important, that's the most useful feedback — open an issue with the paper title and what was missing.

## License

MIT
