# US case law: the United States Court of Appeals for the Federal Circuit

Part of [lexifina/global-law](https://github.com/lexifina/global-law), one git history for every country's law: this is the case law of the United States Court of Appeals for the Federal Circuit, United States, which global-law reads at `united-states/cafc/caselaw/`.

Every published opinion of the United States Court of Appeals for the Federal Circuit in the Caselaw Access Project, as a git history: one file per decision, one commit
per decision, dated the day it was decided. 24,191 decisions from 1982-10-28 to the end of the source.

## Questions as git commands

| Question | Command |
|---|---|
| A decision by its citation | `grep -P '^410 U.S. 113\t' decision-index.tsv` then `cat <path>` |
| Decisions given in a window | `git log --format='%(trailers:key=In-force,valueonly,separator=) %an' \| awk '$1 >= "1973-01-01" && $1 <= "1973-01-31"'`: read the `In-force:` trailer, not the commit date (see Corrections), or use the global-law tools |
| Decisions citing 11 U.S.C. § 1182 | `cat judgments/united-states/federal/usc/title-11/1182.jsonl` |
| The section as the court applied it | each overlay row's `law_commit` is the section's own version in the US Code record on the day decided (or `law_record_from` when the decision is older than the record) |
| Who wrote a line? | `git blame decisions/...`: each line is credited to the decision (court and citation) |

## Dates and authors
The commit date is the day the decision was given, at noon US Eastern (`In-force:` and `Decided:`). Git cannot hold dates
before 1970, so earlier decisions are committed on 1970-01-01, a second apart, and `In-force:` holds the real day. The
author is the court and the official citation, at an address that cannot exist. These are court rulings, not laws: every
commit is `Kind: court`.

## Source
The Caselaw Access Project's bulk data (Harvard Law School Library), dedicated to the public domain under CC0; court
opinions are not copyrightable (17 U.S.C. § 105; Georgia v. Public.Resource.Org, 2020). Each file keeps its source URL.
Text is CAP's OCR, unchanged.

## What it does not show
Opinions after the end of CAP's coverage (added from CourtListener where noted), unpublished decisions not in the
reporters, and statute citations to US Code titles the record does not hold.

## Added from the CAP bulk data (2026-11-08)
335 decisions this repo did not hold, from the Caselaw Access Project's bulk files (F. App'x, F.3d, F.2d, Fed. Cl., Vet. App., Cl. Ct., B.R., Am. Tribal Law, U.S.): every decision of
its courts in CAP that was not here by its CAP id, nor as the same case (day and name) read from another reporter. Each
was appended as its own commit, dated the day decided, after the decisions already here (the history is append-only, so
they are not in date order; the tools read each decision's own date). Their head matter, the publisher's text, is left
out. Now 33,589 decisions.

## Corrections (2026-11-09)
An independent check of the CAP case-law repos found data defects; they are fixed here by new commits on top of the
history (nothing is rewritten). Now 33,589 decisions.

- 18 files had no text: CAP holds no opinion text for them, only head matter. Each now gives the head matter under `## CAP head matter` (`text_source` in the front matter), in a `Kind: correction` commit on the same file (`Corrected:`, `Corrects:` the commit that added it).
- decision-index.tsv: 4,130 rows added (the citations and CAP ids of decisions held here under another reporter, and of the new decisions), 0 rows that gave a citation to a different decision removed.
- `decision-relations.tsv` lists 171 files as `same-decision-as` another file here: decisions the CAP append added although the same decision (same day, docket or name, and text) was already here. Both files are kept; the tools read the relation.
- `decision-dates.tsv` lists the 0 decisions whose CAP date gives only the month or the year (precision `month` or `year`); they are committed on the first day of it, and In-force says that day.

Dates in the commit history: git cannot hold dates before 1970, so a decision before 1970 is committed from 1970-01-01 noon UTC-5, a second apart.
Read the `In-force:` trailer for the day decided, not the commit date.

Head matter differs by when a decision came in: this repo's first build, from the Caselaw Access Project, includes each decision's head matter (syllabus, headnotes, counsel) in its file; the decisions appended later from the CAP bulk data leave it out (the publisher's text, not the court's), except where CAP has no opinion text, where the file gives the head matter under `## CAP head matter`. A text search over head-matter words therefore finds them only in the first build's decisions.

## Decisions moved to their own repos (2026-11-09)
8 decisions were here by a routing mistake (CAP gives them a jurisdiction their court name contradicts, or a court name the router did not read). Each is now in its own repo, and its file here is removed; `decision-relations.tsv` gives each removed path as `moved-to <repo>/<path>`. 8 to united-states-federal-special-caselaw. Now 33,581 decisions.
