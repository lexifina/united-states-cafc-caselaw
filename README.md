# US case law: the United States Court of Appeals for the Federal Circuit

Part of [lexifina/global-law](https://github.com/lexifina/global-law), one git history for every country's law: this is the case law of the United States Court of Appeals for the Federal Circuit, United States, which global-law reads at `united-states/cafc/caselaw/`.

Every published opinion of the United States Court of Appeals for the Federal Circuit in the Caselaw Access Project, as a git history: one file per decision, one commit
per decision, dated the day it was decided. 24,191 decisions from 1982-10-28 to the end of the source.

## Questions as git commands

| Question | Command |
|---|---|
| A decision by its citation | `grep -P '^410 U.S. 113\t' decision-index.tsv` then `cat <path>` |
| Decisions given in a window | `git log --since=1973-01-01 --until=1973-01-31 --format='%ad %an' --date=short` |
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
