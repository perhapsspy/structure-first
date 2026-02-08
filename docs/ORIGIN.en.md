# Structure First - Origin
> Note: This English text was translated and edited with LLM assistance. If anything reads awkwardly, please check the Korean version or open an issue.


This document records why `structure-first` was created, what failed along the way,
and how the final skill format was shaped.

[Korean Original](ORIGIN.md) | [English](ORIGIN.en.md)

## 1. Code Sense

I have worked across multiple domains and services, from solo build-and-run to team-level ownership.
Over time, I kept refining practical ways to keep code readable and change-safe.

Through pair programming and legacy cleanup, one pattern became clear:
readable flow, practical boundaries, and composable small units are what make delivery fast.
When code became easier to read, even a small team could sustain more features.

I mostly worked in Python, which helped speed, but Python code can become just as hard to read once many hands touch it.
So I repeatedly had to restore structure and intent.

## 2. Hard to Transfer

Helping junior developers grow was always meaningful but difficult.

Most of what I relied on was tacit judgment, not something easy to transfer quickly.
Even when 1:1 coaching worked well, that setup depended heavily on timing and team conditions.

## 3. AI Agent Experience

As AI-agent development became mainstream, productivity rose, but limits became visible.
The weakness was clearer in code with many states and branching situations.

During long sessions building complex frontend logic with AI, I could still reach outcomes,
but prompt trial-and-error kept increasing.
At some point, I often ended up accepting "tests pass" output instead of preserving code direction.

## 4. Why a Skill

One recurring question was: can AI help developers (especially juniors) build better coding habits?
That led to trying agentskills.io as a way to package the coding style I had used in product work.

I had years of GPT-based refactoring history, and many of those decisions were still recoverable.
When I reconstructed them with GPT, stable decision patterns became visible.
I already knew AGENTS.md notes alone would not make agents follow this consistently.

## 5. Structure First Experiment

So I shaped those decisions into a skill form that naturally guides toward core behavior.
Then I applied it directly to active projects.

> `$structure-first rethink the map feature we were building from scratch`

I also applied it to projects started by junior developers.

> `$structure-first propose the project structure again from a structure-first perspective`

The result was better than expected:
- code felt close to how I would structure it,
- top-level flow stayed readable,
- small units became testable with compact tests,
- AI handled complex state scenarios with fewer side effects.

This project is public to validate that `structure-first` helps both humans and AI produce readable, lower-risk code.

## 6. About the Skill Content

The skill is not about inventing new theory.
It packages repeated practical decisions observed while shipping product code.

Some ideas will feel familiar:
- boundary thinking may resemble clean/layered architecture,
- ordering rhythm may feel close to tidy-first,
- tests may look like TDD, but here they act primarily as contract checks.

The hard part was not principles themselves, but deciding practical stop points in real projects.
This skill is the most practical version of those repeated decisions.
