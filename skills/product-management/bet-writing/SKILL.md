---
name: bet-writing
description: Problem-first writing discipline for product bets. Use when writing or discussing a product bet, a PRD, a PR/FAQ, a problem statement, or the what and why of an initiative.
---

# Bet Writing

Keep the interview problem-first and write the document down as it crystallises. This skill supplies what grilling doesn't know about product work: where the tree's root is, which nodes a bet must answer, and what to write.

## The tree

The root is **the problem**. Nothing branches until the problem names what the customer does today to get the outcome and where that breaks. "There's a gap" is not a root. "They run twenty hand-configured snapshotters and it drifts" is.

Every bet must answer six nodes. Grow the rest of the tree from them:

1. The problem (root).
2. Who it is for, and whether they are existing accounts or new to us.
3. Why now: what changed, and the cost of standing still.
4. What is different for the market: someone who doesn't use us today.
5. Success: what the customer would say made it worth it, and what internal signal moves.
6. Non-goals.

If the invocation doesn't state the bet in a sentence and who the document is for, those are the first two questions of round one.

## Problem, not solution

Every mechanism that appears in the problem moves to open questions. When the user offers a "how" without noticing (a screen, a data model, an integration), name it and ask whether they are committing to it or handing it to engineering; a mechanism they aren't committing to lands in open questions tagged `[engineering]`. A branch answered "we don't know yet" is settled: it lands in open questions tagged `[unknown]`, or `[customer]` when only the customer can answer.

## Make it concrete

Stress-test each settled node with a plausible named scenario in the customer's domain: a named team, a regulated system, an audit question. Placeholders like "application ABC" hide misunderstanding; a plausible invented example exposes it. Label invented examples as invented, in the conversation and in the document.

Name companies and roles, never individuals ("the platform lead at <customer>"), unless the user asks for names.

## Choosing the format

When the root settles, put the format to the user as a frontier question, recommending by audience. Skip the question if the invocation names a format.

- **PRD-lite** ([PRD-FORMAT.md](./PRD-FORMAT.md)): engineering-facing, for a bet already under way or one where the team owns the solution.
- **PR/FAQ** ([PRFAQ-FORMAT.md](./PRFAQ-FORMAT.md)): a new bet, or anything going to executives or the market, where forcing "what is now true for a customer" earns its keep.

## Write as you go

Create the file when the format is chosen: `<slug>-prd.md` or `<slug>-prfaq.md` in the current directory unless the user names a path, and say where it is. Update the relevant section the moment a node settles and report it in one line naming the section ("Updated: The problem, point 3"). A wrong sentence in a half-built section is cheaper to catch than a wrong page at the end.

## Closing

When the frontier is empty, re-read the document once against its format's length rule and stop. The document is the handoff.
