---
name: crack-the-paper
description: Active reading-note generator for scientific papers and research-style long-form documents, based on Carey, Steiner, and Petri (2020) "Ten simple rules for reading a scientific paper." Use whenever the user provides a research paper, long-form research blog, technical report, interactive article, PDF, arXiv link, DOI, URL, or pasted text and wants to read, summarize, critique, take notes on, understand, or extract takeaways from it. Works across scientific fields, with conditional guidance for ML/AI papers such as interpretability, safety, deep learning, and neuroscience-to-ML crossover. Trigger this even when the user just says things like "help me read this paper", "what's this paper about", "summarize this for me", or provides a likely research document without further instruction. Default to producing a structured reading note; do not ask the user to choose a mode.
---

# Crack the Paper

This skill operationalizes the ten rules from Carey, Steiner, and Petri (2020) for active reading of scientific literature. The goal is to help the user truly understand a paper — its motivation, methods, data, and limitations — rather than skim it.

## Core philosophy

Active reading means reading with intent to understand and critique, not to passively absorb. Two ideas drive everything below:

1. **The reader's goal shapes the reading.** A person new to a field reads differently than someone evaluating a paper for journal club.
2. **Published papers are not truths etched in stone.** Even high-impact papers from famous labs have limitations, biases, and alternative interpretations worth surfacing.

## Step 0: Operational intake

Before deciding what to emphasize, establish what material is actually available and what can be inspected.

- If the user provides a PDF, extract the title, authors, venue/year if visible, abstract, section headings, figure captions, tables, references, supplement links, and code/data links when available.
- If the user provides an arXiv link, DOI, paper URL, long-form blog, technical report, or interactive article, use available browser, search, or download tools to retrieve metadata and document text. If those tools are unavailable, proceed from the content the user supplied and state the limitation.
- If the text is pasted without figures, say that figure-level analysis will be limited unless captions, images, or tables are available.
- If figures, tables, widgets, screenshots, or interactive elements cannot be read clearly, do not infer details from the prose alone. Mark those parts as unavailable and focus on the visible text.
- For ML/AI documents, also look for appendix material, benchmark setup, code repositories, model cards, dataset links, and evaluation scripts because key methodological details often live outside the main text.

## Step 1: Default to a structured reading note

When the user brings a paper, produce a structured reading note by default. Do not offer multiple modes or ask whether they want a walkthrough. Bare research-paper uploads with no instruction, or short messages like "help me with this paper", should trigger the skill and proceed with `Read for: general understanding`.

If the user states a purpose (coursework, journal club, evaluating a method for their own research, tracking a technique, curiosity), adapt emphasis accordingly. If no purpose is stated, do not block on clarification.

Default to returning the note inline. Only save it as a Markdown file when the user asks for a file, or when an obvious file/artifact/workspace-write tool is available and inline output would be too long.

Ask a clarifying question only when the paper itself is unavailable, the user request is too narrow to execute from the available artifact, or the user's purpose would materially change the output and cannot be inferred. Keep clarification to one short question.

## Step 2: Identify the reader's intention and the paper's type

Before reading deeply, anchor on two things:

**Reader's intention** (Rule 1) — what does the user want out of this? Prioritize accordingly:

| If the user is... | Prioritize... |
|---|---|
| New to scientific reading | Explain every figure panel carefully and define core concepts on first use |
| Entering a new field | Introduction (motivation) + Conclusion (next steps) |
| Tracking a specific author | Skim the whole thing, place it in their publication arc |
| Tracking a technique or topic | Methods + the motivation in the introduction |
| Reviewing or presenting at journal club | Everything; plus rigor checks, alternative explanations, bias |
| Applying it to their own research | Methods detail + Discussion's "next steps" + connections to their work |
| Deciding whether to trust the paper | Critical read + what's missing + field reception and follow-up |

**Paper type** (Rule 2) — different paper types have different goals:

- **Research article**: presents new data and the authors' interpretation. The default; most rules apply directly.
- **Review article**: summarizes a field or problem. Look for what the authors think is important and what they leave out.
- **Methods paper**: presents a new technique. Focus on what the technique enables, its limits, and what it's compared against.
- **Resource paper**: presents a tool, dataset, or benchmark. Focus on what's released and how it'd be used.
- **Commentary or perspective**: takes a stand. The authors' viewpoint is the point; ask whose viewpoint is missing.
- **Position paper**: argues for a direction or framing. Treat like commentary; weigh the argument's strength.
- **Long-form research blog / technical report / interactive article**: presents research in a nonstandard web or report format. Focus on central claims and the evidence clusters that support them rather than forcing a journal-paper section structure.

For ML/AI papers specifically, also note: is this empirical (experiments and benchmarks), theoretical (proofs, formal results), interpretability-style (analyzing an existing model), or a system paper (engineering an artifact)? The reading priorities differ.

