---
name: crack-the-paper
description: Active reading guide for scientific papers, based on Carey, Steiner, and Petri (2020) "Ten simple rules for reading a scientific paper." Use whenever the user uploads a research paper (PDF, arXiv link, or pasted text) and wants to read, summarize, critique, take notes on, prepare a journal club presentation, or extract takeaways from it. Especially useful for ML/AI papers (interpretability, safety, deep learning, neuroscience-to-ML crossover) but works for any scientific article. Trigger this even when the user just says things like "help me read this paper", "what's this paper about", "summarize this for me", "I need to present this", or uploads a PDF without further instruction — assume active reading is wanted unless they explicitly ask for something narrow like a one-line TLDR.
---

# Crack the Paper

This skill operationalizes the ten rules from Carey, Steiner, and Petri (2020) for active reading of scientific literature. The goal is to help the user truly understand a paper — its motivation, methods, data, and limitations — rather than skim it.

## Core philosophy

Active reading means reading with intent to understand and critique, not to passively absorb. Two ideas drive everything below:

1. **The reader's goal shapes the reading.** A person new to a field reads differently than someone evaluating a paper for journal club.
2. **Published papers are not truths etched in stone.** Even high-impact papers from famous labs have limitations, biases, and alternative interpretations worth surfacing.

## Step 1: Pick a mode

When the user brings a paper, ask which mode they want, unless their message contains an unmistakable signal (e.g. they literally said "summarize this", "take notes", "walk me through this"). Bare PDF uploads with no instruction, or short messages like "help me with this paper", count as ambiguous — ask.

**Guided mode** (conversational walkthrough): The user wants to learn how to read papers, is new to the topic, or signals they want to discuss as they go. In this mode, take the user through the paper section by section, asking the Rule 3 questions and waiting for their thoughts before moving on.

**Notes mode** (direct deliverable): The user wants a structured artifact they can save and refer back to. In this mode, produce a structured markdown note (see template below) without back-and-forth, and save it as a file using the present_files tool so the user can keep it.

When asking, also briefly check the user's intention: what are they reading this for? Examples: studying for a course, evaluating a method for their own research, preparing journal club, just curious. The answer shapes which sections get emphasis (see Step 2). Combine both questions into one short message — don't make it feel like an interrogation.

## Step 2: Identify the reader's intention and the paper's type

Before reading deeply, anchor on two things:

**Reader's intention** (Rule 1) — what does the user want out of this? Prioritize accordingly:

| If the user is... | Prioritize... |
|---|---|
| New to scientific reading | Every figure panel, asking Rule 3 questions of each |
| Entering a new field | Introduction (motivation) + Conclusion (next steps) |
| Tracking a specific author | Skim the whole thing, place it in their publication arc |
| Tracking a technique or topic | Methods + the motivation in the introduction |
| Reviewing or presenting at journal club | Everything; plus rigor checks, alternative explanations, bias |
| Applying it to their own research | Methods detail + Discussion's "next steps" + connections to their work |

**Paper type** (Rule 2) — different paper types have different goals:

- **Research article**: presents new data and the authors' interpretation. The default; most rules apply directly.
- **Review article**: summarizes a field or problem. Look for what the authors think is important and what they leave out.
- **Methods paper**: presents a new technique. Focus on what the technique enables, its limits, and what it's compared against.
- **Resource paper**: presents a tool, dataset, or benchmark. Focus on what's released and how it'd be used.
- **Commentary or perspective**: takes a stand. The authors' viewpoint is the point; ask whose viewpoint is missing.
- **Position paper** (common in ML/AI): argues for a direction or framing. Treat like commentary; weigh the argument's strength.

For ML/AI papers specifically, also note: is this empirical (experiments and benchmarks), theoretical (proofs, formal results), interpretability-style (analyzing an existing model), or a system paper (engineering an artifact)? The reading priorities differ.

## Step 3: Ask the six questions (Rule 3)

For the paper as a whole, and again for each major figure or experiment, work through:

