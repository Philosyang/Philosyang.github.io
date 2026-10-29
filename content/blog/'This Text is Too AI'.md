---
title: "'This Text is Too AI'"
date: 2026-10-29
tags: ["slice-of-life"]
---

During work today, my upper level said: "this part is very AI. Can you rewrite it by hand?" - What do they actually mean?

There are IRL cases of me thinking about this as well - when I see overly repeating sentence structures such as "This (_makes sure that_ something is done), _not (the other way around)_" or the Opus 5's infamous jargon-maxxing chats (which ultimately led me using the simple-english output style), I get that these sentences are likely being written by an LLM. It felt like I just spent another second reading on a thing I already comprehended, but I still need to read through it because I don't know if I know it or not until I read it.

I think the main expectation gap is that the LLM does not know as good as what you know about the target audience. It sometimes overly dissects a viewpoint too many times (i.e. repetitiveness) while sometimes does the opposite (i.e. jargons everywhere, almost ciphered talk). This is actually quite similar to how we talk, it's just that depending on the situations, we automatically adjust this to an optimal level. For example, we automatically rephrase our words into a new sentence (despite conveying the same information) when the other person is frowning or not responding. We also tend to do this in writing when there is a vocabulary that you suspect the target audience might not know. However, if we are trying to write a report, we will usually opt a concise and easy vocabulary (that you know both of you knows well) rather than rewriting the same sentence again as the next line. When I ask an LLM to deliver a report, it does not know what I know and what I don't know, and given that I asked for a report, the LLM just decides to write it in a slightly verbose way so that if I don't know part of it, I can gather enough prior context to understand this rather than asking specific parts again. This can also go the other way when the LLM uses many jargons that they assumed you know (e.g., they actually don't really know the abbreviations but they think they know it based on the context, and they also think that you know it by default given that it is being passed as part of an previous input and could probably correct them if you notice the issue). We usually don't want the LLM to ask more questions to us (the current trend is autonomous agents - i.e. "can I sleep while you 'read my mind' and decide on my behalfs"), so the definitive model becomes less inquisitive and more "I decide for you."

How to fix? It doesn't mean that we actually have to rewrite it ourselves. For a problematic model at the first place, I used the simple-english formatting instructions as the first line of defence (you can adjust the instructions accordingly). Then, next time we asking for natural language generation, we explicitly mention our target audiences' situations. For example, "my boss, who knows the pipeline but not this new service." Lastly, we can always make revisions on the output and let the model learn the diff and write it to somewhere persistent, e.g. my-boss.md contains the items on what my boss knows and don't know.

---

Related: https://github.com/AminBlg/SimpleEnglish