## Step 3: Use the six questions (Rule 3)

For the paper as a whole, and again for each major figure or experiment, use this as an internal checklist:

1. **Motivation** — what do the authors want to know?
2. **Approach** — what did they actually do?
3. **Context** — why did they do it that way? What alternatives exist?
4. **Results** — what does the data actually show? (Look at the figures, not the prose claims.)
5. **Interpretation** — how do the authors read their own results?
6. **Next steps** — what should be done next? Form your own answer first, then check the discussion.

The sixth question is where most readers slack off. Always do it yourself before reading the authors' version.

## Step 4: Unpack figures and tables (Rule 4)

The data is the paper. The prose is the authors' framing of the data. Read figures and tables on their own terms first.

Choose the "Key results" organization based on the document shape:

- **Standard research papers**: follow the figure/table sequence as the narrative spine. Don't bullet the findings in an arbitrary order. Walk through figures and tables in the order the paper presents them, explain what each one shows, and then articulate **why the authors arranged them in that order** — what is each figure doing in the argument? The sequencing is itself a rhetorical choice and reveals what the authors think their strongest evidence is.
- **Long-form blog posts, technical reports, interactive articles, or documents with many screenshots/widgets/case-study figures**: organize "Key results" by 3-6 central claim clusters instead. Under each claim, list the figures, tables, sections, or examples that support it, explain what role each evidence item plays, and attach limitations to the claim they weaken. Treat figures as evidence units, not the narrative spine. Do not enumerate every figure unless the user explicitly asks for a figure-by-figure read.

Also note what the figures **don't** show. If the paper has a benchmark table but no variance bars, no comparison to obvious baselines, or no ablation of a claimed-important component, point that out alongside the figure that "should have" included it.

For each standard data figure:
- What are the x- and y-axes? Units? Log or linear?
- What's the color scheme encoding?
- What statistical test was used, if any? Is it appropriate?
- Why this particular plot type? Would a different view change the story?

For screenshots, widgets, qualitative examples, case-study excerpts, or interactive demos:
- What claim does this evidence support?
- Is it representative, cherry-picked, or only illustrative?
- What would a counterexample look like?
- What evidence would turn this from a suggestive example into a stronger result?

For each table:
- What experimental groups and variables are shown?
- What's missing that you'd expect to see (control conditions, error bars, ablations)?

For ML/AI papers specifically, also check:
- For benchmarks: what baselines? Are they strong baselines or cherry-picked weak ones?
- For ablations: are the right components being ablated?
- For training curves: are these single seeds or averaged? Variance across seeds?
- For interpretability claims: is the evidence necessary, sufficient, or just suggestive?

After each standard figure or each nonstandard evidence cluster, articulate the "take home" in one sentence in your own words.

## Step 5: Read the sections for what they are (Rule 5)

Different sections of a standard paper serve different purposes and deserve different scrutiny:

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

Even "objective" sections (Results, Methods) are written by humans with intentions. Look for what's emphasized and what's downplayed.

For long-form blogs, technical reports, interactive articles, or documents without standard paper sections, do not force this table onto the source. Instead, identify the document's own structure: central claims, evidence clusters, case studies, demos/widgets, appendix details, and limitations. Preserve useful section names from the source only when they clarify the argument.

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

Use field-specific standards where they matter: sample size and controls in biology, calibration and uncertainty in measurement-heavy fields, identification assumptions in causal social science, boundary conditions in theory papers, and robustness or reproducibility checks in computational work.

For ML/AI papers, common failure modes to flag:
- Strong claims on one benchmark; silence on others.
- Hyperparameter sweeps that benefit the proposed method more than baselines.
- Interpretability evidence that is suggestive but not causal (correlation between an activation and a concept does not mean the activation causes the behavior).
- Cherry-picked qualitative examples without quantitative backing.
- "Emergent" or "surprising" framings that vanish under careful measurement.

## Step 7: Be kind (Rule 7)

The authors are human. A clunky sentence, a missed citation, or a misnumbered figure does not indicate bad science. Separate cosmetic issues from substantive ones when critiquing.

For private reading notes, be direct and technically sharp. Do not soften substantive criticism just to sound polite.

If the user will share critique with the authors or in a public setting (journal club, social media, review, email): phrase substantive critiques constructively. "This claim would be stronger if..." reads very differently from "This claim is wrong because..." even when the technical content is identical. Junior authors especially can be wounded by harsh framings of fair points.

## Step 8: Go the extra mile (Rule 8)

To truly understand a paper, you often have to look things up:
- Unfamiliar terms: define them before continuing.
- Cited prior work: at least skim the most-cited references.
- Supplemental material: where the inconvenient results often live.
- Code or data, if released: skim to see if the methods match the description.

