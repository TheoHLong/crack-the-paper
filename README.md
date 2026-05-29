# Crack the Paper

A portable AI-agent skill that turns research-paper and long-form technical reading from passive consumption into active interrogation. It can be used as a packaged Claude skill or as a raw `SKILL.md` folder for Codex and other skill-compatible agents.

**Philosophy:** A paper is not a truth etched in stone. It is one team's argument, made with selected evidence, framed in their preferred light. Reading well means following the figures, pushing back on the claims, asking what the field decided afterward — not just absorbing the abstract.

## What You Get

Give the agent a paper, long-form research blog, technical report, interactive article, PDF, arXiv link, DOI, URL, or pasted text. It will produce **a structured reading note** you can save and refer back to, written for *your* background.

The structured note follows the paper's evidence rather than its abstract. For standard papers, it walks figure by figure; for long-form blogs, technical reports, and interactive articles, it groups evidence into the central claim clusters. It pushes back critically on the claims, searches the web for follow-up work and field reception, and connects the paper to your own research, courses, and ongoing projects.

## How It's Different from "Summarize This Paper"

Most paper summarizers give you a polished version of the abstract. This skill does the opposite:

* **Evidence leads, prose follows.** For standard papers, the "Key results" section walks through figures and tables in the order the paper presents them. For long-form blogs, technical reports, and interactive articles, it groups figures, examples, and sections by the claims they support.
* **Critique is the default, not an afterthought.** Every claim gets pushed on: alternative explanations, methodology limits, generalization concerns, missing controls, and field-specific failure modes.
* **The story doesn't end with the paper.** For papers older than ~6 months, the skill searches for follow-up work, replications, criticisms, and real-world adoption. Sometimes the most important fact about a paper is what the field did or didn't do with it.
* **Notes are written for you.** The skill calibrates vocabulary, math depth, and tone to your background (subfield expertise specifically, not general technical level), using only the current conversation and any memory available to the agent.

## Philosophy in 11 Steps

Based on Carey, Steiner, and Petri (2020) "[Ten simple rules for reading a scientific paper](https://doi.org/10.1371/journal.pcbi.1008032)" (PLOS Computational Biology), with one addition.

1. Pick a reading goal — what you want determines how you read
2. Understand the author's goal — what kind of paper is this?
3. Ask six questions — motivation, approach, context, results, interpretation, next steps
4. Unpack each figure and table — the data is the paper
5. Read sections for what they are — separate claims from evidence
6. Be critical — published papers in top venues are not truths etched in stone
7. Be kind — authors are human; separate cosmetic flaws from substantive ones
8. Go the extra mile — look up the terms, read the cited references
9. Talk about it — explaining solidifies understanding
10. Build on it — connect to your own work, your other reading
11. **Track what happened after** — follow-ups, criticisms, adoption *(new in this skill)*

The 11th step is what most paper-reading advice misses. A paper from 2020 means something different in 2026 — sometimes the field embraced it, sometimes it quietly died, sometimes the authors themselves published a follow-up admitting the limits. That context belongs in the notes.

## Install

### Claude-compatible upload

1. Download [`crack-the-paper.skill`](./crack-the-paper.skill)
2. In Claude.ai, go to Settings → Capabilities → Skills, and upload the file
3. Upload a paper and it will trigger automatically

### Codex or raw-folder install

Clone the repo and install the inner [`crack-the-paper/`](./crack-the-paper/) folder, not the outer repository folder. The skill root is the directory that directly contains `SKILL.md`:

```
crack-the-paper/
└── SKILL.md
```

For a local Codex install, copy or symlink that inner folder into the skills directory your Codex setup loads.

## Repository structure

```
crack-the-paper/
├── README.md
├── crack-the-paper.skill     # Packaged skill, ready to install
└── crack-the-paper/
    └── SKILL.md              # The skill source — workflow, templates, prompts
```

## Built With

* [skill-creator](https://github.com/anthropics/skills) — scaffolding for building portable agent skills
* The original [Ten Simple Rules](https://doi.org/10.1371/journal.pcbi.1008032) paper by Carey, Steiner, and Petri (2020)

## Contributing

Feedback, issues, and PRs welcome. If you use this skill on a paper and feel the notes missed something important, that's the most useful feedback — open an issue with the paper title and what was missing.

## License

MIT
