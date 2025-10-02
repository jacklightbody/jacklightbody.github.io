---
layout: post
title:  "Accounting"
date:   2025-10-1
---

I initially joined AngelList to learn more about venture capital and startups. Ya know, the sexy headline topics. Yet over time, I found myself increasingly interested in accounting, which was probably the last thing I would’ve expected. In fact, I’d never really thought about accounting before, nor was it in the job description when I joined. But over time it grew from a side consideration for the company— “Oh yeah, we have those two accountants who kept our valuations updated”— to one of the businesses main considerations.

Despite knowing nothing about the space, I was tapped to build the first version of our accounting product. I went into it with a vague “I guess now I gotta figure this out” attitude. I read a bunch of articles online, asked our accounting team a bunch of questions, and got to a point where I could rationalize why debits sometimes increased balances[^1]. I essentially viewed accounting as a different way of visualizing the same information, much like you might export a dataset in json or xml. 

To handle this, I built a system to transform a snapshot of our database into an accountant ready report. I compared these reports against the small handful that accountants were manually creating a quarter, and slowly iterated on any transaction rulesets that weren’t functioning quite right. But the core of the system still treated our relational database as the source of truth, and just added a translation layer to turn it into a table in excel that accountants could interact with.

While this system worked well enough, it didn’t get immediate applause from the accounting team. They used it, but seemed to keep tripping up on the same issues and didn’t seem to be gaining that much leverage vs. compiling reports manually.

Eventually, I learned that my core assumption of building a “translation” layer was deeply wrong. At it’s heart, much of accounting is really about control, not information presentation. By mandating that every debit have a corresponding credit for the same amount, accountants can instantly prevent a whole category of errors. By encoding multiple debits/credits in a single entry accountants can tell a story of a transaction that will bear up to auditor scrutiny. You just can’t get those same guarantees translating a relational database into double-entry bookkeeping, so any attempt will always fall short.

That was really weird to me. Databases have lots of nice properties that a flat set of transactions don’t. It’s really easy to encode relationships between things, to perform operations in bulk, and to add validations. But that’s my perspective as an engineer. For accountants, it’s exactly the opposite:

- If they want to encode a relationship in a database, they need to bug an engineer  
- If they want to perform a bulk operation they need to bug an engineer  
- If they want to add validations, they need to bug an engineer

In short, it’s a completely illegible system to them\! They can only interact with the database through narrowly defined tools that I create with them to do so. And they’re relying on these tools they don’t fully understand to do their job, knowing full well that they’ll be the ones getting yelled at if things go south, not me. If I want to build a product that they’ll really enjoy and love, I needed to live in their world rather than asking them to use mine. 

That was the initial hook that pulled me into accounting, but the closer I looked the more interesting it became. Double-entry bookkeeping was established [half a millenia ago](https://www.math.stonybrook.edu/~tony/whatsnew/column/bookkeeping-1001/book1.html) and has now outlived countless civilizations, much less technologies. Accounting is absolutely everywhere, running through every single company and country out there. And it’s not a rigid formula, but something that’s formed and shaped both by the goals of the company and the person working on it: just like companies will spin up new corporate entities or change pricing structures purely to adjust their accounting numbers, different accountants will make have different risk tolerances and make different judgment calls.

Accounting doesn’t get the spotlight that software or management practices do, but it’s one of the deepest systems operating the modern world. 

Or maybe I’m just a geek :)

[^1]:  For anyone unfamiliar with accounting, here’s a 3 bullet explanation: 

    * Imagine all the money that a business earns, spends, owns, or owes is a bucket filled with different amounts of water (money). 
    * As transactions happen, water can only get moved by simultaneously decreasing the water in one bucket and increasing it in another bucket. This is called a debit/credit, and they always have to be paired.
    * If the company earns some money, they credit their earnings (income) bucket. So the corresponding increase in owned assets (cash) must therefore be a debit.

