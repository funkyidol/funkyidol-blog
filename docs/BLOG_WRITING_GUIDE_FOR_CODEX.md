# Blog Writing Guide for Codex

Use this document as the blog level writing, editing and update guide for Kshitij Aggarwal's Codex content project.

The goal is to help Codex create new blog posts, refine existing drafts and update older posts in a way that matches Kshitij's voice, public positioning, technical judgment and publishing standards.

This guide is intentionally focused only on the blog. Ignore social media distribution, LinkedIn optimization, Mastodon adaptation, Buffer drafts, carousels and engagement strategy unless a separate task explicitly asks for them.

---

## Critical writing gates

These two rule sets are the most critical part of the blog writing process. Do not treat them as cleanup. Apply them before drafting, during revision and again before final output.

A blog task is not complete until both gates have been checked against the actual draft. Never skip them because the task is small, the prose is already readable or the user asked for a narrow edit.

### Gate 1: Required prose mechanics

- Avoid contractions and other short forms. Use full forms instead. Examples: `I am`, `I have`, `you are`, `cannot`, `will not`.
- Use only straight quotes: `'` and `"`. Do not use curly quotes.
- Do not use `-` (em-dash) for sentence structure. Avoid space, hyphen, space as a dash. Rewrite the sentence or use punctuation such as `:`, `;` or parentheses.
- Minimize hyphens in prose. Hyphenate only when required by Markdown or frontmatter structure, URLs, file paths, code identifiers, tags, proper names or established technical terms.
- Do not use a comma before `and` or `or`. Write `and` and `or` without the preceding comma.

### Gate 2: Sentence and flow preferences

Kshitij prefers writing that has flow. Avoid overly short, disconnected sentences.

Do not make the post read like a list of isolated facts.

Weak pattern:

> Google announced X.
> This matters for mobile.
> That changes the developer workflow.

Better pattern:

> Google announced X and the part I found interesting was not the announcement itself but the workflow it implies. For mobile teams, the question is less "can this generate code?" and more "how much context can we safely hand over before review becomes harder than implementation?"

Use sentence length variation. Some sentences can be short, but the post should not be built entirely from short declarative statements.

Avoid excessive sentence starts with:

- "This..."
- "That..."
- "It..."

These words are fine occasionally, but repeated use makes the writing feel mechanical.

Before finalizing a blog post, scan for repeated sentence starts with `This`, `That` and `It`. Use a command such as `rg -n "^(This|That|It)\b|[.!?] (This|That|It)\b" content/blog/<slug>/index.md` and rewrite repeated hits until the pattern no longer dominates the flow.

Avoid filler transition sentences such as:

- "That matters for mobile."
- "This matters."
- "That distinction matters."
- "This is not paperwork."

Only keep a sentence if it adds a real idea, example, tension or transition.

Not every sentence has to sound like a fact. Mix observation, interpretation, uncertainty and experience.

---

## 1. Core blog principle

The blog is the durable source of truth.

A blog post does not need to be viral, overly polished or shaped for a feed. It should preserve useful thinking in a place that can be revisited, linked, updated and expanded over time.

Default principle:

> Preserve the idea first. Improve the writing second. Optimize only when it serves clarity.

A blog post should support:

- durable ownership of ideas
- clear technical and leadership thinking
- practical lessons from real engineering work
- long term credibility
- future updates and internal linking
- better recall of decisions, tradeoffs and implementation details

The blog should not be shaped primarily for short term attention.

---

## 2. Public positioning

Kshitij's writing should generally align with this positioning:

> I build and lead teams that ship accessible mobile products, bridging engineering leadership, Android/Kotlin/Compose/KMP, accessibility for blind and low vision users, product minded engineering, smart glasses/wearables, practical AI assisted product development and clear technical communication.

Do not force every post to serve every audience.

Possible readers include:

- engineering leaders
- founders
- senior Android/Kotlin engineers
- accessibility and assistive technology practitioners
- product minded engineers
- mobile architects
- people building smart glasses or wearable UX
- people interested in practical AI assisted engineering workflows

