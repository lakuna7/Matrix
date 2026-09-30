# Biktarvy & Descovy — Session Findings

Sep 30, 2026 · @Antonis

## Scope and bottom line

The pull script is checked and patched; the only blocker is that no sandbox tried so far can reach the federal APIs.

- **Covers:** this session's work on Biktarvy and Descovy (labeler 61958). It complements the Public Data Reference doc and does not repeat its source catalog.
- **Established:** 61958-2601 is not a real product; all seven CMS dataset titles resolve in the v1.1 catalog; the Part D growth figures recompute exactly; the Part D double count is fixed in the script; Descovy Part D 2020–2024 is now pulled.
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

### Biktarvy Medicaid (Overall row, 2020 to 2024)

Medicaid spent $3.219B gross on Biktarvy in 2024, almost as much as Medicare Part D's $3.456B; growth slowed to 2.1% as claims fell 4.1%. Source: [Medicaid Spending by Drug, be64fce3](https://data.cms.gov/data-api/v1/dataset/be64fce3-e835-4589-b46b-024198e524a6/data?filter%5BBrnd_Name%5D=Biktarvy), pulled 30 Sep 2026.

| Measure | 2020 | 2023 | 2024 | Growth per year 2020–24 | 2024 vs 2023 |
| --- | --- | --- | --- | --- | --- |
| Gross spend | $1.807B | $3.154B | $3.219B | 15.5% | +2.1% |
| Claims | 548,569 | 794,405 | 761,489 | 8.5% | −4.1% |
| Spend per tablet | $104.89 | $122.36 | $127.31 | 5.0% | +4.0% |

- Biktarvy across Medicare Part D and Medicaid: $6.68B gross in 2024. Adding Descovy's $1.015B gives $7.69B for the two brands.
- Medicaid spend per tablet rose 4.0% in 2024 while Part D's fell 1.3%, the same split as Descovy. Both brands point to a Medicare-specific cause for the Part D dip.
- Medicaid pays about $4 per tablet less than Part D in 2024 ($127.31 vs $131.33), before Medicaid's rebate, which is not public.
- Same data quirk as Descovy: the `Overall` row's `Chg_Avg_Spnd_Per_Dsg_Unt_23_24` reads +4.6%; the yearly values and the `Gilead Sciences` row give +4.0%.

### Descovy Part D (Overall row, 2020 to 2024)

Descovy's Medicare spend is flat to falling: volume shrank about 4% a year while price per tablet rose 3.7% a year. Source: [Part D Spending by Drug, 7e0b4365](https://data.cms.gov/data-api/v1/dataset/7e0b4365-fd63-4a29-8f5e-e0ac9f66a81b/data?filter[Brnd_Name]=Descovy), pulled 30 Sep 2026.

| Measure | 2020 | 2023 | 2024 | Growth per year 2020–24 | 2024 vs 2023 |
| --- | --- | --- | --- | --- | --- |
| Gross spend | $557.9M | $589.8M | $544.7M | −0.6% | −7.7% |
| Claims | 278,040 | 249,185 | 238,782 | −3.7% | −4.2% |
| Beneficiaries | 32,107 | 29,514 | 30,179 | −1.5% | +2.3% |
| Spend per tablet | $62.47 | $75.49 | $72.19 | 3.7% | −4.4% |

- One manufacturer (Gilead), so the file returns only the `Overall` row; no double count here.
- Both brands' spend per tablet fell in 2024 (Biktarvy −1.3%, Descovy −4.4%) after rising every year since 2020. A drop in both at once may have a program-level cause rather than a price change; check WAC history before saying which. Worth one question on the slide.
- 2024 beneficiaries rose while claims fell: claims per beneficiary dropped from 8.44 to 7.91, which fits longer fills (for example 90-day supplies) rather than fewer patients.
- Biktarvy is 6.3× Descovy's Medicare spend in 2024 ($3.456B vs $544.7M).

### Descovy Medicaid (Overall row, 2020 to 2024)

Descovy's Medicaid spend peaked at $520.6M in 2023 and fell 9.6% in 2024 as claims dropped 14%. Source: [Medicaid Spending by Drug, be64fce3](https://data.cms.gov/data-api/v1/dataset/be64fce3-e835-4589-b46b-024198e524a6/data?filter[Brnd_Name]=Descovy), pulled 30 Sep 2026.

| Measure | 2020 | 2023 | 2024 | Growth per year 2020–24 | 2024 vs 2023 |
| --- | --- | --- | --- | --- | --- |
| Gross spend | $425.2M | $520.6M | $470.3M | 2.6% | −9.6% |
| Claims | 226,932 | 222,374 | 190,355 | −4.3% | −14.4% |
| Spend per tablet | $59.82 | $69.58 | $71.15 | 4.4% | +2.3% |

- Medicare and Medicaid together: $1.015B of gross Descovy spend in 2024 ($544.7M Part D, $470.3M Medicaid).
- Medicaid spend per tablet rose 2.3% in 2024 while Part D's fell 4.4%, which points to a Medicare-specific cause for the 2024 Part D dip rather than a list-price cut.
- Medicaid Spending has no beneficiary columns and is gross of the Medicaid rebate, which is large for brand drugs; net Medicaid cost is much lower.
- **Data quirk:** the `Overall` row's `Chg_Avg_Spnd_Per_Dsg_Unt_23_24` reads +5.6%, but its own per-tablet values give +2.3%, which the `Gilead Sciences` row also reports. Recompute changes from the yearly values; don't quote that field.
- Unlike Part D, this file returns both `Overall` and `Gilead Sciences` rows; keep `Overall` only.

### Descovy for PrEP under Part B (J0751)

Medicare Part B paid $44.7M for Descovy PrEP in 2025, its first year, and $15.2M in Q1 2026 alone. Source: [Quarterly Part B Spending by Drug, bf6a5b3b](https://data.cms.gov/data-api/v1/dataset/bf6a5b3b-31ee-4abb-b1ad-2607a1e7510a/data?filter[HCPCS_Cd]=J0751), pulled 30 Sep 2026; preliminary and revised each release.

| Period label | Spend | Claims | Beneficiaries | Spend per claim |
| --- | --- | --- | --- | --- |
| 2026 (Q1) | $15.2M | 5,521 | 2,813 | $2,748 |
| 2025 (Q1-Q4) | $44.7M | 16,282 | 3,080 | $2,744 |

- The annual Part B file (2024) has no J0751 rows, which fits Part B PrEP billing starting in 2025.
- Q1 2026 reached 2,813 beneficiaries, 91% of the full-year 2025 count, so uptake is still climbing. Don't multiply the quarter by four: quarterly figures are preliminary and claims lag.
- The two labels are different periods in one release; never add them.
- Part B J0751 is small next to Descovy's Part D ($544.7M) and Medicaid ($470.3M) spend in 2024.

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
