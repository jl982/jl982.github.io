# Blog Writing Style Notes (xhigh reasoning)

These notes capture the recurring writing patterns across the posts in `_posts/`, with enough detail for another agent to write a new post that plausibly sounds like “me”.

## Corpus (what this is based on)

Posts reviewed (all `layout: post` entries in `_posts/`):
- `_posts/2020-12-13-5-lines-in-vimrc.md` — “5 lines I put in a blank .vimrc”
- `_posts/2021-01-10-vim-read-logs.md` — “Effectively read logs using vanilla vim”
- `_posts/2021-02-23-probability-code.md` — “Solving probability problem with code”
- `_posts/2021-08-31-jvm-xmx.md` — “Why is my JVM's max heap size less than -Xmx?”

This guide intentionally ignores `_site/` since it’s generated output.

## High-level “voice signature”

If you only remember one sentence:

> A pragmatic, mildly nerdy engineer writes to help a peer solve a real problem, shows concrete evidence early, explains the “why” step-by-step, and keeps the tone humble with occasional dry humor.

Key attributes:
- Clear, practical, and technical, but not academic.
- Mildly conversational and first-person (“I noticed…”, “I thought…”) without turning into a diary.
- Evidence-driven: commands, logs, numbers, code, and outputs appear early and often.
- Humble and low-ego: admits what wasn’t known before, gives credit via links, calls out caveats.
- Light humor / self-awareness sprinkled sparingly (“Phew.”, “Math is beautiful.”, “nerd sniped”).

## Typical post types and their structures

### A) Quick tip / configuration post
Example: the `.vimrc` “5 lines” post.

Template:
1. `## TL;DR` with immediately copy-pastable snippet.
2. Optional follow-up snippet: “spelled out and annotated version”.
3. Optional “Edit” acknowledging reader feedback and updating the recommendation.
4. `## Motivation` describing the real-world context (usually “fresh/remote environment” constraints).
5. `## Discussion` explaining tradeoffs and reasoning; ends with a gentle recommendation.
6. `Discuss this post on [HN](...)`.

Signature moves:
- Provide the exact minimal answer first.
- Use a memorable hook (e.g., acronym like `HIINN`) but keep it subtle.
- Call out when the advice is for temporary environments vs. “properly maintained local setup”.

### B) Workflow tutorial / “show me how” post
Example: the “read logs in vanilla vim” post.

Template:
1. `## TL;DR` as a very short instruction (often “look at the gifs”).
2. `## Preface` explaining why this workflow matters and what constraints exist.
3. A short, copyable sample artifact (log snippet / input) so readers can follow along.
4. Numbered sections for each capability (`## 1. ...`, `## 2. ...`), each with:
   - A 1–3 sentence explanation.
   - A concrete command or keystroke sequence in backticks.
   - Media (gif/video) + `figcaption` summarizing the point.
5. When needed: a breakdown list (“Breakdown of commands…”, “Deconstructing the syntax…”).
6. `## Discussion` + HN link.

Signature moves:
- Teach intuition, not just the recipe (“The goal is to provide you intuition…”).
- Warn about footguns (“But be careful to not save!”) and offer a safe mode / workaround.

### C) Technical deep dive / “why does this happen?” post
Example: the JVM `-Xmx` post.

Template:
1. `## TL;DR` with the one-line formula / answer and a reference link.
2. `## How we got here` as a brief origin story (work problem + “rabbit hole”).
3. Show the minimal reproducer (code) and the observed output early.
4. Rhetorical checkpoint: “Why is that?”
5. Explanatory sections that are enumerated and labeled:
   - `## Reason 0: ...` (yes, starting at 0 is a thing here)
   - `## Reason 1: ...`
   - `## Reason 2: ...`
6. A “math / breakdown” section with numbered steps and actual computed values.
7. `## Loose ends` for remaining curiosities and clarifications.
8. `## Discussion` with a reflective, slightly humorous ending + HN link.

Signature moves:
- Make claims testable: show commands and outputs; name versions (“Java 8”, default GC).
- Use bold sparingly to mark the key conclusion in a section.
- Link to primary sources (docs, Stack Overflow, sometimes source code) when the explanation hinges on details.

### D) Problem solving via code (narrative + experiment)
Example: the probability / Monte Carlo post.

Template:
1. `## The Problem` with a short anecdote about how the problem was found.
2. Quote the exact problem statement as a blockquote.
3. Admit the “math might be hard” moment, then pivot to code as the tool of choice.
4. `## Monte Carlo method` describing the idea and showing runnable code.
5. A mini plot twist (e.g., answer options don’t match) resolved with community consensus / a link.
6. `## Exact solution` showing a cleaner algorithm (often “someone else’s solution” credited via link).
7. Optional: show the math solution as a sanity-check summary.
8. `## Discussion` with a compact reflection about learning vs. pragmatism + HN link.

Signature moves:
- Make the reader feel the “trail”: curiosity → attempt → surprise → resolution.
- Keep the narrative short; let the artifacts (code/output) carry most of the weight.

## Tone and stance (the details)

### How “I” shows up
- “I” is used for:
  - The origin story (“Some time ago at work… I noticed…”).
  - Honest reactions (“Strange,” I thought…; “Interesting,” I thought…; “Phew.”).
  - Confessions of learning (“I didn’t know… but will definitely start doing this…”).
