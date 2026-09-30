# Biktarvy & Descovy — Public Data Reference

Sep 30, 2026 · @Antonis

## Scope and bottom line

Every figure below comes from free public sources with no sign-in; the only thing still missing is one live run of the pull script for Descovy and the NDC-level Medicaid numbers.

- **Products:** Gilead's Biktarvy (bictegravir/emtricitabine/tenofovir alafenamide) and Descovy (emtricitabine/tenofovir alafenamide), labeler 61958, adult and pediatric strengths.
- **Verified:** corrected NDC map, list price (WAC) for both families, Biktarvy Medicare Part D 2020–2024, Biktarvy's #2 rank and $3.904B on CMS's 2028 negotiation list, Descovy's Part B PrEP payment limit, and all five CMS dataset IDs.
- **Open:** Descovy Part D and Medicaid spend, NDC-level Medicaid volume (SDUD), pharmacy acquisition cost (NADAC), and Biktarvy's negotiated price (due by 30 Nov 2026).
- **Part B** applies only to Descovy for PrEP (HCPCS J0751). Biktarvy is Part D only.
- **Net price** after rebates, 340B volume, commercial claims and Ryan White ADAP purchasing are not public.

## Corrected NDC code map

Pediatric Biktarvy is 61958-2505 and 61958-2506, not 61958-2601; no FDA, CMS or label source lists 61958-2601, so treat it as a typo.

| Family | Strength | Product NDC | Package | Billing NDC-11 | Marketed since |
| --- | --- | --- | --- | --- | --- |
| Biktarvy | 50/200/25 mg | 61958-2501 | 30-tab bottle | 61958250101 | 2018-02-07 |
| Biktarvy | 50/200/25 mg | 61958-2501 | 7-tab bottle | 61958250102 | 2018-07-26 |
| Biktarvy | 50/200/25 mg | 61958-2501 | 30-tab blister (4×7 + 1×2) | 61958250103 | 2021-08-24 |
| Biktarvy | 50/200/25 mg | 61958-2501 | 30-tab blister (3×10) | 61958250105 | 2026-03-30 |
| Biktarvy | 30/120/15 mg | 61958-2505 | 30-tab bottle | 61958250501 | 2021-10-07 |
| Biktarvy | 30/120/15 mg | 61958-2506 | 30-tab bottle (scored "BVY" tablet) | 61958250601 | 2024-10-08 |
| Descovy | 200/25 mg | 61958-2002 | 30-tab bottle | 61958200201 | 2016-04-04 |
| Descovy | 200/25 mg | 61958-2002 | 30-tab blister | 61958200202 |  |
| Descovy | 120/15 mg | 61958-2005 | 30-tab bottle | 61958200501 | 2022-01-07 |

- The 3×10 blister (61958250105) launched after CMS's negotiation look-back window, so it is missing from most historical datasets.
- Repackager NDCs also count in CMS's Biktarvy totals: 50090624700 (A-S Medication Solutions) and 70518308000–03 (RemedyRepack).
- Billing format is 5-4-2 with zero padding: 61958-2501-1 becomes 61958250101.