1. **Motivation** — what do the authors want to know?
2. **Approach** — what did they actually do?
3. **Context** — why did they do it that way? What alternatives exist?
4. **Results** — what does the data actually show? (Look at the figures, not the prose claims.)
5. **Interpretation** — how do the authors read their own results?
6. **Next steps** — what should be done next? Form your own answer first, then check the discussion.

The sixth question is where most readers slack off. Always do it yourself before reading the authors' version.

## Step 4: Unpack figures and tables (Rule 4)

The data is the paper. The prose is the authors' framing of the data. Read figures and tables on their own terms first.

**In notes mode, the "Key results" section should follow the figure/table sequence as its narrative spine.** Don't bullet the findings in an arbitrary order. Walk through figures and tables in the order the paper presents them, explain what each one shows, and then articulate **why the authors arranged them in that order** — what is each figure doing in the argument? The sequencing is itself a rhetorical choice and reveals what the authors think their strongest evidence is.

Also note what the figures **don't** show. If the paper has a benchmark table but no variance bars, no comparison to obvious baselines, or no ablation of a claimed-important component, point that out alongside the figure that "should have" included it.

For each figure:
- What are the x- and y-axes? Units? Log or linear?
- What's the color scheme encoding?
- What statistical test was used, if any? Is it appropriate?
- Why this particular plot type? Would a different view change the story?

For each table:
- What experimental groups and variables are shown?
- What's missing that you'd expect to see (control conditions, error bars, ablations)?

For ML/AI papers specifically, also check:
- For benchmarks: what baselines? Are they strong baselines or cherry-picked weak ones?
- For ablations: are the right components being ablated?
- For training curves: are these single seeds or averaged? Variance across seeds?
- For interpretability claims: is the evidence necessary, sufficient, or just suggestive?

After each figure, articulate the "take home" in one sentence in your own words.

## Step 5: Read the sections for what they are (Rule 5)

Different sections of a paper serve different purposes and deserve different scrutiny:

| Section | What it's for | How to read it |
|---|---|---|
| Title | Authors' chosen "headline" | Note what's claimed and what's vague |
| Abstract | The elevator pitch | Read once before, once after; see what changed |
| Introduction | Motivation and field context | Note what literature is and isn't cited |
| Methods | What was done | Pretend you'll reproduce it; flag missing detail |
| Results | Objective data presentation | Look for hedging language hiding weak effects |
| Discussion | Authors' interpretation | The most opinion-laden part; push back hard here |
| Conclusion | Implications | Compare to what the abstract promised |
| References | The lego bricks below | Note who's cited, who's missing |
| Supplemental | Extra material | Often where the inconvenient results live; worth checking |

Even "objective" sections (Results, Methods) are written by humans with intentions. Look for what's emphasized and what's downplayed.

## Step 6: Be critical (Rule 6)

This is the heart of active reading. Published papers in high-impact venues, by famous labs, are not truths etched in stone. Push back on every claim.

For any conclusion the paper draws, ask:

- **Alternative explanations**: Is there another, equally likely, story for what's observed?
- **Methodology limits**: What does this method genuinely measure, and what can't it see?
- **Selection bias**: Why this dataset, these subjects, this benchmark? What was filtered out?
- **Confounders**: What unmeasured variables could be driving the result?
- **Generalization**: How far does the conclusion actually reach? One model, one task, one architecture?

**Watch your own biases too.** Two failure modes:
- Loving the paper because it confirms what you already believe (or wish were true).
- Dismissing the paper because it contradicts your work or worldview.

Ask yourself directly: "Would I be applying this same scrutiny if the result went the other way?"

For ML/AI papers, common failure modes to flag:
- Strong claims on one benchmark; silence on others.
- Hyperparameter sweeps that benefit the proposed method more than baselines.
- Interpretability evidence that is suggestive but not causal (correlation between an activation and a concept does not mean the activation causes the behavior).
- Cherry-picked qualitative examples without quantitative backing.
- "Emergent" or "surprising" framings that vanish under careful measurement.

