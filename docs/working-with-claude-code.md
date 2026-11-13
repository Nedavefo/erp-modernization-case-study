# Working with Claude Code

This is how I use Claude Code on the ERP modernization project. The speed comes from how I direct it, not from accepting whatever it produces.

## 1. Spec first

Before any code, I write down the goal, the data involved and what "done" looks like. For a legacy screen that means: which table it reads, which filters it applies, how it calculates, and a few real numbers to compare against. Claude Code then works against a clear target instead of guessing.

## 2. Small steps

One model, one screen, one migration at a time, each ending in a commit that works. When something is wrong, the change that caused it is small and easy to find or roll back.

## 3. Delegate the repetitive, keep the decisions

Boilerplate, data migrations, test scaffolding, refactors and documentation go to the agent. I keep the design choices, the naming, what to build next and what to leave out.

## 4. Verify everything

- I read every diff before it is committed.
- Tests come with each module (about 150 so far), and I run them.
- Behaviour is compared with the system being replaced, on real data, using a command I can rerun.
- Anything I cannot explain does not ship.

## 5. Document as I go

The repository keeps a record of what was compared and what differs on purpose, an equivalence map from the old menus to the new screens, and a production guide with a checklist. This is the part that keeps the project understandable weeks later.

## What I changed along the way

- Moved from "build the screen" to "read the old source first": the labels in the old menus turned out to be unreliable, so every screen is now checked against the legacy code and its data.
- Kept the commit history readable: one working module per commit.

## An example of the kind of instruction I give

This is an illustration of the style, not a transcript.

> Read the old form for "units sold report" and tell me which table it queries and how it filters. Do not change anything yet. Then compare its result for October with the new report, and list every difference.

Asking for the analysis and the comparison before the change is what catches wrong assumptions early.
