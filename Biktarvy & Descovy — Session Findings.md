# Biktarvy & Descovy — Session Findings

Sep 30, 2026 · @Antonis

## Scope and bottom line

The pull script is checked and patched; the only blocker is that no sandbox tried so far can reach the federal APIs.

- **Covers:** this session's work on Biktarvy and Descovy (labeler 61958). It complements the Public Data Reference doc and does not repeat its source catalog.
- **Established:** 61958-2601 is not a real product; all seven CMS dataset titles resolve in the v1.1 catalog; the Part D growth figures recompute exactly; the Part D double count is fixed in the script.
- **New from CMS guidance:** the negotiated price file drops NDC-11 package prices, and fixed-dose combinations stay separate drugs for 2028.
- **Blocked:** three sandboxes (this one, another Claude session, a ChatGPT sandbox) deny outbound traffic to api.fda.gov, data.cms.gov, data.medicaid.gov and rxnav.nlm.nih.gov. The script needs one run on a machine with open internet.

## Code map check

Three of the four product codes in the original brief are right; 61958-2601 matches no product, and pediatric Biktarvy is 61958-2505 / 2506.

| Code in brief | Product | Status |
| --- | --- | --- |
| 61958-2501 (50/200/25 mg) | [Biktarvy](https://ndclist.com/ndc/61958-2501) | Confirmed |
| 61958-2601 (30/120/15 mg) | none | Not found in any FDA, CMS or label source; pediatric Biktarvy is 61958-2505 and 61958-2506 |
| 61958-2002 (200/25 mg) | Descovy | Confirmed |
| 61958-2005 (120/15 mg) | [Descovy low-dose](https://fda.report/NDC/61958-2005) | Confirmed |

- The pediatric bottle row in the brief was missing its package suffix; it is 61958-2505-01 (billing NDC-11 61958250501).
- Full package list with marketing dates is in the Public Data Reference doc.

## Verified figures

Every Biktarvy Part D growth rate recomputes exactly from the 2020 and 2024 rows; the 2024 per-tablet dip is real in the data.

### Part D arithmetic (Overall row, 2020 to 2024)

| Measure | 2020 | 2024 | Growth per year (recomputed) |
| --- | --- | --- | --- |
| Gross spend | $1.776B | $3.456B | 18.1% |
| Claims | 500,405 | 840,772 | 13.9% |
| Beneficiaries | 55,805 | 92,246 | 13.4% |
| Spend per tablet | $111.16 | $131.33 | 4.3% |

- 2024 vs 2023: spend +9.6%, spend per tablet −1.3% ($133.13 to $131.33).
- $3.456B for calendar 2024 against $3.904B for Nov 2024–Oct 2025 fits the 18% trend; the two windows and scopes differ, so they are not directly comparable.

### Negotiation cycle (IPAY 2028)

- CMS named 15 drugs on 27 Jan 2026 from spend between 1 Nov 2024 and 31 Oct 2025; together $27B, about 6% of Medicare drug spend ([Avalere](https://advisory.avalerehealth.com/insights/cms-announces-the-third-round-of-medicare-drug-price-negotiation)).
- First cycle with Part B drugs; Tradjenta was added for renegotiation. Manufacturers signed agreements by 28 Feb 2026.
- Biktarvy rank #2 at $3,904,486,000 and the Doptelet cutoff at $236,862,000 come from the [CMS top-50 fact sheet](https://www.cms.gov/files/document/factsheet-medicare-top-50-negotiation-eligible-drug-list-ipay-2028.pdf), read by the other session; the Avalere copy shows its table only as an image.

### Final guidance: what changes for this deck

From the [IPAY 2028 final guidance](https://www.cms.gov/priorities/medicare-prescription-drug-affordability/overview/medicare-drug-price-negotiation-program/guidance-and-policy-documents) summary of changes (30 Sep 2025, first 5 of about 390 pages):

| Change | Effect on the Biktarvy / Descovy work |
| --- | --- |
| NDC-11 package price removed from the MFP file | Biktarvy's negotiated price must be mapped to the nine NDC-11s by hand |
| Fixed-combination drug policy unchanged for 2028 | Biktarvy's selection does not extend to Descovy; CMS flags it as a program-integrity risk for 2029 rulemaking |
| WAC of therapeutic alternatives added as a possible starting point | Keeps WAC (Vermont disclosure, California HCAI) relevant to the negotiation story |
| Manufacturers submit ASP for the last two quarters of 2025 | ASP is an input to the price; supports keeping the ASP pull |
| MA encounter data now counts in Part B totals | Part B spend used for selection is broader than the public Part B Spending file |

## CMS catalog check

All seven dataset titles the script looks up match the uploaded v1.1 catalog (159 datasets), so title matching will not fail on first run.

| Dataset title | Release the script picks | Modified |
| --- | --- | --- |
| Medicare Quarterly Part D Spending by Drug | 2026-01-01 to 2026-03-31 | 2026-07-23 |
| Medicare Quarterly Part B Spending by Drug | 2026-01-01 to 2026-03-31 | 2026-07-23 |
| Medicare Part D Spending by Drug | 2024 | 2026-06-25 |
| Medicare Part B Spending by Drug | 2024 | 2026-06-25 |
| Medicaid Spending by Drug | 2024 | 2026-06-25 |
| Medicare Part D Prescribers - by Geography and Drug | 2024 | 2026-05-21 |
| Medicare Part D Prescribers - by Provider and Drug | 2024 | 2026-05-21 |

- The uploaded catalog identifies itself as `data.cms.gov/v1-1-data.json`, which supports pointing the script there instead of `data.json` (now DCAT-US v3).
- A quarterly release carries several `Year` labels; a live Part B pull showed `2025 (Q1-Q4)` inside the Q1 2026 release. Filter to one label before charting.

## Script review: hiv\_public\_pull.py

The script is sound; one real bug (the Part D double count) was fixed and tested offline, and it has not yet run against live APIs.

| Finding | Severity | Status |
| --- | --- | --- |
| Part D Spending repeats each brand as `Overall` + manufacturer rows; the long sheet kept both, doubling spend | High | Fixed: long sheet keeps `Overall` only; tested offline, 2020–2024 sums match $1.776B–$3.456B once |
| Part D by Geography mixes the National row with state rows | Medium | Fixed: new `partd_geo_state` sheet, State rows only |
| Quarterly releases hold several `Year` labels | Medium | Documented on the README sheet; no automatic filter |
| An unreachable host retries 5 times with backoff on every call | Low | Fixed in the other agent's copy (startup reachability check) |
| Catalog read from `data.json`, now DCAT-US v3 | Medium | Fixed in the other agent's copy (`v1-1-data.json`) |
| Warnings raised while writing the workbook miss the README sheet | Low | Fixed in the other agent's copy |

- **Copy to keep:** the other agent's version; it carries all fixes above. Mine lacks the last three.
- **Dry-run evidence:** with networks blocked, that copy still wrote a workbook with README, provenance, NDC master and negotiation sheets, and listed every skipped host.

## Environment and repo state

Nothing was committed to API-papi; the repo is still docs only, and the script lives only in uploads and chat.

| Item | Finding |
| --- | --- |
| Network, this session | Egress policy denies api.fda.gov, rxnav.nlm.nih.gov, dailymed.nlm.nih.gov, data.medicaid.gov, data.cms.gov, data.chhs.ca.gov and www.cms.gov; web fetch is blocked the same way |
| GitHub Actions route | Adding a workflow to run the pull on a GitHub runner was refused by the permission system; needs your explicit approval |
| Branch name | `claude/hello-94ugab` cannot be created: a `claude` branch already exists locally and on GitHub, and git cannot hold both |
| Script in repo | Not present; the other Claude session found no file containing "hiv" for this reason |
| NDC-Mapping zips (\_2, \_3) | Byte-identical; scripts are ASCII-clean and pass syntax checks; workflow file name starts with a space |

## Open items

One live run unblocks the deck; pick one route to it.

- [ ] Choose a run route: laptop (fastest), approve the GitHub Actions workflow, or open this environment's network and start a new session.
- [ ] Before running in any new sandbox, test one URL: `curl -s -o /dev/null -w "%{http_code}" "https://data.cms.gov/data-api/v1/dataset/7e0b4365-fd63-4a29-8f5e-e0ac9f66a81b/data?size=1"`; anything but 200 means blocked.
- [ ] Run the other agent's copy of `hiv_public_pull.py` and send back the workbook.
- [ ] Check provenance row counts; confirm `partd_spending_qtr` has rows.
- [ ] Decide where the script lives in git: push to `claude`, or a new branch such as `hiv-pull`.
- [ ] After 30 Nov 2026, map Biktarvy's negotiated price to its NDC-11s by hand.

## Sources

- [Avalere: CMS announces the third round of Medicare drug price negotiation](https://advisory.avalerehealth.com/insights/cms-announces-the-third-round-of-medicare-drug-price-negotiation) (uploaded PDF, 29 Jan 2026)
- [CMS IPAY 2028 final guidance](https://www.cms.gov/priorities/medicare-prescription-drug-affordability/overview/medicare-drug-price-negotiation-program/guidance-and-policy-documents) (uploaded pages 1–5)
- [CMS top-50 negotiation-eligible drugs, IPAY 2028](https://www.cms.gov/files/document/factsheet-medicare-top-50-negotiation-eligible-drug-list-ipay-2028.pdf) (figures via the other session)
- [CMS selected drugs, IPAY 2028](https://www.cms.gov/files/document/factsheet-medicare-negotiation-selected-drug-list-ipay-2028.pdf)
- [data.cms.gov v1.1 catalog](https://data.cms.gov/v1-1-data.json) (uploaded copy)
- [Medicare Part D Spending by Drug API (7e0b4365)](https://data.cms.gov/data-api/v1/dataset/7e0b4365-fd63-4a29-8f5e-e0ac9f66a81b/data)
- [NDC 61958-2501 Biktarvy (ndclist)](https://ndclist.com/ndc/61958-2501)
- [NDC 61958-2005 Descovy (fda.report)](https://fda.report/NDC/61958-2005)
- [Descovy label (DailyMed)](https://dailymed.nlm.nih.gov/dailymed/drugInfo.cfm?setid=06f66e98-e6ee-4538-9506-6c1282cc14c1)