## Step 7: Be kind (Rule 7)

The authors are human. A clunky sentence, a missed citation, or a misnumbered figure does not indicate bad science. Separate cosmetic issues from substantive ones when critiquing.

If the user will share critique with the authors or in a public setting (journal club, Twitter, review): phrase substantive critiques constructively. "This claim would be stronger if..." reads very differently from "This claim is wrong because..." even when the technical content is identical. Junior authors especially can be wounded by harsh framings of fair points.

## Step 8: Go the extra mile (Rule 8)

To truly understand a paper, you often have to look things up:
- Unfamiliar terms: define them before continuing.
- Cited prior work: at least skim the most-cited references.
- Supplemental material: where the inconvenient results often live.
- Code or data, if released: skim to see if the methods match the description.

A common practice: read the paper three times. First pass without pressure to understand. Second pass for understanding. Third pass taking notes. Time-consuming but builds real comprehension.

If the user is working through a paper with you, encourage them to actually look up the unfamiliar things — don't just paper over with a quick gloss.

## Step 9: Talk about it (Rule 9)

Understanding is solidified by articulating. Suggest the user explain the paper to someone — a peer, a mentor, a non-scientist friend, or even just back to you in their own words. Each level of explanation (full technical, big picture, "what this means for a normal person") reveals different gaps in understanding.

## Step 10: Build on it (Rule 10)

The lego brick metaphor: every paper sits on a wall of prior work, and your own work will sit on top. Help the user explicitly connect the paper to:

- Other papers they've read (which bricks below?)
- Their own ongoing work (which brick are they trying to lay?)
- Open questions the paper opens up (what bricks come next?)

**Personalize the Connections section using what's in user memory.** If you know the user's research area, coursework, ongoing projects, or technical background, use that knowledge to draw specific connections — not generic "this might be relevant to ML researchers" platitudes. The Connections section is where the notes go from generic to genuinely useful, and personalization is what makes that flip. If the user has explicitly asked for a non-personalized read, respect that; otherwise default to personalizing.

For the user's career stage and goals, also prompt:
- Is there a technique here worth implementing or adapting?
- Does this change which problems look tractable?
- Does it suggest an angle on a project they're already working on?

## Step 11: Track what happened after the paper

For papers more than ~6 months old, the paper itself is only half the story. The other half is **what the field did with it** — follow-up work, replications, criticisms, extensions, real-world adoption (or failure to adopt). This context often changes how to read the original.

For notes mode, do a web search for follow-up work and assessments before finalizing the note. Useful queries:
- `<paper title or key method name> follow-up` or `<method name> 2023 2024 2025`
- `<paper title> criticism` or `<method name> limitations`
- `<first author last name> <method name>` to find the authors' own follow-up work
- Google Scholar "cited by" if the paper is on arXiv (the arXiv ID is in the citation)

What to look for:
- Direct extensions by the same authors (often reveals what they themselves thought needed fixing)
- Independent replications (did the result hold?)
- Critical follow-ups (what did others find broken or overstated?)
- Whether the method became standard, niche, or abandoned
- Application to new domains (vision → NLP, etc.)

Include this as a dedicated section in the notes (see template). Be honest if the answer is "this paper was largely forgotten" — that's itself important information, often more so than a list of citations.

If the paper is very recent (<6 months) or the search returns nothing substantive, say so briefly rather than padding the section.

## Output: Notes Mode template

When producing a structured reading note (notes mode), use this template. Adapt sections to the paper type and reader's intention; don't pad sections that aren't useful.

**Length calibration.** Match the note length to the paper's complexity, not to the template's section count. A short methods paper or a focused empirical paper might warrant a 600 to 1000 word note. A dense theory paper, a long review, or a paper with many experiments might warrant 1500 to 2500 words. If a section has nothing substantive to add, write one sentence and move on — don't pad. The reader is busy.

