# Ricky P.

**I map how work gets done, build the AI-powered system that does it, and measure what changed.**

Five years in healthcare revenue cycle as a business analyst and then Manager, Product Line Management, then four years running
my own data-driven real estate operation, where I design and operate the automation platform the team
works from: sixteen workstreams running as 17 scheduled and on-demand workflows (**measured**, counted from
the production repo 2026-09-16; the platform README's 16 is the 2026-09-25 recount after a CI check was
folded into another workflow). I set the requirements and business rules, build with AI tools, test
each piece, and keep a person in the loop wherever the system could be wrong.

Everything here is a reference implementation on synthetic data, with one exception: the Ops Heartbeat is
the real code, generalized. The production repository remains private and contains 1,069 commits dating back to April 11, 2026
(**measured**, counted 2026-10-15). The contribution graph below also counts the pull requests behind those
commits and a few smaller private repos. This public repository is a sanitized reference implementation of
that operational work. Every outcome or impact claim carries a tag: **measured**, **goal**, **recollection**, or **finding**.

## Three stories

### Automate — redesign the work
**[County records pipeline](https://github.com/rp1906-bit/operations-automation-platform/blob/main/docs/county-pipeline.md)**
A scheduled job that watches a county's public-records portal, reads each scanned filing, normalizes and
de-duplicates the rows, checks them against a second source, and writes clean rows to the sheet the team
works from. At each point where it can be wrong, it is built to stop and hand the row to a person
instead of guessing.
Replaced a manual pull I used to do by hand.

### Validate — make the process trustworthy
**[QA Verifier](https://github.com/rp1906-bit/operations-automation-platform/blob/main/docs/qa-verifier.md)**
and **[Ops Heartbeat](https://github.com/rp1906-bit/operations-automation-platform/blob/main/docs/ops-heartbeat.md)**
The Verifier grades every data pull by the rows it wrote, not the exit code it returned, names the likely
cause with a confidence level, and decides whether a pre-vetted repair is eligible under defined safety
gates. Everything else it drafts for approval or escalates to a person in Slack. The Heartbeat watches the whole fleet from outside all
of it, so a job that never started still produces an alert. Its first live run found four reliability
problems nobody knew about, two in jobs that had never worked (**measured**).

### Improve — turn results into decisions
**[KPI engine and diagnostic](https://github.com/rp1906-bit/operations-automation-platform/blob/main/docs/kpi-engine.md)**
Nightly activity pulls with proof of delivery, and a weekly stoplight report that colors each metric
against agreed bands and walks a fixed diagnostic order before it ever names a person. It separates
"no data" from "bad result", which is the difference between a report people trust and one they argue with.
Its write-up carries one full cycle: a productivity decline, the diagnosis, the operating rule that
changed, the metric that moved, and the confounder that was recorded with it.

## Repos

| Repo | What it shows |
|---|---|
| [operations-automation-platform](https://github.com/rp1906-bit/operations-automation-platform) | The three stories above, a workflow inventory, and two supporting analyses (build vs. buy, build velocity). 118 tests. |

It runs offline from a fresh clone: `pip install -r requirements.txt && python -m pytest -q`, then one demo command.

## How I work
I start with the work as it's actually done: who touches it, where it breaks, and what a correct result
looks like. I write the rules and the acceptance criteria before anything is built, and every rule gets a
test. Once it runs, a separate check grades the output, and a watcher outside the system tells me when it
didn't run at all. Then I measure what changed and write down what the numbers don't support. The code is
written with Claude Code; the requirements, the tests, the ship decisions and the operation are mine.
