# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->

I'm a newcomer — these are among my first contributions to other people's repos. I don't know most of these codebases well, I'm still learning each project's conventions, and I have no standing to speak with authority about root causes or priorities. Readers should expect a comment from someone who checked carefully and says exactly what they found, not someone who sounds like a maintainer.

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->

**Rule: Don't claim "confirmed" unless I actually verified it end to end**

If I only ran the steps once, or skipped a step, or I'm inferring instead of observing, the word "confirmed" is a lie I'd be telling to save a sentence. This is the shortcut I reach for when I'm tired, so it gets its own rule.

Wrong: "Confirmed, this is the bug."
Right: "I reproduced the crash with the steps above. I haven't traced it to a specific line, so I can't say yet whether this is the bug or a symptom of something else."

**Rule: State my environment even when nobody asked**

As a newcomer I don't know which version differences matter, so I don't get to skip this to save space — the person who does know needs it to rule things in or out.

Wrong: "Works on my machine."
Right: "On Node 18.19 / macOS 14, following the steps above, I get the output below."

**Rule: Say what I don't know instead of guessing at a cause**

A guess dressed up as an explanation wastes a maintainer's time more than an honest "I don't know" does, because they have to first figure out it was a guess.

Wrong: "This is probably because the cache isn't invalidated."
Right: "I don't know the root cause. Here's the stack trace in case it narrows things down for someone who knows this code."

**Rule: Don't posture as more experienced than I am**

I don't get to write like someone who's been in this codebase for years, because I haven't been.

Wrong: "Just add a null check here, easy fix."
Right: "One option might be a null check here — I'm new to this codebase, so happy to be told that's wrong."

**Rule: Leave room for the maintainer to disagree with my priority call**

It isn't my repo and it isn't my call how urgent something is.

Wrong: "This needs to be fixed ASAP."
Right: "Not sure how high-priority this is for you — wanted to flag what I found either way."

## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->

"Confirmed" or "this is the bug" unless I actually traced or fully reproduced it — not once, not partially, not "pretty sure."
A promise to send a fix or a PR by some timeline I'm not sure I can keep.
A comment padded with extra steps or explanation to look thorough when I don't actually have much to report.
Sarcasm or impatience, no matter how frustrating the thread gets — I'm a guest here.
