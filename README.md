# Resource Hero Billable Utilization Reports

Two Salesforce reports that split [Resource Hero](https://resourcehero.com) actual
utilization into billable and non-billable time, per resource and per month, against
the same full capacity. A 100% month then explains itself: client work, time off, a
holiday, or internal projects.

The full walkthrough, with screenshots and the click-by-click build, is in the solution post:
[Split Utilization into Billable and Non-Billable Time](https://www.resourceheroapp.com/solutions/billable-vs-non-billable-utilization/).

Built as a community pattern in response to a customer request. It is not part
of the Resource Hero managed package and is not covered by Resource Hero
support. Use it, fork it, change it.

## What you get

| Report | Columns per resource and month | Colored by |
|---|---|---|
| Utilization - Billable vs Non-Billable | Capacity, Non-Billable %, Billable %, Total % | Total %: green under 80%, yellow 80 to 100%, red over 100% |
| Utilization - Billable Only | Capacity, Billable Hours, Billable % | Billable % against an 80% target: red under 60%, yellow 60 to 80%, green 80% and over |

Both reports are grouped by resource and by calendar month of Forecast Date, and
filtered to the last six months. They show actuals only.

Non-billable utilization covers approved time off, holidays, and hours on
non-billable work. Billable utilization covers hours where **Is Billable** is
checked. Total utilization is the two added together.

## What gets deployed

| Component | Purpose |
|---|---|
| `RH Billable Utilization` (report folder) | Holds the two reports. Public, read-only. |
| `Utilization_Billable_vs_Non_Billable` (report) | The three utilization lines per resource and month |
| `Utilization_Billable_Only` (report) | Billable hours and billable utilization against a target |

No fields, flows, or code. The reports use the report type and fields that ship
with Resource Hero.

## Prerequisites

- Resource Hero installed (namespace `ResourceHeroApp`).
- Permission to deploy metadata and manage public reports.

## Install

**With the Salesforce CLI** (recommended):

```bash
git clone https://github.com/Resource-Hero/rh-solution-billable-utilization.git
cd rh-solution-billable-utilization
sf project deploy start --source-dir force-app --target-org <your-org-alias>
```

**With a coding agent.** Tools like Claude Code and Agentforce Vibes, with
Salesforce skills loaded, can read this repo and help you deploy it or rebuild
the same reports in your own org. Point the agent at the repo, tell it which
org you want it in, and review what it proposes before approving each step.

After deployment, open the **Reports** tab and select **All Folders** →
**RH Billable Utilization**.

## Set your own target

The colors on **Utilization - Billable Only** assume an 80% billable target.
To change it, edit the report, click **Conditional Formatting**, edit the
**Billable %** rule, and enter your own range values.

Capacity stays at its full value in both reports, so time off counts against
billable utilization. A month with a week of vacation tops out near 75%
billable. Set targets with that in mind.

## Things to know

- **Hours follow the checkbox.** A time entry counts as billable when **Is Billable** is checked on it.
- **Report totals cover named resources.** Hours on an assignment that has a role but no resource do not belong to any resource row.
- **The same formulas work by role or team.** Swap the resource row group and nothing else changes.

## Removing it

Delete the two reports, then the report folder.

## License

MIT. See [LICENSE](LICENSE).