```markdown
# [Paper Title]

**Authors**: [author list]
**Venue / Year**: [venue, year]
**Paper type**: [research / review / methods / position / etc.]
**Read for**: [user's stated intention]

## TLDR
[1-2 sentences in your own words. Not the abstract.]

## Motivation
[What problem are they trying to solve? Why does it matter?]

## Approach
[What did they do, at a level a colleague in an adjacent field could follow.]

## Key results
[Walk through the figures and tables in the order the paper presents them. For each, explain what it shows. Then articulate the logic of the sequence — why this figure before that one, what each is doing in the paper's argument. Add observations the paper itself does not state explicitly but that follow from the data (e.g. "Table 3 implicitly shows that the gap to CNN grows with depth", "Figure 4 raises a question the authors do not address").]

- Figure 1: [what it shows, why it's first]
- Table 2: [what it shows, what role it plays in the argument]
- ...

## How the authors interpret it
[Their reading of the results, separated from the data itself.]

## Critical read
[Your push-back. Alternative explanations, methodology limits, generalization concerns. Be specific.]

## What's missing
[Experiments not run, baselines not compared, populations not included.]

## Field reception and follow-up
[What happened after this paper. Direct follow-ups by the same authors, independent extensions, criticisms, replications, real-world adoption or non-adoption. Be honest if the paper was largely forgotten. Skip or shorten if the paper is too recent for this to be answerable.]

## Connections
[How does this relate to the reader's own work, courses, or research area? Use what you know about the reader from memory and earlier conversation to make this specific. Generic ML/AI relevance is not useful here.]

## Open questions / next steps
[What would you want to know next? What experiments would settle the remaining doubts?]

## Take home
[One sentence: what does this paper actually tell us about the world?]
```

## Language

Default to the language the user is writing in. If they're writing in Chinese, produce notes in Chinese. If mixed, mirror their mix. Technical terms in ML/AI can stay in English even within Chinese prose — that's how the field is read.

## Voice and level

The notes are written **for the specific reader**, not for a generic audience. Adapt the prose level using what you know about them from memory and conversation.

**Calibrate to their expertise in the paper's subfield specifically**, not their general technical level. Someone with a PhD in one area is a beginner in another. A neuroscience PhD reading an interpretability paper has deep methodological intuitions but may not know which SAE variant is current; an ML engineer reading a neuroscience paper knows tensor math but may not know what a spike-triggered average is.

Adjust along these axes:

- **Concept density**: For experts, you can use field-standard terms (SAE, IRT, ELBO, signSGD) without unpacking. For newcomers, define on first use, ideally with a one-line intuition rather than a textbook gloss.
- **Mathematical depth**: Match the user's comfort. If they have a strong math background, drop equations in directly. If not, render the equation in words first and the formula second (or skip the formula when the intuition is enough).
- **What gets explained vs assumed**: For someone with relevant background, skip the basics and spend the words on what's genuinely new or contested. For newcomers, spend more words building intuition for why the standard approach exists before getting to what this paper changes.
- **Tone**: Match the user's own register. If they write casually and informally, write back the same way. If they write in dense academic prose, you can be more formal. Don't impose a single house style.

**The same paper notes can look very different for different readers.** That's the point. A reader's existing knowledge is the scaffolding the notes attach to; ignoring it forces them to either re-read what they already know or guess at what you skipped.

If you have no information about the reader's level in this specific subfield, default to "informed graduate student in an adjacent field" — assume general ML/science literacy but not deep subfield expertise.

## What to avoid

- Don't just summarize the abstract back. The abstract is the authors' framing; the user wants more than that.
- Don't be falsely deferential to high-impact venues or famous labs. Critique on the merits.
- Don't manufacture critique either — if a result is solid, say so. Phony skepticism is as useless as phony enthusiasm.
- Don't reproduce extended passages from the paper. Paraphrase. Quote sparingly (under 15 words at a time) when exact wording matters.
- Don't end a notes-mode output with a question. End with the take-home.