Sources: [Biktarvy label (Drugs.com)](https://www.drugs.com/pro/biktarvy.html), [Biktarvy label (MedLibrary)](https://medlibrary.org/lib/rx/meds/biktarvy/page/11/), [Descovy label (DailyMed)](https://dailymed.nlm.nih.gov/dailymed/fda/fdaDrugXsl.cfm?setid=06f66e98-e6ee-4538-9506-6c1282cc14c1&type=display), [CMS top-50 list](https://www.cms.gov/files/document/factsheet-medicare-top-50-negotiation-eligible-drug-list-ipay-2028.pdf).

## Verified figures

Biktarvy is Medicare's #2 negotiation-eligible drug at $3.904B, and its Part D gross spend nearly doubled from 2020 to 2024, driven mostly by volume.

### List price (WAC) and Part B payment

| Product | Metric | Per 30 tablets | Per tablet | As of | Source |
| --- | --- | --- | --- | --- | --- |
| Biktarvy, both strengths | AWP (= WAC + 20%) | $5,059.32 | $168.64 | FDB, 2026-07-19 | [Gilead Vermont disclosure](https://www.gilead.com/-/media/files/pdfs/company/disclosures/vermont/descovy-long-form.pdf) |
| Biktarvy, both strengths | WAC, implied | \~$4,216 | \~$140.54 | FDB, 2026-07-19 | derived |
| Descovy, both strengths | AWP (= WAC + 20%) | $2,772.25 | $92.41 | FDB, 2026-07-19 | [Gilead Vermont disclosure](https://www.gilead.com/-/media/files/pdfs/company/disclosures/vermont/descovy-long-form.pdf) |
| Descovy, both strengths | WAC, implied | \~$2,310 | \~$77.01 | FDB, 2026-07-19 | derived |
| Descovy 200/25 for PrEP (J0751) | Part B payment limit (ASP + 6%) | \~$2,143 | $71.427 | Q3 2026 (Jul–Sep) | [HCPCS.codes, Jul 2026](https://hcpcs.codes/drugs/07-2026/?page=6) |
| Descovy 200/25 for PrEP (J0751) | ASP, implied | \~$2,021 | \~$67.38 | Q3 2026 | derived; \~12.5% below WAC |

Both families price every strength the same: the pediatric tablet costs what the adult tablet does. Descovy 120/15 is not billable under J0751, which covers the 200/25 tablet only.

### Medicare negotiation (IPAY 2028)

- Biktarvy ranks #2 of 50 negotiation-eligible drugs, with $3,904,486,000 in combined Part B + D spend from Nov 2024 to Oct 2025 ([CMS top-50 fact sheet](https://www.cms.gov/files/document/factsheet-medicare-top-50-negotiation-eligible-drug-list-ipay-2028.pdf)).
- It is one of 15 drugs selected for the third cycle and the first HIV drug selected; about 101,000 beneficiaries used it in that window ([CMS selected-drug fact sheet](https://www.cms.gov/files/document/factsheet-medicare-negotiation-selected-drug-list-ipay-2028.pdf), [Positively Aware](https://www.positivelyaware.com/articles/biktarvy-among-15-drugs-facing-medicare-price-negotiations)).
- The negotiated price (MFP) is due by 30 Nov 2026 and applies from 1 Jan 2028.
- Descovy is not on the top-50 list; the #50 cutoff was Doptelet at $236,862,000.

### Medicaid

- Biktarvy, Humira, Stelara, Dupixent and Ozempic together account for 10% of all Medicaid drug spending in 2024 ([KFF](https://www.kff.org/medicaid/a-look-at-the-generous-model-and-factors-that-could-impact-medicaid-drug-costs/)).
- Biktarvy's estimated Medicaid rebate was 24% in 2019, per the same KFF analysis; stale, but the only public rebate signal.

### Biktarvy Medicare Part D, gross spend (Overall row)

Source: [Part D Spending by Drug API, dataset 7e0b4365](https://data.cms.gov/data-api/v1/dataset/7e0b4365-fd63-4a29-8f5e-e0ac9f66a81b/data), read live 2026-09-30.

&#91;embedded content: CMS Part D Spending by Drug, Overall row, read live 2026-09-30 · reference line: CMS top-50 fact sheet, IPAY 2028\]

- 2020–24 growth per year: spend 18.1%, claims 13.9%, beneficiaries 13.4%, spend per tablet 4.3% (CMS's own CAGR). Volume drove most of the increase.
- 2024: claims 840,772, beneficiaries 92,246, spend per tablet $131.33, down 1.3% from 2023 and the first decline in the series. It is gross pharmacy spend, not WAC; raise it as a question, not a conclusion.
- The dashed line is a different measure (Part B + D, Nov 2024 to Oct 2025), shown to check the trend; it is not a 2025 Part D figure.

## Source catalog

None of these sources needs a sign-in; the pricing and usage core is data.medicaid.gov and data.cms.gov, with openFDA and RxNav for identity.

| Source | What you get for Biktarvy / Descovy | Grain | Cadence | Access |
| --- | --- | --- | --- | --- |
| [openFDA NDC](https://open.fda.gov/apis/drug/ndc/) (`api.fda.gov/drug/ndc.json`) | NDC validation (61958-2601 check), packages, repackagers, marketing dates | Package NDC | Continuous | REST; key optional for higher limits |
| [openFDA label, FAERS, Drugs@FDA, recalls](https://open.fda.gov/apis/) | Label text, adverse-event counts, approval history (NDA 210251 / 208215) | Brand / application | Continuous | REST |
| [RxNav](https://lhncbc.nlm.nih.gov/RxNav/APIs/) (`rxnav.nlm.nih.gov`) | NDC to RxCUI, NDC history, drug classes for a competitor set | RxCUI | Monthly | REST; 20 req/s per IP |
| [DailyMed](https://dailymed.nlm.nih.gov/dailymed/app-support-web-services.cfm) | Label versions with dates; when 2506 and the 3×10 blister entered the label | SPL set ID | Continuous | REST + bulk SPL |
| [State Drug Utilization Data](https://data.medicaid.gov/dataset/61729e5a-7aa8-448c-8903-ba3e0cd0ea3c) (data.medicaid.gov) | Medicaid units, prescriptions, amount reimbursed | NDC-11 × state × quarter × FFS/MCO | Quarterly | DKAN API + CSV |
| NADAC (data.medicaid.gov) | Retail pharmacy acquisition cost per tablet | NDC-11 × week | Weekly | DKAN API + CSV |
| Medicaid Drug Rebate Program product file (data.medicaid.gov) | Market dates, status, unit type per NDC | NDC-11 | Quarterly | DKAN API |
| [Medicare Part D Spending by Drug](https://data.cms.gov/summary-statistics-on-use-and-payments/medicare-medicaid-spending-by-drug/medicare-part-d-spending-by-drug) | Gross spend, claims, beneficiaries, $/tablet, CAGR, 2020–2024 | Brand × manufacturer | Annual | data-api + CSV |
| [Medicare Quarterly Part D Spending by Drug](https://data.cms.gov/summary-statistics-on-use-and-payments/medicare-medicaid-spending-by-drug/medicare-quarterly-part-d-spending-by-drug) | Preliminary 2025 and Q1 2026 | Brand × period label | Quarterly | data-api + CSV |
| [Medicare Part B Spending by Drug](https://data.cms.gov/summary-statistics-on-use-and-payments/medicare-medicaid-spending-by-drug/medicare-part-b-spending-by-drug) + quarterly | J0751 (Descovy PrEP) spend and claims | HCPCS | Annual / quarterly | data-api |
| [Medicaid Spending by Drug](https://data.cms.gov/summary-statistics-on-use-and-payments/medicare-medicaid-spending-by-drug/medicaid-spending-by-drug) | Brand-level Medicaid spend, cross-check for SDUD | Brand × manufacturer | Annual | data-api |
| Part D Prescribers by Geography and by Provider and Drug (data.cms.gov) | Top states; prescriber count and concentration | State / NPI × brand | Annual | data-api |
| Part D Formulary PUF (monthly) and SPUF (quarterly) (data.cms.gov) | Tier, PA, step therapy, quantity limits; SPUF adds plan-level `UNIT_COST` per NDC | Plan × RxCUI / proxy NDC | Monthly / quarterly | ZIP, \~2.3 GB |
| [CMS ASP pricing files](https://www.cms.gov/medicare/payment/part-b-drugs/asp-pricing-files) + NDC-HCPCS crosswalk (incl. PrEP file) | J0751 payment limit; Descovy NDC to J0751 bridge | HCPCS / NDC | Quarterly | ZIP, manual |
| [CMS negotiation program fact sheets](https://www.cms.gov/files/document/factsheet-medicare-top-50-negotiation-eligible-drug-list-ipay-2028.pdf) | Rank, spend window, NDC scope; MFP by 30 Nov 2026 | Drug / NDC | Per cycle | PDF |
| [California HCAI WAC increases](https://data.chhs.ca.gov/dataset/prescription-drug-wholesale-acquisition-cost-wac-increases) + [new drugs to market](https://data.chhs.ca.gov/dataset/prescription-drugs-introduced-to-market) | Manufacturer-reported WAC increases and launch WAC, if Gilead crossed the threshold | NDC-11 × event | Monthly | CSV/XLSX; downloads redirect to S3 |
| [Gilead Vermont price disclosures](https://www.gilead.com/-/media/files/pdfs/company/disclosures/vermont/descovy-long-form.pdf) | AWP (WAC + 20%) for Gilead and class comparators | NDC-11 | Periodic | PDF |
| HRSA 340B OPAIS | Covered entities and contract pharmacies | Entity | Continuous | Web + export |
| NPPES NPI Registry | Prescriber and pharmacy identity for the NPI-level Part D file | NPI | Weekly | REST + monthly bulk |

Excluded because they need an account: the full RxNorm release (UMLS), Blue Button and BCDA, Snowflake or Databricks Marketplace listings, and Socrata SODA3 app tokens.

## CMS dataset IDs and catalog

All five CMS series IDs your repo hardcodes are stable series IDs and were live on 30 Sep 2026, so they roll to each new release on their own.

| Dataset | Stable series ID | Latest data | Check |
| --- | --- | --- | --- |
| Medicare Part D Spending by Drug | `7e0b4365-fd63-4a29-8f5e-e0ac9f66a81b` | 2024 | Live; Biktarvy rows returned |
| Medicare Quarterly Part D Spending by Drug | `4ff7c618-4e40-483a-b390-c8a58c94fa15` | Q1 2026 (modified 2026-07-23) | Confirmed in catalog as `latest` |
| Medicaid Spending by Drug | `be64fce3-e835-4589-b46b-024198e524a6` | 2024 | Live |
| Medicare Part B Spending by Drug | `76a714ad-3a2c-43ac-b76d-9dadf8f7d890` | 2024 | Live |
| Medicare Quarterly Part B Spending by Drug | `bf6a5b3b-31ee-4abb-b1ad-2607a1e7510a` | 2025 (Q1-Q4) label in current release | Live |

Test any ID from a phone with `https://data.cms.gov/data-api/v1/dataset/<ID>/data?size=1`; add `&filter[Brnd_Name]=Biktarvy` (Part D, Medicaid) or `&filter[HCPCS_Cd]=J0751` (Part B).

**Two catalogs, two formats:**

- [`data.json`](https://data.cms.gov/data.json) is now DCAT-US v3 (catalog modified 29 Sep 2026). Each yearly release is its own entry titled `Name : YYYY-MM-DD`, and the stable ID sits in `inSeries[0].identifier`.
- [`v1-1-data.json`](https://data.cms.gov/v1-1-data.json) keeps the old layout: one entry per dataset, with the stable ID on the distribution marked `"latest"` and in `identifier`. The pull script reads this one.
- Each distribution links a machine-readable dictionary at `/data-api/v1/dataset/<ID>/dictionary`; compare column names against it before parsing.
- Use `modified`, not `temporal`, to detect refreshed files. Distribution titles can carry suffixes like `oc1`, so don't parse dates from them.

**Column names differ between datasets:** Part D uses `Avg_Spnd_Per_Dsg_Unt_Wghtd_YYYY`, Part B uses `Avg_Spndng_Per_Dsg_Unt_YYYY`, and the quarterly files use a single `Year` label with no year suffix.

## Tools and how to run them

Use the NDC Intelligence System repo on the GitHub Actions runner for the NDC-level pulls, and `hiv_public_pull.py` on a laptop for the multi-year workbook; both need open internet, nothing else.

| Tool | What it does | Run | Status |
| --- | --- | --- | --- |
| `hiv_public_pull.py` (single file, this chat) | openFDA validation, RxCUIs, SDUD multi-year, NADAC, Part D annual + quarterly, Part B J0751, Medicaid Spending, Part D by state, optional prescribers and ASP; one Excel workbook with README and provenance sheets | `pip install requests pandas openpyxl`, then `python hiv_public_pull.py --out ./out` | Tested offline; not yet run live |
| NDC Intelligence System (`lakuna7/Pharma-Intelligence-Platform`) | Package-level matrix with exact-match validation for NADAC and SDUD, state tables, shortages, derived KPIs | Actions tab → "NDC run", one product per run: `61958-2501`, `61958-2505`, `61958-2506`, `61958-2002`, `61958-2005`; plus `61958-2601` with `lookup` | Works; gaps below |
| API-papi (docs only) | Clean rebuild: ADRs, source registry, source contracts | Not runnable yet | Architecture reference |

**`hiv_public_pull.py` options:** `--sdud-years 2022-2025` (faster), `--nadac-years 2024-2026`, `--prescribers` (NPI-level, large), `--asp-zip <path or URL>` (J0751 payment limit), `--no-repackagers`. Behind a corporate proxy, set `HTTPS_PROXY` and `REQUESTS_CA_BUNDLE`.

**Fixes already in the script:** Part D long sheet keeps the `Overall` row only; state and National geography rows are split; catalog lookup uses `v1-1-data.json`; a startup check skips unreachable hosts instead of retrying for minutes; README warnings include late ones.

**Gaps in the repo for this deck:**

- SDUD is 2024 only (issue I-14), so no trend line.
- Part B is looked up by brand name, which misses Descovy's J0751. The fix is an HCPCS filter or the CMS PrEP NDC-HCPCS crosswalk.
- The California WAC lookup may point at the data-dictionary resource `3a133d3f-…`; test with `limit=1` and check for NDC columns.
- The workflow file is named `  ndc-run.yaml ` with a leading space; rename if "NDC run" is missing from the Actions tab.
- Brand-level values repeat on every NDC row (issue I-19): take them from one row, never sum the column.

**API-papi:** record the v3 catalog layout in its CMS contract and read stable keys from `inSeries[0].identifier`. Snapshot the catalog daily and compare `modified` per distribution to catch new releases.

## Pull checklist for the VP deck

Items 1–5 carry the deck; the VP's first three questions will be Biktarvy's Medicare spend, Medicaid spend on both brands, and the gap between list and realized price.

**Core (one slide each)**

- [ ] 1\. Part D Spending by Drug: `Brnd_Name` = Biktarvy and Descovy, `Mftr_Name` = Overall; spend, claims, beneficiaries, $/tablet, CAGR for 2020–2024. Biktarvy done; Descovy open.
- [ ] 2\. Quarterly Part D Spending: same filter; 2025 and Q1 2026, filtered to one `Year` label and labelled preliminary.
- [ ] 3\. SDUD 2022–2025: the nine NDC-11s; units, prescriptions, total and Medicaid reimbursed by quarter. Use state `XX` rows for national totals only.
- [ ] 4\. NADAC, latest week: the nine NDC-11s; `nadac_per_unit` × 30 for a monthly figure.
- [x] 5\. List price (WAC): Vermont disclosure, done.

**Supporting**

- [ ] 6\. Part B Spending, annual and quarterly: `HCPCS_Cd` = J0751.
- [ ] 7\. ASP payment limits, last 4–8 quarters: J0751; divide by 1.06 for ASP.
- [ ] 8\. Part D by Geography and Drug: both brands, state rows only.
- [ ] 9\. Part D by Provider and Drug: prescriber count and top-10% share of claims.
- [ ] 10\. California HCAI WAC increases and new drugs: manufacturer = Gilead; drop the slide if there are no Gilead rows.
- [ ] 11\. Quarterly Part D SPUF `UNIT_COST`: plan-level realized unit cost for Biktarvy.

**Validation (no slide)**

- [ ] 12\. openFDA lookup of 61958-2601: expect NOT\_FOUND.
- [ ] 13\. Biktarvy negotiated price (MFP): check CMS on 30 Nov 2026; map it to the NDC-11s yourself, since it may not be published per package.

## Caveats and data gaps

Every spend figure here is gross, before rebates; say so on each slide.

| Rule | Why it matters |
| --- | --- |
| Part D and Medicaid Spending are brand-level, not NDC-level | Only the CMS negotiation list ties Medicare spend to specific NDCs |
| CMS repeats each brand as an `Overall` row plus one row per manufacturer | Summing both doubles spend; keep `Overall` only |
| Quarterly releases hold several `Year` labels, some cumulative (`2025 (Q1-Q4)`) | Filter to one label; never sum across labels or read quarters as a run-rate |
| SDUD blanks cells under 11 prescriptions | Totals are minimums; count the suppressed rows |
| SDUD state `XX` rows are national totals | Adding them to state rows double-counts |
| NADAC covers retail community pharmacies | Misses 340B and specialty pharmacy, where most HIV volume moves |
| A Part B payment limit is not an acquisition cost, and presence in the file is not coverage | J0751 = ASP + 6% for the PrEP use only |
| Formulary PUF NDCs are proxy NDCs | They don't show which package was dispensed |
| Descovy's pediatric 120/15 tablet is outside J0751 | Part B PrEP figures cover the 200/25 tablet only |

**Not in any public source:** net price after rebates, 340B purchase volume, commercial claims, and Ryan White ADAP purchasing. ADAP is a material HIV channel, so Medicare + Medicaid understates the market.

## Open items

One live run unblocks everything else; the rest are checks.

- [ ] Run `hiv_public_pull.py` on a machine with open internet and send back the workbook; check the provenance row counts and whether `partd_spending_qtr` has rows.
- [ ] Pull Descovy Part D annual: `https://data.cms.gov/data-api/v1/dataset/7e0b4365-fd63-4a29-8f5e-e0ac9f66a81b/data?filter[Brnd_Name]=Descovy`.
- [ ] Download the current ASP pricing ZIP and pass it with `--asp-zip` for J0751.
- [ ] Test the repo's California WAC resource ID against the dictionary resource.
- [ ] Rename the repo's workflow file to remove the leading space.
- [ ] Check CMS for Biktarvy's negotiated price after 30 Nov 2026.
- [ ] Retire the other session's copy of the script; this chat's version is the one to keep.

## Sources

- [CMS top-50 negotiation-eligible drugs, IPAY 2028](https://www.cms.gov/files/document/factsheet-medicare-top-50-negotiation-eligible-drug-list-ipay-2028.pdf)
- [CMS selected drugs, IPAY 2028](https://www.cms.gov/files/document/factsheet-medicare-negotiation-selected-drug-list-ipay-2028.pdf)
- [Medicare Part D Spending by Drug API (7e0b4365)](https://data.cms.gov/data-api/v1/dataset/7e0b4365-fd63-4a29-8f5e-e0ac9f66a81b/data)
- [Medicare Part D Spending by Drug landing page](https://data.cms.gov/summary-statistics-on-use-and-payments/medicare-medicaid-spending-by-drug/medicare-part-d-spending-by-drug)
- [Medicare Quarterly Part D Spending by Drug](https://data.cms.gov/summary-statistics-on-use-and-payments/medicare-medicaid-spending-by-drug/medicare-quarterly-part-d-spending-by-drug)
- [data.cms.gov catalog, DCAT-US v3](https://data.cms.gov/data.json) and [v1.1](https://data.cms.gov/v1-1-data.json)
- [State Drug Utilization Data 2024](https://data.medicaid.gov/dataset/61729e5a-7aa8-448c-8903-ba3e0cd0ea3c)
- [Gilead Vermont disclosure, Descovy long form (FDB 2026-07-19)](https://www.gilead.com/-/media/files/pdfs/company/disclosures/vermont/descovy-long-form.pdf)
- [J0751 payment limit, Jul–Sep 2026](https://hcpcs.codes/drugs/07-2026/?page=6)
- [CGS Medicare PrEP fee page](https://cgsmedicare.com/partb/fees/prep.html)
- [Biktarvy label (Drugs.com)](https://www.drugs.com/pro/biktarvy.html)
- [Descovy label (DailyMed)](https://dailymed.nlm.nih.gov/dailymed/fda/fdaDrugXsl.cfm?setid=06f66e98-e6ee-4538-9506-6c1282cc14c1&type=display)
- [KFF on Medicaid drug spending and the GENEROUS model](https://www.kff.org/medicaid/a-look-at-the-generous-model-and-factors-that-could-impact-medicaid-drug-costs/)
- [California HCAI WAC increases](https://data.chhs.ca.gov/dataset/prescription-drug-wholesale-acquisition-cost-wac-increases)
- [Positively Aware on Biktarvy's selection](https://www.positivelyaware.com/articles/biktarvy-among-15-drugs-facing-medicare-price-negotiations)
