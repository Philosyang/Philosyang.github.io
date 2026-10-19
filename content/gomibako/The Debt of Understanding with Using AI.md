---
title: "The Debt of Understanding with Using AI"
date: 2026-09-30
# tags: ["slice-of-life"]
---

there is an increasing issue of these both in work and life.
in work, people work with AI to create PRs that contains 10k+ lines of diff then have trouble understanding it but raised the PR nonetheless since AI can take care of the whole process (ghe lets you write PR desc and then some). The burden shifts to the reviewer to a point the reviewers use AI to review the PRs (10k+ lines btw) and prays that AI catches all the bugs / misalignments, sends a lgtm, and merges. The results is significantly less stable code, everyone can feel it, the stable release is no longer nearly as stable, and new incident tickets contains context nobody understands (but the AI).
in life, people asks AI to "split this costco bill to my roommates" and then AI misclassifies smth between personal use (buys pays all, e.g. candies bought for themself) vs. even split (e.g. toilet paper, detergent, etc). and it gets slipped unnoticed until later another roommate discovered that hey why is your candy and clothes in the shared pool or smth even more complicated like when it gets old and nobody even knows if its personal or shared.
how would you frame this issue as a whole and what can we do to prevent this?

---

Both cases are the same problem: AI made it almost free to produce an artifact, but it did not make it any cheaper to understand one, so artifacts now get approved by people who do not understand them.

Before AI, producing the work forced understanding. You could not write 10,000 lines without knowing roughly what they did, and you could not split a Costco receipt without deciding, item by item, what was shared. The author was a free first check, and the reviewer checked someone who already understood the work. Now the author of record signs the work but cannot explain it. I would call the result comprehension debt (work that exists but nobody can explain). You pay it back later, with interest, during incidents or roommate arguments. Your observation about incident tickets that only the AI understands is exactly that debt coming due.

Two mechanisms produce the debt. The first is volume beyond human reading capacity. When a PR is larger than anyone can read, review becomes a ritual, and an AI reviewing an AI is not an independent check because both can share the same blind spots. Two models agreeing looks like confirmation but is closer to one opinion counted twice. The second mechanism is hidden judgment. In the Costco case, the arithmetic was fine. The failure was a judgment call ("is this candy shared?") that needed private knowledge the AI did not have. The AI then showed that guess in the same confident format as the math, so nobody noticed it was a guess. Time makes this worse, because intent is easy to know at the moment of purchase or authorship and nearly impossible to recover months later.

So the prevention follows from two rules. The output must stay small enough that the responsible human can actually read it, and every judgment call must go to a human who has the context, at the time the context still exists.

At work, that means a size cap on PRs and stacked PRs for large changes. Cisco's well-known review study found that defect detection falls off sharply past a few hundred lines per review, and that result predates AI. The author writes the intent of the change in their own words before generating anything, and must answer reviewer questions without the AI, for example in a short walkthrough. Tests that a human wrote or read become the real specification, because a reviewer can verify a test far faster than 10,000 lines of implementation. AI review is still useful as a first pass that lists risky areas, but the human reviewer then reads those areas instead of trusting the summary. Staged rollouts and feature flags limit the damage when something slips through. The strongest cultural lever is ownership: the author of a change owns its incidents. People stop shipping code they cannot explain when they know they will be the one explaining it at 2 a.m.

At home, let the AI do the mechanical part and make it show its judgment. Ask for a line-item table with a shared or personal label on each item and a flag on anything uncertain, and have each roommate confirm their own lines before anyone pays. Better still, classify at checkout, for example by splitting the transaction or marking personal items on the receipt that day, because that is the moment when everyone still knows what the candy was for. A simple default rule also helps: anything that is not obviously a household item counts as personal unless someone claims it as shared.

The common principle is that a human approves decisions, not outputs. AI can generate the output, but the decision has to be small enough to see and made by someone who knows the answer.