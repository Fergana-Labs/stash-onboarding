# Extraction rules

Three kinds of page, three questions:

- **Term** — *what is this thing?* Durable, re-encountered, needs context.
- **Event** — *what happened?* Dated, episodic, does not repeat.
- **Procedure** — *how do we do this?* Repeatable, reusable next time.

When something fits two, write the durable one and link it from the other. A
launch is an event; the product is a term; how launches get run is a procedure.

## Terms

Extract a term when a future agent would otherwise ask "what is that?" or "which
one do you mean?" — people, teams, customers, products, projects, codenames,
systems, repos, dashboards, environments; acronyms and jargon whose local
meaning differs from the general one; named artifacts that live somewhere
specific (*the marketing strategy*, *the pricing doc*), where the value is
knowing what it says and where it is; local conventions like naming schemes,
tiers, and statuses.

The test: the phrase points at a **specific** thing in this person's world, and
knowing which thing changes how you act.

**Every named entity gets its own page.** A customer, prospect, partner,
competitor, product, project, or person named in more than one record gets a
page under its own name, even when each individual mention is thin and even
when the material would fit on a broader page. A thin page that exists beats a
rich page nobody can route to: someone asking "what do we know about
<entity>?" gets nothing back from a paragraph buried in a strategy page. Say
plainly on the page how little is known.

Skip generic vocabulary used generically, a phrasing seen once with nothing
attached, a status that will be false next month (event), and a list of steps
(procedure). An entity that appears exactly once with nothing attached stays a
dated mention on a related page — but count occurrences across every source
before deciding, not just the one in front of you.

Lead with one sentence on what it is, then current state, then whatever of key
facts, where it lives, relationships, and open questions has content. A reader
who stops after two sentences should still be right.

Updating:

- Rewrite toward the present; do not append a paragraph per run.
- Keep prior state only when it explains the current state, and date it.
- Contradicted claims get superseded — state what is true now, then what it
  replaced and when.
- Two sources disagree with neither governing: record both with dates, mark the
  page `uncertain`. Do not average them.
- Facts live on one page; others link rather than copy. Check `terms.md` and
  aliases for the same thing under another name before creating.
- Consolidation applies to concepts and procedures, never to named entities.
  Two concepts saying the same thing should merge; two customers never should.

For a set whose membership changes — customers, active projects, team members —
where one source is authoritative, write down how to enumerate that source
instead of caching a member list. A cached list presented as current is worse
than no list; dated, clearly non-exhaustive examples are fine.

## Events

Record an event when something changed the world: a decision, a launch, an
incident, a customer conversation, a reversal, a piece of work finished, a
significant agent session. Skip chatter that changed nothing.

Write it as a short monologue — five to ten sentences of plain prose, the way
you would tell a colleague: what happened, who was involved, what led to it,
what came out of it, what it implies. Link the terms it touches.

Date it by when it happened, not when you read it; convert relative references
using the source's own timestamp, and say so if the date is approximate. Event
pages are written once. New information usually means a new event plus an update
to the term page, not a rewrite of history.

## Procedures

A procedure is a repeatable method or policy: how marketing analysis gets done
here, how a release is cut, how an escalation is handled, where a report's
inputs come from.

Promote one when it's a clear procedure that could be used again, or the user
stated it as how things should be done. Consolidate aggressively — three
near-identical procedures are one page with the variations named inside it — and
replace the duplicated steps on term and event pages with a link.

Never promote an agent's suggestion into a procedure. A proposal gets
`status: proposed` and the name of whoever proposed it.

Cover the trigger, the steps, the inputs and where they come from, the gotchas,
the variations, and the owner.

## Evidence

Rank conflicting sources:

1. Explicit user correction or confirmation
2. User statement
3. Approved source document or record
4. Agent output the user explicitly accepted or acted on
5. Agent proposal — kept as a proposal, never as fact

The assistant side of a transcript is not ground truth. In a session, extract
from the user turns; read agent turns only to resolve what the user meant. The
brief sits at levels 1–2: it establishes what the user believes and approves,
not facts about the outside world.

## Time

- Prefer the newest *applicable* evidence, not the newest timestamp. A recent
  restatement does not override a later decision.
- Convert relative dates to explicit ones before writing.
- Before finalizing an overview or collection, check whether a newer decision
  elsewhere governs it — recency within one channel is not recency overall.
  Link the governing page rather than copying it.
- Label proposals, drafts, and incomplete work instead of presenting them as
  state.

## Retention

Keep a material detail even if it appeared once — who, what, when, where, the
number, the exception. Retention is not endorsement. When dropping a mention
would make an inventory look complete, keep it as an unverified mention with its
date, and invent nothing: a mentioned company is not a customer, competitor, or
partner until a source says so.
