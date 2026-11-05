# User outputs: "decision needed" and closing summary

Two short files the user actually reads. Both are written by the orchestrator (or by the judge for its own escalations, as a proposed section) in the user-facing language from STATE.md. Headings below are given in Bosnian (ijekavica) and English; use the user's language. Keep IDs as they are.

Rules for both:
- **One page.** If it does not fit on one screen, it is too long: link to the detail files instead of repeating them.
- **No new analysis here.** Every number is a reference to its owning section or U-item, or copied from it at its stated precision.
- **Concrete asks.** Each ask names what the user must give (a choice, a number, a document, a contact, an approval) and what it unblocks.

## `.product/decision-needed.md`

Written when the run stops because progress depends on the user (hard stop in Phase 3, a judge `escalate-to-user`, or open blocking U-items at the end).

```markdown
# Odluka potrebna / Decision needed
Stanje: <one line: what is ready, what is waiting>   ·   Datum: <YYYY-MM-DD>

## Da bismo nastavili, trebamo od tebe / To proceed we need from you
1. **<U-03> <question in one line>**: izaberi A / B (/ C).
2. **<U-05> <question>**: <a number / a document / a contact / an approval>.
3. ...
(Maximum 5. Ordered by what unblocks the most.)

## <U-03>: <short title>
| Opcija | Trošak | Rok | Rizik | Šta se mijenja u planu |
|---|---|---|---|---|
| A: <...> | <range> | <range> | <one line> | <owning sections + one line> |
| B: <...> | ... | ... | ... | ... |
**Preporuka:** <A>, jer <one sentence with the evidence reference>.
**Ako ne odlučiš:** ništa se ne pokreće što zavisi od ove odluke; <what stays blocked>.

(repeat the block for each ask, keep each to ~6 lines)

## Šta radimo čim odgovoriš / What happens once you answer
<one targeted revision of <sections>, verify, consistency sync, handoff of N prompts — expected agent calls: ~n>
```

When the AskUserQuestion tool is available, also ask each blocking item there, with the options as choices, the recommendation first and labelled as recommended, and "nastavi s preporukom" / "proceed with the recommendation" as an explicit option. Only an explicit answer counts.

## `.product/SUMMARY.md`

Written at the end of every run (done, waiting-on-user or not-ready) and refreshed after the post-decision path.

```markdown
# Sažetak / Summary: <project>
Status: spremno za DEV | čeka tvoju odluku | nije spremno   ·   Datum: <YYYY-MM-DD>

## Šta je spremno / What is ready
- MVP: <3–5 lines, with → product.md §6>
- Plan: <duration range and budget range as references to their owning sections>
- Za DEV: <N prompts, M blocked> → handoff/README.md   (or "not yet: waiting on U-xx")

## Šta treba od tebe / What we need from you
- <U-03>: <one line> → decision-needed.md
- <anything else only the user can give: access, contacts, content, approvals>
(or "ništa / nothing")

## Šta se mijenja ako odlučiš A ili B / What changes if you choose A or B
| Odluka | Ako A | Ako B |
|---|---|---|
| U-03 <short> | <duration / cost / scope effect> | <...> |

## Poznati nedostaci / Known gaps
- <items still not met after the judge's verify or the consistency fix, each with owner and what closes it>
(or "nema / none")

## Kako smo došli dovde / How we got here
Krugova revizije: <n>/2 · sudija: <yes/no> · mehaničkih ispravki: <n> (→ reviews/sync-log.md) · otvoreni nalazi: <n critical / n significant / n minor>
```
