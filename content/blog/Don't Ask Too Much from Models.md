---
title: "Don't Ask Too Much from Models"
date: 2025-07-29
tags: ["slice-of-life"]
---

I enjoy using models to assist with my projects, whether it's to find the best tech stack to kick off a hobby project or to generate a piece of code. However, we should only let them help to an extent.

My CTO _loves_ vibe coding with Replit. I totally get it, Replit fits their needs perfectly - being able to generate a working app based on a single natural language paragraph is how you can quickly scaffold an idea to a working prototype and pitch it to clients (, or to generate progress slop if you realize you need to at least deliver _some thing_ to your client's meeting-in-15-minutes.)

We never coded like that before, therefore we don't really realize the problems of using these until too late.

## You are not prepared at all
When you are writing (or, in my CTO's case, using faster-whisper STT to transcribe their spoken English) into the prompt, you don't really know the details on what you are trying to build.

You don't know whether we should go TypeScript or Python until you realize two weeks later that a package you want is exclusively in the other package manager. And it is already impossible to refactor the whole project into the other language while promising the same cadence of progress to the client. Your client does NOT care whether it's in TS or Py. They _paid_ you for _progress_. You buy McDonalds with the expectation of enjoying some fast food in 5 minutes - you don't care how they do it. "Our fryer exploded and we are now heating up the oil in the new fryer as fast as we can" is a valid response, but your client will just do a refund and find the next McDonalds. You have a nightmare that night while praying them not giving your store a 1.0 on Yelp.

We are not even mentioning that you need to spend your saved time back to audit the generated code if you want to have an easier time debugging.

## The prototype is rushed
Carefully structuring the base is as, if not more, important than building new features onto it.

A valid project needs us to think of everything _before_ we `git init`. How many miles do you want this engine to last before any component gives? You will have a hard time baking a cake on top of a plastic cup, and replacing the base means wasting hours of work on building that plastic cup. Planning ahead saves you time in the long run, but since most ideas are sprints, people don't really care as much. "Just keep strengthening the cake structure every time you put more things on it."

## Models are too Obedient
Models are increasingly obedient.

The model never asks. If I tell them to write a 384D vector database in Verilog, they do it immediately. That's not how we should build things, but I guess investors prefer these than the other model who directly refutes the absurdness and suggests another language.

Obedience feels like intelligence. Pushback feels like error.

"Sure!" "You're right!"


## It applies universally
Would you like an engineer that says "Sure!" and works right away, or one that says "We might be better off using Python. You sure want Verilog?"

I can either code the vector database in Verilog today and make my CTO very happy with me, or question their move while waiting till 4pm for a reply and work overtime to keep our progress within expectations to the client.

It's just how we are trying to survive right now. People don't want pushbacks and they upvote instant results. The "better" is already determined.