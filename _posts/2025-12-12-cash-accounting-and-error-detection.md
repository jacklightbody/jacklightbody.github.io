---
layout: post
title:  "Accrual Accounting & Error Detection"
date:   2025-12-12
---
Most accounting starts out following cash: when money comes in, mark revenue up; when money goes out, mark expenses down. It’s simple, but there’s something comforting in simple. Plus, it comes with built-in error detection: if your books say you have $50,000 but the bank says $42,000, you probably screwed up somewhere.

Still, cash based accounting quickly reaches its limits: a company with $50,000 in the bank should definitely be underwater if it’s also overdue on three different $25,000 payments. The typical way to handle this is to switch to booking expenses on the day that the contract says they’re due, not when the cash actually moves (and do the same with recognizing revenue when it’s earned, not when it’s paid). This is commonly known as accrual based accounting. 

Accrual accounting is far more faithful to actual economic reality and can seem only marginally more difficult. But implementing it can quickly turn into a minefield as it sacrifices the innate error-detection that cash accounting offers. Simply checking your bank balance isn’t enough to check your work anymore. 

I experienced this first-hand at AngelList, where I led the switch from cash-based accounting to accrual based accounting across tens of thousands of distinct entities. We built a sprawling beast of an accounting system with dozens of currencies, thousands of subledgers, and millions of journal entries. Setting up the infrastructure to support this was a pain but ultimately tractable. The much harder problem was verifying that the output of such a complex system was actually correct. 

The typical way to ensure correctness across complex accounting spaces is to run audits: you can be pretty confident in your results if a third-party accountant has pored over your books, examined supporting evidence, run validations, and ended up with the same answer. But that breaks at scale. At the end of the day, auditors are just people, constrained by human error, human cost, and human response times. They can’t guarantee correctness, only increase confidence—and even if they only miss 1% of edge cases, that quickly becomes unacceptable across tens of thousands of entities. Plus, since we produced dozens of new entries every hour of the day we’d need an army of auditors available 24/7 to keep up with the demand.

LLMs face a very similar problem. Agents already out-produce humans by orders of magnitude, but without guarantees of correctness (or the legal culpability that comes with human judgment), their effectiveness is bottlenecked by the verification of their work.  I don’t think it’s a coincidence that so much of the initial agent success stories have been in coding. Software development structurally resembles cash accounting, where actions produce an immediate, unambiguous signal: the unit tests either pass or fail[^1].

Most domains aren’t like that, and instead rely on webs of human reviews through audits or certifications to reach high levels of accuracy. But those human reviews will never be fast or objective enough to actually provide meaningful feedback to the agent and improve performance. Instead, the agent will produce massive quantities of work at an unknown quality bar. In short, slop.

A naive fallback to speed up feedback is to use a second LLM as the judge. But that’s akin to using an intern as an auditor. While it might occasionally work, it’s still just another probabilistic guess, not a true control layer. You really need automated review steps to apply determinism and domain context to be confident in their work. 

At AngelList, we approached this by embedding the domain context directly into the work output. We encoded accounting rules into a “checks” sheet that was embedded in every report we produced. The checks in it ranged from the basic (assets \+ liabilities \= equity) to highly context-specific tests on carried-interest allocations. But it meant that if you opened a spreadsheet and the checks didn’t clear, you instantly knew something was wrong in the upstream accounting. 

This method unlocked several other powerful abilities for us. As we tried out different hypotheses and fixes, we got an instant feedback loop to check our work. And, since these checks run \~instantly, we could run them with every single new transaction that came in. It’s much easier to zero in on the specific issue if only one or two variables have changed since yesterday than it would be to audit the hundreds or thousands of events that might have happened throughout the quarter. 

While we deployed this in a deterministic accounting system, the same pattern applies to autonomous agents in any complex domain. If an Excel agent produces a model for me, I’m likely to be pretty skeptical by default. Yes I can audit every formula by hand, but that’s slow and defeats the whole point of using an agent in the first place. I’d trust it much more if I knew that the model had already passed through a battery of unit tests— and, I bet the model would be much more likely to actually produce a correct model.

I’d love to see more of this as AI work accelerates. In simple problem spaces like cash accounting, it’s trivial to prove correctness because every action emits a clean, mechanical signal. But as AI enters increasingly complex domains, those signals won’t exist until we build them. If we want agents to produce reliable work instead of slop, we can’t rely on smarter models or clever LLM-as-judge hacks. Instead we need to encode expert’s domain knowledge into the system as deterministic rules that the system must satisfy before it’s done. 

In other words: don’t just build better agents. Build better checks tabs. I think that’s where the real breakthroughs will happen.

Hook

Everyone seems to be building agents these days— making them smarter, more capable, and cheaper to run. It seems like they can do everything humans can, but faster. But without real verification, that speed just gets you to the wrong answer faster. The real opportunity is in effectively embedding domain context into the verification layer so you get better answers, not in making a better slop machine.

[^1]:  Plus, researchers [already know the rules of the domain](https://jacklightbody.github.io/2025/10/14/legibility-and-ai.html).