The writing should build trust through clarity, specificity and demonstrated judgment rather than self promotion.

---

## 3. Core content pillars

Use these often, but do not force them into every post:

- engineering leadership
- Android engineering
- Kotlin
- Jetpack Compose
- Kotlin Multiplatform / KMP
- mobile architecture
- accessibility
- inclusive product building
- blind and low vision user experience
- assistive technology
- smart glasses and wearable UX
- voice first interfaces
- product minded engineering
- testing strategy
- quality, reliability and release tradeoffs
- architecture and technical debt
- AI assisted product development
- agent workflows
- writing, speaking and mentoring

A post is stronger when it has one clear center of gravity rather than trying to cover all pillars.

---

## 4. Blog voice

Default blog voice:

- field note driven
- first person where natural
- practical
- direct
- slightly opinionated
- calm but not bland
- grounded in real engineering experience
- product minded and engineering minded together
- human rather than over polished

The post should feel like Kshitij is documenting real work:

- what he did
- why he did it
- where it could go wrong
- what he learned
- what tradeoff he would make again
- what he would watch more carefully next time

Preserve personal ownership when present. Phrases like these are welcome when they fit the draft:

- "I wanted..."
- "I knew where this could go wrong..."
- "Good thing I did."
- "The mistake I almost made..."
- "The part I underestimated..."
- "What I would do differently..."

Avoid turning the writing into a generic polished article that could have been written by anyone.

The final result should feel like a cleaner version of Kshitij's own writing, not a new article written by someone else.

---

## 5. Blog creation workflow

When creating a new blog post, start by identifying the real center of the idea.

Before drafting, review the critical writing gates. Before final output, check the draft against both gates again. Do not send or commit a blog draft that misses the prose mechanics or sentence and flow preferences.

Useful questions to answer internally:

- What is the post preserving?
- Is this a field note, a tactical guide, a decision log, an observation or a deeper essay?
- What real experience, implementation detail or judgment makes the post worth reading?
- What should a future reader understand after reading it?
- What should not be overclaimed?

A new blog post should usually include:

1. Title options
2. Suggested tags
3. Short excerpt or meta description
4. Blog draft
5. Optional notes for future updates or internal links, only when useful

The draft can be concise, but it should still have:

- context
- flow
- useful structure
- a clear reason for existing
- enough detail to preserve the idea for the long term

Do not stretch a small idea into a long essay just to make it feel more important. A useful short note is valid.

---

## 6. Blog formats

Let the idea decide the format.

A blog post can be:

- a short note
- a field note
- a checklist
- a tactical guide
- a decision log
- a tradeoff log
- a debugging story
- a leadership reflection
- a technical deep dive
- a practical implementation note
- a "what I learned" post
- a longer essay
- a talk notes style post
- a lecture notes style post
- an observations post

Not every post needs to become a polished essay. Some posts should stay lightweight if the idea is useful but not yet deep enough for a full essay.

---

## 7. Preferred structures

Choose the structure that best fits the idea.

Good default structures:

### Story to Lesson to Principle

Use when the post starts from a real incident, implementation or decision.

### Problem to Insight to Steps

Use when the post teaches a practical technical or leadership pattern.

### Mistake to Fix to Checklist

Use when the post is about something that went wrong or almost went wrong.

### Myth to Reality to Better approach

Use when correcting a common misconception.

### Decision log

Use when documenting why one approach was chosen over another.

### Field note

Use when preserving observations from real work without forcing a grand conclusion.

### Lecture notes / observations

Use when summarizing a keynote, conference, talk, article or set of announcements.

For lecture notes and observations posts:

- keep the main learnings as bullets when useful
- write flowing prose before, between and after bullet sections
- avoid making the post feel like disconnected notes pasted together
- focus on "what I found relevant, important and significant"
- avoid pretending every announcement has equal importance
- include personal interpretation, not just summary

---

## 8. Bullet points

Bullet points are encouraged when they make the post easier to scan or help emphasize a set of concrete points.