Use a three-pass workflow when the document is substantial: first pass to build a rough mental model, second pass for critical examination of methods/evidence/claims, and third pass to write the structured note. For short papers or narrow user requests, compress these passes rather than padding the process.

If the user is reading along, the same three-pass habit applies to them too. Encourage them to actually look up unfamiliar things — don't just paper over with a quick gloss.

## Step 9: Talk about it (Rule 9)

Understanding is solidified by articulating. Suggest the user explain the paper to someone — a peer, a mentor, a non-scientist friend, or even just back to you in their own words. Each level of explanation (full technical, big picture, "what this means for a normal person") reveals different gaps in understanding.

Make this visible in the note with an "Explain it three ways" section. If you cannot explain the paper simply without hiding behind jargon, revisit the TLDR, motivation, and key results.

## Step 10: Build on it (Rule 10)

The lego brick metaphor: every paper sits on a wall of prior work, and your own work will sit on top. The original image leaves a blank top brick for the reader's own work. That blank brick is the user's brick; the Connections section should explicitly name what could go on it.

Help the user explicitly connect the paper to:

- **Bricks below**: prior work, methods, datasets, theories, or assumptions the paper builds on.
- **The user's brick**: the project, course question, research idea, implementation, critique, or decision the user might build from this paper.
- **Bricks above**: open questions, follow-up experiments, replications, extensions, or applications this paper makes possible.

**Personalize the Connections section using only available context.** If the conversation or accessible memory gives the user's research area, coursework, ongoing projects, or technical background, use that knowledge to draw specific connections — not generic "this might be relevant to ML researchers" platitudes. Do not invent missing background, and do not surface personal details unless they directly improve the reading note. If the user has explicitly asked for a non-personalized read, respect that; otherwise default to personalizing from available context.

For the user's career stage and goals, also prompt:
- Is there a technique here worth implementing or adapting?
- Does this change which problems look tractable?
- Does it suggest an angle on a project they're already working on?

## Step 11: Track what happened after the paper

For papers more than ~6 months old, the paper itself is only half the story. The other half is **what the field did with it** — follow-up work, replications, criticisms, extensions, real-world adoption (or failure to adopt). This context often changes how to read the original.

For the reading note, use available web/search tools for follow-up work and assessments before finalizing the note. Use the current year and recent prior years rather than hard-coded dates. Useful queries:
- `<paper title or key method name> follow-up` or `<method name> <current year> <previous 2-3 years>`
- `<paper title> criticism` or `<method name> limitations`
- `<first author last name> <method name>` to find the authors' own follow-up work
- Google Scholar, Semantic Scholar, Connected Papers, Papers with Code, or arXiv citation trails when available

Expand date placeholders into actual integers before querying. For example, in 2026, use queries containing `2024 2025 2026`, not the literal text `<current year>`.

What to look for:
- Direct extensions by the same authors (often reveals what they themselves thought needed fixing)
- Independent replications (did the result hold?)
- Critical follow-ups (what did others find broken or overstated?)
- Whether the method became standard, niche, or abandoned
- Application to new domains (vision → NLP, etc.)

Include this as a dedicated section in the notes (see template). Be honest if the answer is "this paper was largely forgotten" — that's itself important information, often more so than a list of citations.

Include links or precise source names/dates for claims about follow-up work when the environment supports that. If web tools are unavailable, the user forbids search, the paper is very recent (<6 months), or the search returns nothing substantive, say so briefly rather than padding the section.

## Output: Structured reading note

Always produce a structured reading note using this template. Adapt sections to the paper type and reader's intention; don't pad sections that aren't useful.

Default output behavior:

- Start with metadata, paper type, and the user's purpose or `general understanding`.
- Separate the authors' claims from what the data actually shows.
- Make "Key results" evidence-driven rather than abstract-driven. Use figure/table order for standard papers; use claim clusters for long-form blogs, technical reports, interactive articles, or figure-heavy documents.
- Surface limitations next to the result they weaken, then summarize broader concerns in "Critical read" and "What's missing."
- Keep "Critical read" and "What's missing" distinct: "Critical read" evaluates what the paper did and how to push back on it; "What's missing" lists important things the paper did not do at all, such as missing controls, baselines, populations, ablations, or follow-up experiments.
- Mark unavailable evidence explicitly instead of guessing from prose.
- End with a concrete take-home, not a question or an offer.

**Length calibration.** Match the note length to the paper's complexity, not to the template's section count. A short methods paper or a focused empirical paper might warrant a 600 to 1000 word note. A dense theory paper, a long review, or a paper with many experiments might warrant 1500 to 2500 words. If a section has nothing substantive to add, write one sentence and move on — don't pad. The reader is busy.