- “We” is used for:
  - Guided walkthroughs (“We run it on…”, “As we can see…”).
  - Shared reasoning (“let’s first look at…”, “to verify, let’s try…”).
- “You” is used for:
  - Direct actionable advice (“You can use…”, “You can run `vim -R`…”).
  - Safe recommendations (“I recommend that you…”).

### Humility without hand-wringing
Common patterns:
- Admit limits / context: “for what it’s worth…”, “probably not…”, “in practice though…”.
- Speculate carefully and label it: “My guess is…”.
- Give credit via links instead of asserting authority.

### Humor and personality (used lightly)
The style has small, controlled “personality leaks”:
- Short single-word/phrase beats: “Phew.”, “Hooray.”, “Math is beautiful.”
- Nerd references: XKCD “nerd sniped”.
- Mild self-deprecation: “blissfully unaware…”, “rabbit hole”.

Rule of thumb: 0–2 small jokes/quirky lines per post; the rest stays straight.

## Language and sentence-level habits

### Diction
- Prefer simple, direct words (“run”, “set”, “copy”, “filter”, “divide”) over fancy synonyms.
- Use precise technical nouns when needed (GC, Survivor Space, CIDR, regex, recursion).
- Define or parenthetically clarify jargon the first time (“vanilla vim (i.e. without custom plugins)”).

### Sentence shape
- Mostly short-to-medium sentences; long sentences appear when listing “the journey” (e.g., “Fast forward through…”) or packing a nuanced caveat.
- Frequent transitional starters: “So…”, “But…”, “However…”, “As it turns out…”, “In fact…”, “Before we…”, “To verify…”, “Finally…”.
- Occasional rhetorical questions as section pivots (“Why is that?”).

### Punctuation / cadence
- Parentheses used often for clarifications and constraints.
- Dashes used to insert quick contrasts (“straightforward - …”).
- Ellipses used sparingly for comic timing (“and found… none?”).
- Quotes used for inner dialogue (“Strange,” I thought…).

## Evidence-first writing (what to include)

### Show the artifact early
Within the first section or two, include at least one of:
- A code snippet the reader can run.
- A command + output block.
- A realistic input sample (e.g., log excerpt).
- A screenshot/GIF with a one-line caption.

### Then explain “why”
After the artifact, the explanation tends to follow this pattern:
1. Restate the observation plainly.
2. Name the controlling factor(s) (version defaults, flags, constraints).
3. Break down the mechanics in steps.
4. Verify with a second experiment or a calculation.
5. Call out caveats and edge cases.

### Quantification style
- Numbers and computed values are frequently wrapped in backticks.
- Approximations are labeled with `~`.
- Units are explicit (bytes, KB, GB).

## Formatting and markup conventions

### Headings
- Use `##` headings heavily; keep them short and descriptive.
- Numbered headings are common for sequences (`## 1. ...`) and for “reasons” (`## Reason 0: ...`).
- End-of-post convention: `## Discussion`.

### Code and command blocks
- Mix of fenced styles: triple backticks and `~~~lang` fences both appear.
- Use language tags when it helps readability (`~~~java`, `~~~python`, `~~~javascript`).
- Shell sessions are shown with `$` prompts inside fenced blocks.

### Lists
- Use numbered lists for sequences of actions or a reasoning chain.
- Use bullet lists to “deconstruct” syntax or list properties.
- When describing a GIF/video, add a short breakdown list right after it.

### Media
- For short demos: HTML `<figure>` with `<video ...>` and `<figcaption markdown=span>...`.
- For step-by-step UI guides: Markdown images `![](...)` (often GIFs) between bullet lists.

### Linking
- External links often include `{:target="_blank"}`.
- Internal links (between posts) use Jekyll `{% raw %}{% link ... %}{% endraw %}` pattern.
- Links are embedded inline rather than footnoted.

### Emphasis
- Bold is used sparingly to highlight the one key sentence in a section.
- Inline code is used heavily for commands, flags, values, and filenames.

## Endings and “takeaway” style

Typical ending components:
- A short reflection: one paragraph max, mildly opinionated but not preachy.
- Optional: “Does this have practical use? Probably not…” style humility.
- A final line: `Discuss this post on [HN](...)`.

If a new post isn’t actually going to HN, keep the spirit:
- Add a brief “Discussion” section anyway, pointing to comments, email, or another forum.

## Variation / outliers to be aware of

The IPv6 EC2 post is intentionally “documentation-like” for most of its length (imperative, step lists, minimal narrative). If you want to match the more personal voice of the earlier posts, lean more on:
- A short origin story (“why I needed this”).
- A concrete artifact or experiment.
- Explanations and tradeoffs, not just steps.

## A practical checklist for writing “like me”

Before writing:
- Decide which post type you’re emulating (Quick tip / Workflow tutorial / Deep dive / Problem-solving narrative).
- Identify the one-liner answer for the TL;DR (even if you don’t label it TL;DR).
- Collect one concrete artifact (code, command+output, log snippet, screenshot).

While drafting:
- Start with the artifact early; don’t bury it.
- Use first-person only where it adds authenticity (origin story, reaction, decision).
- Explain with steps, numbers, and verification; avoid vague claims.
- Include at least one caveat or alternative path.
- Keep jokes rare and short; default to matter-of-fact.

Before finishing:
- Add a compact reflection in `## Discussion`.
- Read the intro aloud: does it sound like a helpful peer, not a press release?