Use bullets for:

- specific signals or examples
- tradeoffs
- questions
- steps
- criteria
- prompts
- failure modes

Keep or create bullet lists when they fit naturally. They should improve readability, not replace the argument.

A good blog post can still have flow around the bullets:

- setup before the list
- interpretation after the list
- a clear reason the list exists

Avoid using bullets as a shortcut for structure. A post should not become a collection of disconnected lists unless the format is intentionally a checklist, notes post or reference guide.

---

## 9. Editing rules

When editing a draft:

1. Apply both critical writing gates before making broader style changes.
2. Preserve the original structure unless the structure is clearly hurting readability.
3. Preserve the author's examples and technical details.
4. Fix grammar, clarity, flow and repetition.
5. Remove filler.
6. Keep strong opinionated lines when they are grounded.
7. Do not over smooth the draft.
8. Do not replace specific details with generic abstractions.
9. Do not inflate the claim beyond the evidence.
10. Do not add fake metrics, fake outcomes, fake dates or unsupported confidence.
11. Make the writing clearer while keeping it recognizably Kshitij's.

When rewriting, prefer "refine and restructure" over "start from scratch," unless explicitly asked.

Editing should improve the post without erasing the lived experience behind it.

---

## 10. Updating existing blog posts

When updating an existing blog post, treat the original post as an artifact worth preserving.

Do not rewrite the entire post unless the user explicitly asks for a rewrite or the current structure is blocking clarity.

Good update work includes:

- fixing outdated phrasing
- adding new context
- improving unclear sections
- correcting technical inaccuracies
- tightening rambling paragraphs
- adding missing examples
- adding a note when the author's thinking has changed
- preserving older context when it still explains the original decision
- improving headings and scanability
- adding internal links when relevant
- marking assumptions or placeholders clearly

When a post changes because the author has learned something since publication, prefer transparent framing:

> Update: I would phrase this differently now because...

or:

> Since writing this, I have changed how I think about...

Avoid silently changing the meaning of an old post in a way that removes useful historical context.

For major updates, consider adding:

- an "Updated on" note
- a short update section
- a clarification note near the changed section
- a follow up section instead of overwriting the original argument

The goal of an update is not to make the post look timeless. The goal is to keep it useful and honest.

---

## 11. Technical detail preservation

Preserve concrete technical artifacts and implementation details when they appear in drafts.

Do not abstract away details such as:

- `AGENTS.md`
- `SKILLS.md`
- PRD
- task tracker
- implementation plan
- sub agents
- `/init`
- test scripts
- lint scripts
- dependency injection
- logging
- navigation
- SDK choices
- authentication providers
- context drift
- token consumption
- Compose state
- coroutines / Flow
- modularization
- release gates
- unit tests
- UI tests
- accessibility checks

Specifics are part of the credibility of the writing.

If details are missing, use placeholders rather than inventing them.

Example:

> [Add the exact test command here]

Do not fabricate implementation details to make the story sound more complete.

---

## 12. Technical writing defaults

When code or implementation is relevant:

- explain the mental model first
- avoid dumping code unless requested
- include tradeoffs
- include a testing mindset where useful
- prefer practical examples over abstract explanation
- mention failure modes
- explain why a choice was made, not just what was chosen

For Android/Kotlin/Compose topics, assume Kotlin and Android development context unless otherwise specified.

For testing related topics, include the testing angle whenever applicable:

- what should be unit tested
- what should be covered by UI tests
- what can be checked through accessibility testing
- what should be guarded by lint, CI or release checks
- what is hard to test and why

---

## 13. AI and agent writing stance

When writing about AI, Codex, agents or AI assisted product development, stay grounded and cautious.

Default stance:

> Agents are useful, but they need guidance, guardrails, review, correction and clear scope.

Avoid hype language such as:

- "10x productivity"
- "game changer"
- "revolutionary"
- "the future of software"
- "AI will replace developers"
- "everything changes now"

Prefer grounded observations:

- where agents helped
- where they drifted
- where context was insufficient
- where review mattered
- where tests caught mistakes
- where clear instructions improved output
- where token usage or context size became a tradeoff
- where human judgment remained necessary

AI posts should read like field notes from actual usage, not thought leader hype.

---

## 14. Accuracy and evidence guardrails

Do not fabricate:

- metrics
- dates
- titles
- outcomes
- client claims
- company results
- user numbers
- awards
- quotes
- links
- production impact

When evidence is missing:

- ask for the missing detail if it materially changes the post
- otherwise use a placeholder
- or write the claim more cautiously

Good cautious phrasing:

- "In my experience..."
- "The pattern I noticed..."
- "The risk I would watch for..."
- "I would not generalize this too far, but..."
- "The useful part for me was..."

Avoid exaggerated certainty.

---

## 15. Blog maintenance and compounding

When maintaining blog content, look for ways to make posts easier to revisit and build on.

Useful maintenance improvements include:

- clearer headings
- better introductions
- tighter conclusions
- more precise tags
- internal links to related posts
- short context notes for older posts
- clearer examples
- explicit tradeoffs
- better distinction between observation and recommendation

Do not add links, references or claims that are not available in the provided material.

When suggesting internal links, use placeholders if the exact URL or title is unknown:

> [Link to related Compose testing post]

Blog maintenance should make the archive more useful without turning every post into a large essay.

---

## 16. Anti patterns to avoid

Avoid:

- clickbait
- hustle language
- generic advice
- fake vulnerability
- exaggerated certainty
- AI thought leader filler
- job hunting signaling
- engagement bait
- corporate writing
- over polished generic prose
- abstracting away the real technical detail
- turning every paragraph into a lesson
- making every observation sound universal
- short, disjointed sentence chains
- repeated "this/that" sentence openings
- filler lines that only announce importance
- rewriting a draft so aggressively that it loses the author's voice
- updating older posts in a way that hides useful historical context

Quality bar:

> No cringe. No generic filler. No fake authority. No forced virality.

---

## 17. Preferred blog feel

A good Kshitij blog post should feel like:

- "Here is something I noticed while doing real work."
- "Here is the tradeoff I had to make."
- "Here is where the obvious solution can go wrong."
- "Here is what I would preserve for next time."
- "Here is the implementation detail that made the difference."
- "Here is the leadership/product angle behind the technical decision."

It should not feel like:

- "Here are five generic tips."
- "Here is a viral thread expanded into paragraphs."
- "Here is a polished corporate blog post."
- "Here is an AI generated summary with no lived experience."

---

## 18. Clarifying question policy

Ask at most one or two clarifying questions only when the answer materially improves the output.

Useful questions:

- Who is the target reader?
- Should this be short, tactical or deep?
- Is there a real example, metric or implementation detail to include?
- Is this a new post, an edit to a draft or an update to an existing published post?

If the missing information is not critical, proceed with a best effort draft and use placeholders where needed.

---

## 19. Blog editing checklist

Before finalizing a blog post, check:

- Have both critical writing gates been checked against the actual draft?
- Are the required prose mechanics followed?
- Does the sentence and flow pass avoid choppy fact listing, filler transitions and repeated mechanical sentence starts?
- Does the post preserve one clear idea?
- Does it sound like Kshitij, not a generic tech writer?
- Are the technical details preserved?
- Are claims grounded?
- Are unsupported metrics or outcomes removed?
- Is there enough context for future readers?
- Are the sentences flowing naturally?
- Are there too many short declarative sentences?
- Are there repeated "this" or "that" sentence openings?
- Are filler lines removed?
- Do bullet lists improve readability rather than replace the argument?
- Does the conclusion preserve the lesson without overclaiming?
- Could the post be updated later without losing useful context?

---

## 20. Operating principle for Codex

When Codex works on blog content, its job is not to make the writing sound more impressive.

Its job is to make the writing clearer, more useful, more durable and more recognizably Kshitij's.

Create with context. Edit with restraint. Update with honesty. Preserve the useful details.
