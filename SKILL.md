---
name: learning-planner
description: >
  Turns "I want to learn X" into a consistent self-study plan for any hands-on
  technical skill (Kubernetes, Terraform, Docker, CI/CD, cloud, databases,
  programming languages) built on a fixed daily time slot and a pre-planned week
  of specific, testable build outcomes instead of video watching and crash
  courses. Use this skill whenever the user wants to learn, practice, or master
  a technology themselves — asks for a study plan, learning roadmap, or "how
  should I learn X", mentions a topic they keep starting and abandoning,
  complains that tutorials or courses "don't stick" or that they can't stay
  consistent, has spent hours on content with nothing to show for it, or wants
  practical skills rather than theory — even when they never say the words
  "plan", "schedule", or "system". Don't use it when the user is arranging
  learning for other people (workshops, onboarding programs, mentoring advice),
  setting up flashcard or study-tool software, or wants a one-off explanation,
  command, or config file.
---

# Learning Planner

The deliverable is a plan, not a lesson. Do not teach the topic itself. Produce
a schedule the user can execute without making decisions: a fixed daily slot, a
multi-week cumulative arc, and Monday-through-Friday task cards where each day
ends with a real artifact they can point at and say "this works".

## Why this method (keep this in mind when adapting)

Sporadic consumption fails for cumulative skills because context decays fast:
a few days off means re-learning yesterday's basics before touching today's.
Total hours matter far less than daily repetition, so the system is designed to
make motivation irrelevant — the user should never have to decide *whether*,
*when*, or *what* to study. Deep technical skill comes from artifacts that
break and get debugged, which only happens when the hands are on the keyboard
every day. Every design choice below serves that: fixed time kills decision
paralysis, testable outcomes kill "I kind of learned it", and daily commits
turn the learning into reference material and job-search proof.

## Gather only what's missing

The user's message usually answers most of this already. Ask (at most one or
two questions, in one message) only if genuinely unknown:

- **Topic** — one skill, learned for 2–4 weeks. If they name several, help them
  pick one and note what comes next.
- **Current level** — zero / some theory / has built things before. Changes
  where week 1 starts, not the structure.
- **Slot** — a specific daily time and length. If they give a window ("evenings,
  ~45 min"), pick a concrete slot inside it and recommend earlier-in-the-day if
  they're flexible, since a fresh mind beats a drained one. Default to 30 min.
- **Horizon** — 2–4 weeks. If they ask only for week 1, still show the full arc
  so each week visibly builds on the last.

## The rules that make a plan work

**Fixed slot, same time daily.** Name it explicitly ("Mon–Fri, 07:00–07:30"),
frame it with standup-level priority, and tell them to block the calendar.
If the user's reality doesn't fit Mon–Fri, adapt the days — never the cadence.

**Prep lives outside the slot.** Installs, account setup, and tool wrangling
that are not the skill itself belong in a one-time "Before day 1" block (the
night before, or a weekend hour), listed as its own short section — not in
slot days. Nothing should eat the first morning's momentum on a package
install, and nothing that isn't the target skill should consume the 25 minutes.

**Provide the raw materials inside the plan.** If the plan needs a sample app,
a Dockerfile, seed data, or manifests for the adjacent work, write them into
the plan itself (an appendix or a setup section) instead of telling the user to
"pick an app" or "find a dataset". Sessions should spend their minutes on the
skill being learned; scaffolding the adjacent domain focuses the effort where
it counts and removes one more daily decision. A Kubernetes learner should be
typing `kubectl`, not writing Flask; a SQL learner should be querying, not
hunting for a CSV.

**Each day is one artifact, verifiable in one sit-down.** A task is only good
if a stranger could check it in 10 seconds: the image runs in a browser, the
pipeline goes green, the pod survives a restart with data intact. Size it to
about 25 minutes of hands-on work — slightly under what fits the slot, because
flow and debugging eat time.

**Each day builds on yesterday's artifact.** Tuesday reuses Monday's image,
Wednesday pushes it to a registry, Thursday deploys it. This chain is the whole
point: it keeps yesterday's context alive and makes skipping visible. When
planning, sketch the chain first, then write the cards.

**Schedule the breaking, not just the building.** Real engineering time goes
into diagnosis, and a plan that only builds never teaches recovery. Build
chained success and then deliberately sabotage it: end a week with a card that
plants bugs in the user's *own* working artifact (a mismatched selector, a wrong
port, a budget-inflating join, a broken probe) and fixes it using only the
tool's own inspection commands. The prior days' notes become the debugging
reference, which is exactly why they were written. Readers consistently rate
these cards the most valuable part of a plan.

**Prefer the operations practitioners actually do.** When choosing what a day
builds, reach past the toy version toward the awkward real-world step: importing
something that already exists rather than only creating fresh, refactoring live
state without recreating it, tightening an overly-open rule after it worked,
pre-aggregating before joining. These operations are where competence and
interview stories both come from, and they cost nothing extra to schedule.