```markdown
# [Paper Title]

**Authors**: [author list]
**Venue / Year**: [venue, year]
**Paper type**: [research / review / methods / position / long-form blog / technical report / interactive article / etc.]
**Read for**: [user's stated intention, or "general understanding" if none was given]

## TLDR
[1-2 sentences in your own words. Not the abstract.]

## Motivation
[What problem are they trying to solve? Why does it matter?]

## Approach
[What did they do, at a level a colleague in an adjacent field could follow.]

## Key results
[For standard research papers: walk through the figures and tables in the order the paper presents them. For each, explain what it shows and what role it plays in the argument. For long-form blogs, technical reports, interactive articles, or figure-heavy documents: organize this section by 3-6 central claim clusters. Under each claim, list the supporting figures/tables/sections/examples, explain what each contributes, and place limitations next to the claim they weaken. Add observations the source itself does not state explicitly but that follow from the evidence.]

### [Claim or Figure/Table]
[Evidence, role in the argument, and nearby limitations.]

## How the authors interpret it
[Their reading of the results, separated from the data itself.]

## Critical read
[Evaluate what the paper actually did. Push back on methodology, evidence quality, interpretation, assumptions, alternative explanations, generalization, and robustness. Be specific.]

## What's missing
[Important things the paper did not do at all: controls, baselines, populations, ablations, measurements, replications, follow-up experiments, or alternative analyses.]

## Field reception and follow-up
[What happened after this paper. Direct follow-ups by the same authors, independent extensions, criticisms, replications, real-world adoption or non-adoption. Be honest if the paper was largely forgotten. Skip or shorten if the paper is too recent for this to be answerable.]

## Connections
- **Bricks below**: [Prior work, methods, datasets, theories, or assumptions this paper builds on.]
- **The user's brick**: [How this relates to the reader's course, project, research area, implementation plans, critique, or decisions. Use only information available in the current conversation or accessible memory; do not invent background.]
- **Bricks above**: [Follow-up questions, replications, extensions, or applications this paper opens.]

## Open questions / next steps
[What would you want to know next? What experiments would settle the remaining doubts?]

## Explain it three ways
- **One sentence for a non-scientist**: [Plain-language version with no field jargon.]
- **One paragraph for an adjacent-field colleague**: [A technically literate explanation that defines field-specific terms.]
- **One paragraph for an in-field expert**: [A concise technical explanation using the field's normal vocabulary.]

## Take home
[One sentence: what does this paper actually tell us about the world?]
```

## Language

Default to the language the user is writing in. If they're writing in Chinese, produce notes in Chinese. If mixed, mirror their mix. Field-specific technical terms can stay in English when that is how the field is normally read.

## Voice and level

The notes are written **for the specific reader**, not for a generic audience. Adapt the prose level using only information available in the current conversation or accessible memory. Do not invent the user's background, and do not expose sensitive personal details that are not necessary for the note.

**Calibrate to their expertise in the paper's subfield specifically**, not their general technical level. Someone with a PhD in one area is a beginner in another. A neuroscience PhD reading an interpretability paper has deep methodological intuitions but may not know which SAE variant is current; an ML engineer reading a neuroscience paper knows tensor math but may not know what a spike-triggered average is.

Adjust along these axes:

- **Concept density**: For experts, you can use field-standard terms without unpacking. For newcomers, define on first use, ideally with a one-line intuition rather than a textbook gloss.
- **Mathematical depth**: Match the user's comfort. If they have a strong math background, drop equations in directly. If not, render the equation in words first and the formula second (or skip the formula when the intuition is enough).
- **What gets explained vs assumed**: For someone with relevant background, skip the basics and spend the words on what's genuinely new or contested. For newcomers, spend more words building intuition for why the standard approach exists before getting to what this paper changes.
- **Tone**: Match the user's own register. If they write casually and informally, write back the same way. If they write in dense academic prose, you can be more formal. Don't impose a single house style.

**The same paper notes can look very different for different readers.** That's the point. A reader's existing knowledge is the scaffolding the notes attach to; ignoring it forces them to either re-read what they already know or guess at what you skipped.

If you have no information about the reader's level in this specific subfield, default to "informed graduate student in an adjacent scientific field" — assume general scientific literacy but not ML expertise or deep subfield expertise.

## What to avoid

- Don't just summarize the abstract back. The abstract is the authors' framing; the user wants more than that.
- Don't be falsely deferential to high-impact venues or famous labs. Critique on the merits.
- Don't manufacture critique either — if a result is solid, say so. Phony skepticism is as useless as phony enthusiasm.
- Don't reproduce extended passages from the paper. Paraphrase. Quote sparingly (under 15 words at a time) when exact wording matters.
- Don't end a reading note with a question. End with the take-home.
