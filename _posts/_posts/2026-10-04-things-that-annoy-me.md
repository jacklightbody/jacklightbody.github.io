---
layout: post
title:  "Things That Annoy Me"
date:   2026-10-04
---
At previous jobs I could always rattle off a list of \~5 services or systems that just didn't work quite right. Some modeled the wrong domain object, some were breaking at scale, and some had just always been held together by duct tape and good wishes. The exact items on the list changed, but there was always a list. 

Some things got on the list from an inconveniently timed combustion and an incident. Others from a code review that never quite answered my concerns. But the most common way was annoying me while I worked on something else. 

I can't count the number of times I'd have a build all planned out in my head only to start coding and quickly realize that I was relying on some other component that just wasn't right. I’d then need to choose between totally reworking my plan or trying to tear down the other service and reconstructing it correctly.

With LLMs I haven’t been experiencing that frustration much. Yet I find myself missing it. That first-hand experience and pain helped me prioritize and find the natural leverage points where I could invest some focus and make every future build easier.

Maybe that doesn’t matter. Why care about tracking problems when you can fix them just-in-time whenever they bite you. But how long might that take? How will customers have encountered them in the meantime? How can you be confident that you’ve fixed it the right way if you haven’t felt the pain of the problem?

I've been trying to bring that pain back up to the surface. A few approaches I've found useful so far:

1. Doing processes manually to start. It’s a lot easier to judge what should be hard and what should be easy once I’ve done something myself a few times. As a bonus, this also gives me a verification dataset for free.  
2. Dogfooding. Nothing new here, but when you're actually using the product every day it's far clearer which edges fit together awkwardly, even without looking through reams of code.  
3. Timeboxing LLMs when prototyping. If the LLM can't do something I think should be simple in a few minutes, it's a decent sign there's something deeper going on. "Why are you thinking so much?" has proven to be a pretty useful prompt.

Even with these, I don't think my list is quite as accurate as it used to be. But at least it’s a list.