**Outcome verbs are physical.** If the outcome reads "understand", "learn",
"study", "get familiar with", or "basics of", rewrite it as *build something +
verify something*. "Understand Docker networking" is a feeling; "run two
containers on a custom network and curl between them by container name" is a
plan.

**Session shape: ~3 min retrieval + build + ~5 min document, every session.**
It opens by redoing yesterday's core action from memory — retype the query,
re-run the command sequence, no notes. Failing at it is the exercise: the gap
between what you type and what yesterday proved is what needs relearning, and
this is the single mechanism that makes short daily sessions accumulate instead
of evaporate. It closes with documentation — not homework but the reference the
user will thank themselves for in three weeks, and interview evidence ("here
are 30 days of infrastructure I wrote"). Tell them what to capture: files
committed, what broke, how they diagnosed it, the exact commands. Build gets
whatever minutes the slot has left.

**Capstone.** The final day deletes or resets everything and rebuilds from only
the user's own repo and notes, timed, with one deliberate breakage to fix.
It's the difference between "I went through the lessons" and "it works or it
doesn't" — and the before/after is the thing to show in an interview.

**When the user's runway is longer than the plan, say what the extra time is
for.** If they have six weeks but you're planning two, the remaining weeks get
one honest paragraph naming their different job — consolidation rhythm: timed
rebuilds from memory, re-running the capstone cold, converting notes into
interview stories — not a thinner copy of the planned weeks. An under-detailed
stretch reads as an afterthought; a differently-purpose stretch reads as design.

## Output format

Use this structure:

```markdown
# Learning plan: <topic>

**Slot:** <days>, <HH:MM–HH:MM> (<N> min, same time daily — block it in your
calendar now).
**Horizon:** <N> weeks. By the end you will <capstone: one concrete thing you
can build and troubleshoot from scratch>.

## Before day 1 (<N> min, the night before or a weekend hour — not in a slot)
- <installs, account/CLI access, repo creation — everything that is not the
  skill itself>

## Curriculum arc
- Week 1 — <theme>: <what exists at the end of the week>
- Week 2 — <theme>: <builds on week 1>
...
Each week ends with a break-it-and-fix-it card; the arc ends with the capstone.

## Week <N> — <theme>
### Monday
- **Build:** <one specific artifact/task>
- **Verify:** <binary check — it works or it doesn't>
- **Doc (5 min):** commit <files> to week<N>/monday/; note what broke and how you fixed it
### Tuesday
...

## Doc repo
Create `<learning-|devops-learning-><topic>` on GitHub/GitLab now:
- one folder per week (`week1/`), one subfolder or file per day
- per-session note: what I built / what broke / how I fixed it / commands used
- commit after every session — screenshots and failing attempts included;
  the failures are the valuable part

## How to run a day
At the slot, open today's card — no deciding, no resource-hunting. First ~3 min:
redo yesterday's core action from memory, no notes (failing at it is the point).
Then build, 5 min doc, commit, stop. If it breaks and you can't fix it inside
the slot, that debugging *is* the session: write it up, and tomorrow opens with
a few minutes on yesterday's mess before touching today's card.

## Appendix: materials
<the sample app / Dockerfile / seed data / starter manifests the plan leans on,
inlined so no session spends its minutes on anything but the skill>
```

## Sizing examples

**Bad:** "Monday: understand Kubernetes pods" — unmeasurable, no artifact.
**Good:** "Monday: create the 2-node kind cluster from your `kind-config.yaml`,
run an nginx pod from a manifest, confirm `kubectl get pods` shows it Running
and `curl` to port-forwarded :8080 returns nginx's welcome page." (Installs
belong in the "Before day 1" block, not in Monday's 25 minutes.)

**Bad:** "Tuesday: learn about services" — vague, and it doesn't use Monday.
**Good:** "Tuesday: expose Monday's nginx pod with a Service, verify a second
pod can reach it by DNS name `nginx-svc` — then delete the pod and verify the
service still routes to its replacement."

## Adapting, without breaking the method

- More time available (45–60 min): scale task ambition, keep the daily cadence
  and the 5-minute doc step; do not stack two topics into one session.
- Experienced learner: week 1 can start mid-topic, but keep the chain — day 1
  still produces an artifact day 2 depends on.
- Non-DevOps topics (a language, a database): the artifact just changes shape —
  a running script, a query plan, a small API. The rules are identical.
- A topic that needs paid infrastructure: default to free/local options
  (kind, minikube, Terraform with the free tier or local stack) and say so in
  the plan.

When the user comes back mid-week ("what's today?") or wants the next week,
regenerate from this plan's chain rather than inventing something new.
