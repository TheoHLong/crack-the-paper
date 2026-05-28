# read-paper

A Claude skill for active reading of scientific papers, based on Carey, Steiner, and Petri (2020) "[Ten simple rules for reading a scientific paper](https://doi.org/10.1371/journal.pcbi.1008032)" (PLOS Computational Biology).

## What it does

When you upload a research paper to Claude with this skill installed, Claude will:

1. Ask whether you want a **guided walkthrough** or a **structured note**
2. Walk the paper figure by figure, explaining what each shows and why the authors sequenced them that way
3. Push back critically (alternative explanations, methodology limits, missing experiments)
4. Search for follow-up work and field reception, so you see what happened after the paper, not just the paper itself
5. Personalize the connections and voice based on what Claude knows about you

Especially useful for ML/AI papers (interpretability, safety, deep learning, neuroscience-to-ML crossover), but the workflow works for any scientific article.

## Install

1. Download `read-paper.skill` from this repo (or build it yourself, see below)
2. In Claude.ai, go to settings and add the skill

## Build from source

The `.skill` file is just a zip of the skill folder. To build:

```bash
zip -r read-paper.skill read-paper/
```

Or use Anthropic's `package_skill.py` if you have skill-creator installed.

## Structure

```
read-paper/
└── SKILL.md      # The skill itself (workflow + notes template)
```

## What it adds beyond the original paper

The original 10 rules cover how to read a single paper. This skill adds an 11th step: **tracking what happened after the paper** (follow-up work, criticisms, real-world adoption). For papers more than ~6 months old, that context often matters more than the paper itself.

## Credits

Workflow based on:

Carey MA, Steiner KL, Petri WA Jr (2020) Ten simple rules for reading a scientific paper. *PLoS Comput Biol* 16(7): e1008032. https://doi.org/10.1371/journal.pcbi.1008032

## License

MIT (or whatever you prefer).
