# SEC EDGAR Form Types Supporting XBRL

## Introduction

XBRL (eXtensible Business Reporting Language) is the machine-readable format the SEC uses to standardize financial and disclosure data across EDGAR filings. It was first introduced on **January 30, 2009** through Release [33-9002](https://www.sec.gov/rules/final/2009/33-9002.pdf) ("Interactive Data to Improve Financial Reporting"), which required operating companies to tag their financial statements. Just twelve days later, on **February 11, 2009**, Release [33-9006](https://www.sec.gov/rules/final/2009/33-9006.pdf) extended XBRL to mutual fund risk/return summaries, and Release [34-59342](https://www.sec.gov/rules/final/2009/34-59342.pdf) brought NRSRO credit rating histories into scope later that same year.

Over the past 15+ years, the SEC has progressively expanded XBRL requirements — from financial statements of operating companies, to cover pages, fund prospectuses, cybersecurity disclosures, pay-versus-performance data, broker-dealer annual reports, and credit rating histories from NRSROs. More recent waves pulled in self-regulatory organizations (2023), security-based swap execution facilities (2023), and broker-dealers and security-based swap entities (2024).

Today, XBRL (in most cases, Inline XBRL) touches seven distinct categories of SEC filers, each with its own submission types, taxonomies, and rule history. This post consolidates, in one place, every EDGAR form type that must be filed with XBRL data — along with the taxonomies that govern them and the SEC releases that created the requirements.

## XBRL vs. Inline XBRL

**Classic XBRL** is a separate XML instance document — tagged facts live in a standalone file (e.g., `EX-100.*`) that sits next to the human-readable filing. Humans read the HTML; machines parse the XML. Two artifacts, two sources of truth, and a perpetual drift risk between them.

**Inline XBRL (iXBRL)** collapses both into a single XHTML document. Tags are embedded directly in the filing using the `ix:` namespace (e.g., `<ix:nonFraction>`), so the same file renders as a readable document in a browser and exposes structured data to parsers. SEC attachment type: `EX-101.*`. One artifact, one source of truth, no drift.

The SEC first mandated iXBRL via Release [33-10514](https://www.sec.gov/rules/final/2018/33-10514.pdf) (June 28, 2018), phased in by filer status from 2019–2021. Every category in this post uses **Inline XBRL today — except NRSROs**, who still publish credit rating histories as classic XBRL on their own websites (not through EDGAR), under the ROCR taxonomy.

**All XBRL files are attached to EDGAR filings** as submission attachments (classic XBRL under `EX-100.*`, Inline XBRL under `EX-101.*`), and are accessible alongside the primary filing document in every EDGAR submission's index. The only exception is NRSRO ROCR data, which is not filed with the SEC and must be retrieved directly from each NRSRO's own website.

Practical implications for data consumers:

- For standardized XBRL-JSON data access, the [XBRL-to-JSON Converter API](https://sec-api.io/docs/xbrl-to-json-converter-api) converts any 10-K, 10-Q, 20-F, 40-F (and other iXBRL-tagged filings) into structured JSON — financial statements, footnotes, and cover-page facts — without needing to parse `ix:` tags, resolve contexts, or load taxonomy linkbases yourself.
- The SEC's Financial Statement and Notes Data Sets and Frames API normalize iXBRL facts across filings, so most users never touch the raw `ix:` tags.
- Classic XBRL (NRSRO ROCR) requires fetching the XML instance plus its taxonomy schema and linkbases from the issuer's site — there is no EDGAR endpoint for it.

---

## Categories at a Glance

7 categories of XBRL-enabled form types, all sourced from official SEC pages:

| #   | Category                                 | Submission Types                                                                    | Taxonomies                                   | First Introduced | Originating Release                                                                                                                                                                                                                              |
| --- | ---------------------------------------- | ----------------------------------------------------------------------------------- | -------------------------------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1   | Operating Companies                      | 80+ types (10-K, 10-Q, 8-K, 20-F, 40-F, S-1, S-3, F-1, proxy statements, etc.)      | US GAAP, IFRS, DEI, ECD, CYD, RXP, FFD, SPAC | Jan. 30, 2009    | [33-9002](https://www.sec.gov/rules/final/2009/33-9002.pdf) — Interactive Data to Improve Financial Reporting                                                                                                                                    |
| 2   | Investment Companies / Funds             | 60+ types (N-1A, N-2, N-3, N-4, N-6, N-CSR, 485/486/497 variants, 424 prospectuses) | OEF, CEF, VIP, FND                           | Feb. 11, 2009    | [33-9006](https://www.sec.gov/rules/final/2009/33-9006.pdf) — Interactive Data for Mutual Fund Risk/Return Summary                                                                                                                               |
| 3   | Broker-Dealers                           | Form X-17A-5 Part III, Form 17-H Item 4                                             | —                                            | Dec. 16, 2024    | [33-11342](https://www.sec.gov/files/rules/final/2024/33-11342.pdf) — Electronic Submission of Certain Materials Under the Exchange Act; FOCUS Report                                                                                            |
| 4   | Security-Based Swap Entities             | Form X-17A-5 Part III, CCO reports                                                  | —                                            | Dec. 16, 2024    | [33-11342](https://www.sec.gov/files/rules/final/2024/33-11342.pdf) — Electronic Submission of Certain Materials Under the Exchange Act; FOCUS Report                                                                                            |
| 5   | Security-Based Swap Execution Facilities | Form SBSEF exhibits, financial/compliance reports                                   | SBS                                          | Nov. 2, 2023     | [34-98845](https://www.federalregister.gov/documents/2023/12/15/2023-24587/security-based-swap-execution-and-registration-and-regulation-of-security-based-swap-execution) — Security-Based Swap Execution and Registration/Regulation of SBSEFs |
| 6   | Self-Regulatory Organizations            | Rule 17Ad-27 annual report, Form 1 exhibits, Form CA-1 exhibits                     | SRO                                          | Feb. 15, 2023    | [34-96930](https://www.sec.gov/rules/final/2023/34-96930.pdf) — Shortening the Securities Transaction Settlement Cycle                                                                                                                           |
| 7   | NRSROs                                   | Credit rating histories in standard XBRL (published on their own websites)          | ROCR                                         | 2009             | [34-59342](https://www.sec.gov/rules/final/2009/34-59342.pdf) — NRSROs (original XBRL requirement)                                                                                                                                               |

---

## 1. Operating Companies (Inline XBRL)

Operating companies must file cover page, financial statement information (including footnotes, schedules, and auditor information in annual reports), and certain other disclosures in Inline XBRL.

**Attachment Type:** `EX-101.*`

### EDGAR Submission Types

| Form Type | Description                                       |
| --------- | ------------------------------------------------- |
| 10-K      | Annual report                                     |
| 10-K/A    | Annual report amendment                           |
| 10-KT     | Transition report (annual)                        |
| 10-KT/A   | Transition report amendment (annual)              |
| 10-Q      | Quarterly report                                  |
| 10-Q/A    | Quarterly report amendment                        |
| 10-QT     | Transition report (quarterly)                     |
| 10-QT/A   | Transition report amendment (quarterly)           |
| 10-12B    | Registration under Section 12(b)                  |
| 10-12B/A  | Registration under 12(b) amendment                |
| 10-12G    | Registration under Section 12(g)                  |
| 10-12G/A  | Registration under 12(g) amendment                |
| 8-K       | Current report                                    |
| 8-K/A     | Current report amendment                          |
| 8-K12B    | Current report (Section 12(b) registration)       |
| 8-K12B/A  | Current report (12(b) registration) amendment     |
| 8-K12G3   | Current report (Section 12(g) registration)       |
| 8-K12G3/A | Current report (12(g) registration) amendment     |
| 8-K15D5   | Current report (15(d) suspension)                 |
| 8-K15D5/A | Current report (15(d) suspension) amendment       |
| 20-F      | Annual report (foreign private issuer)            |
| 20-F/A    | Annual report (FPI) amendment                     |
| 20FR12B   | Registration under 12(b) (FPI)                    |
| 20FR12B/A | Registration under 12(b) (FPI) amendment          |
| 20FR12G   | Registration under 12(g) (FPI)                    |
| 20FR12G/A | Registration under 12(g) (FPI) amendment          |
| 40-F      | Annual report (Canadian issuer)                   |
| 40-F/A    | Annual report (Canadian issuer) amendment         |
| 40FR12B   | Registration under 12(b) (Canadian issuer)        |
| 40FR12B/A | Registration under 12(b) (Canadian) amendment     |
| 40FR12G   | Registration under 12(g) (Canadian issuer)        |
| 40FR12G/A | Registration under 12(g) (Canadian) amendment     |
| 6-K       | Report of foreign private issuer                  |
| 6-K/A     | Report of FPI amendment                           |
| SP 15D2   | Special financial report                          |
| SP 15D2/A | Special financial report amendment                |
| S-1       | Registration statement (Securities Act)           |
| S-1/A     | S-1 amendment                                     |
| S-1MEF    | S-1 (master effective filing)                     |
| S-3       | Registration statement (short form)               |
| S-3/A     | S-3 amendment                                     |
| S-3ASR    | Automatic shelf registration                      |
| S-3D      | S-3 designation of additional securities          |
| S-3DPOS   | S-3D post-effective amendment                     |
| S-3MEF    | S-3 (master effective filing)                     |
| S-4       | Registration (business combinations)              |
| S-4/A     | S-4 amendment                                     |
| S-4EF     | S-4 (auto-effective)                              |
| S-4MEF    | S-4 (master effective filing)                     |
| S-4 POS   | S-4 post-effective amendment                      |
| S-11      | Registration (real estate companies)              |
| S-11/A    | S-11 amendment                                    |
| S-11MEF   | S-11 (master effective filing)                    |
| POS AM    | Post-effective amendment                          |
| POS EX    | Post-effective exhibit amendment                  |
| POSASR    | Post-effective amendment (automatic shelf)        |
| F-1       | Registration (foreign private issuer)             |
| F-1/A     | F-1 amendment                                     |
| F-1MEF    | F-1 (master effective filing)                     |
| F-3       | Registration (FPI short form)                     |
| F-3/A     | F-3 amendment                                     |
| F-3ASR    | Automatic shelf registration (FPI)                |
| F-3D      | F-3 designation of additional securities          |
| F-3DPOS   | F-3D post-effective amendment                     |
| F-3MEF    | F-3 (master effective filing)                     |
| F-4       | Registration (FPI business combinations)          |
| F-4/A     | F-4 amendment                                     |
| F-4EF     | F-4 (auto-effective)                              |
| F-4MEF    | F-4 (master effective filing)                     |
| F-4 POS   | F-4 post-effective amendment                      |
| F-10      | Registration (Canadian issuer)                    |
| F-10/A    | F-10 amendment                                    |
| F-10EF    | F-10 (auto-effective)                             |
| F-10POS   | F-10 post-effective amendment                     |
| DEF 14A   | Definitive proxy statement                        |
| DEF 14C   | Definitive information statement                  |
| DEFA14A   | Additional definitive proxy materials             |
| DEFA14C   | Additional definitive information materials       |
| DEFC14A   | Definitive proxy (contested solicitations)        |
| DEFC14C   | Definitive information (contested solicitations)  |
| DEFM14A   | Definitive proxy (merger/acquisition)             |
| DEFM14C   | Definitive information (merger/acquisition)       |
| DEFR14A   | Definitive revised proxy                          |
| DEFR14C   | Definitive revised information statement          |
| PRE 14A   | Preliminary proxy statement                       |
| PRE 14C   | Preliminary information statement                 |
| PREC14A   | Preliminary proxy (contested solicitations)       |
| PREC14C   | Preliminary information (contested solicitations) |
| PREM14A   | Preliminary proxy (merger/acquisition)            |
| PREM14C   | Preliminary information (merger/acquisition)      |
| PRER14A   | Preliminary revised proxy                         |
| PRER14C   | Preliminary revised information statement         |

### What Must Be Filed in Inline XBRL

- **Cover page** information
- **Financial statements** (including footnotes and schedules)
- **Auditor information** (in annual reports)
- **Pay versus performance** disclosures (DEF 14A, etc.)
- **Resource extraction payment** disclosures (Form SD)
- **Filing fee** disclosures
- **Cybersecurity** risk management, strategy, governance, and incident disclosures
- **Insider trading arrangements** disclosures
- **Clawback/compensation recovery** disclosures
- **SPAC-related** disclosures
- **HFCAA** (Holding Foreign Companies Accountable Act) disclosures
- **Employee benefit plan** financial statements (11-K annual reports)

### Taxonomies

| Taxonomy | Description                                 | Guide                                                                                                                        |
| -------- | ------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| US GAAP  | Financial reporting (FASB)                  | [2026 Release Notes](https://xbrl.fasb.org/resources/annualrelease/2026/GAAP_Financial_Reporting_Taxonomy_Release_Notes.pdf) |
| IFRS     | International Financial Reporting Standards | [IFRS Taxonomy](https://www.ifrs.org/issued-standards/ifrs-taxonomy/)                                                        |
| DEI      | Document & Entity Information               | Included in US GAAP/IFRS packages                                                                                            |
| ECD      | Executive Compensation Disclosure           | [ECD Guide 2026](https://xbrl.sec.gov/ecd/2026/ecd-taxonomy-guide-2026-03-16.pdf)                                            |
| CYD      | Cybersecurity Disclosure                    | [CYD Guide 2026](https://xbrl.sec.gov/cyd/2026/cyd-taxonomy-guide-2026-03-16.pdf)                                            |
| RXP      | Resource Extraction Payments                | [RXP Guide 2026](https://xbrl.sec.gov/rxp/2026/rxp-taxonomy-guide-2026-03-16.pdf)                                            |
| FFD      | Filing Fee Disclosure                       | [FFD Files 2026](https://xbrl.sec.gov/ffd/2026/)                                                                             |
| SPAC     | Special Purpose Acquisition Company         | [SPAC Guide 2026](https://xbrl.sec.gov/spac/2026/spac-taxonomy-guide-2026-03-16.pdf)                                         |

### Relevant SEC Releases (Rules)

| Release                                                             | Title                                                                        | Date          |
| ------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ------------- |
| [33-9002](https://www.sec.gov/rules/final/2009/33-9002.pdf)         | Interactive Data to Improve Financial Reporting                              | Jan. 30, 2009 |
| [33-10320](https://www.sec.gov/rules/final/2017/33-10320.pdf)       | IFRS Taxonomy for FPIs                                                       | Mar. 1, 2017  |
| [33-10514](https://www.sec.gov/rules/final/2018/33-10514.pdf)       | Inline XBRL Filing of Tagged Data                                            | June 28, 2018 |
| [33-10618](https://www.sec.gov/rules/final/2019/33-10618.pdf)       | FAST Act Modernization (Reg S-K)                                             | Mar. 20, 2019 |
| [34-93701](https://www.sec.gov/rules/final/2021/34-93701.pdf)       | Holding Foreign Companies Accountable Act Disclosure                         | Dec. 2, 2021  |
| [33-11070](https://www.sec.gov/rules/final/2022/33-11070.pdf)       | Updating EDGAR Filing Requirements / Form 144                                | June 2, 2022  |
| [34-95607](https://www.sec.gov/rules/final/2022/34-95607.pdf)       | Pay Versus Performance                                                       | Aug. 25, 2022 |
| [33-11126](https://www.sec.gov/rules/final/2022/33-11126.pdf)       | Listing Standards for Recovery of Erroneously Awarded Compensation           | Oct. 26, 2022 |
| [33-11138](https://www.sec.gov/rules/final/2022/33-11138.pdf)       | Insider Trading Arrangements and Related Disclosures                         | Dec. 14, 2022 |
| [33-11216](https://www.sec.gov/rules/final/2023/33-11216.pdf)       | Cybersecurity Risk Management, Strategy, Governance, and Incident Disclosure | July 26, 2023 |
| [33-11265](https://www.sec.gov/files/rules/final/2024/33-11265.pdf) | Special Purpose Acquisition Companies, Shell Companies, and Projections      | Jan. 24, 2024 |

---

## 2. Investment Companies / Funds (Inline XBRL)

Funds and investment companies must file certain prospectus, shareholder report, and registration information in Inline XBRL.

**Attachment Type:** `EX-101.*`

### EDGAR Submission Types

| Form Type  | Description                                                |
| ---------- | ---------------------------------------------------------- |
| N-1A       | Open-end fund registration statement                       |
| N-1A/A     | N-1A amendment                                             |
| N-2        | Closed-end fund registration statement                     |
| N-2/A      | N-2 amendment                                              |
| N-2ASR     | N-2 automatic shelf registration                           |
| N-2 POSASR | N-2 post-effective amendment (automatic shelf)             |
| N-2MEF     | N-2 (master effective filing)                              |
| N-3        | Variable annuity separate account (management company)     |
| N-3/A      | N-3 amendment                                              |
| N-4        | Variable annuity separate account (UIT)                    |
| N-4/A      | N-4 amendment                                              |
| N-6        | Variable life insurance separate account (UIT)             |
| N-6/A      | N-6 amendment                                              |
| N-CSR      | Certified shareholder report                               |
| N-CSR/A    | N-CSR amendment                                            |
| N-CSRS     | Certified semi-annual shareholder report                   |
| N-CSRS/A   | N-CSRS amendment                                           |
| 485APOS    | Post-effective amendment (auto-effective)                  |
| 485BPOS    | Post-effective amendment (effective upon filing)           |
| 485BXT     | Post-effective amendment (extension of time)               |
| 486APOS    | Post-effective amendment (auto-effective, 1933 Act)        |
| 486BPOS    | Post-effective amendment (effective upon filing, 1933 Act) |
| 486BXT     | Post-effective amendment (extension, 1933 Act)             |
| 487        | Initial registration (investment co.)                      |
| 497        | Definitive materials (fund prospectus supplement)          |
| 497J       | Certification of no change                                 |
| 424A       | Prospectus (Rule 424(a))                                   |
| 424B1      | Prospectus (Rule 424(b)(1))                                |
| 424B2      | Prospectus (Rule 424(b)(2))                                |
| 424B3      | Prospectus (Rule 424(b)(3))                                |
| 424B4      | Prospectus (Rule 424(b)(4))                                |
| 424B5      | Prospectus (Rule 424(b)(5))                                |
| 424B7      | Prospectus (Rule 424(b)(7))                                |
| 424B8      | Prospectus (Rule 424(b)(8))                                |
| POS EX     | Post-effective exhibit amendment                           |
| POS462B    | Post-effective (Rule 462(b))                               |
| POS462C    | Post-effective (Rule 462(c))                               |
| POS 8C     | Post-effective amendment (Section 8(c))                    |
| POS AMI    | Post-effective amendment (investment company)              |
| SC 13E3    | Going-private transaction                                  |
| SC 13E3/A  | Going-private amendment                                    |
| DEF 14A    | Definitive proxy statement                                 |
| DEF 14C    | Definitive information statement                           |
| DEFA14A    | Additional definitive proxy materials                      |
| DEFA14C    | Additional definitive information materials                |
| DEFC14A    | Definitive proxy (contested solicitations)                 |
| DEFC14C    | Definitive information (contested solicitations)           |
| DEFM14A    | Definitive proxy (merger/acquisition)                      |
| DEFM14C    | Definitive information (merger/acquisition)                |
| DEFR14A    | Definitive revised proxy                                   |
| DEFR14C    | Definitive revised information statement                   |
| 8-K        | Current report                                             |
| 8-K/A      | Current report amendment                                   |
| 8-K12B     | Current report (12(b) registration)                        |
| 8-K12B/A   | Current report (12(b) registration) amendment              |
| 8-K12G3    | Current report (12(g) registration)                        |
| 8-K12G3/A  | Current report (12(g) registration) amendment              |
| 8-K15D5    | Current report (15(d) suspension)                          |
| 8-K15D5/A  | Current report (15(d) suspension) amendment                |
| 10-K       | Annual report (BDCs)                                       |
| 10-K/A     | Annual report amendment (BDCs)                             |
| 10-KT      | Transition report (BDCs)                                   |
| 10-KT/A    | Transition report amendment (BDCs)                         |
| 10-Q       | Quarterly report (BDCs)                                    |
| 10-Q/A     | Quarterly report amendment (BDCs)                          |
| 10-QT      | Transition report quarterly (BDCs)                         |
| 10-QT/A    | Transition report quarterly amendment (BDCs)               |

### What Must Be Filed in Inline XBRL

- **Open-end funds (N-1A):** Risk/return summary information
- **Open-end funds (N-CSR):** Tailored shareholder reports
- **Closed-end funds & BDCs (N-2):** Specified prospectus items and cover page
- **BDCs:** Financial statements and Exchange Act report disclosures (same extent as operating companies)
- **Variable contracts (N-3, N-4, N-6):** Specified prospectus items
- **Investment company names (N-1A, N-2, N-8B-2, S-6):** Rule 35d-1 prospectus disclosures

### Taxonomies

| Taxonomy | Description                                       | Guide                                                                             |
| -------- | ------------------------------------------------- | --------------------------------------------------------------------------------- |
| OEF      | Open-End Fund (risk/return & shareholder reports) | [OEF Guide 2026](https://xbrl.sec.gov/oef/2026/oef-taxonomy-guide-2026-03-16.pdf) |
| CEF      | Closed-End Fund                                   | [CEF Guide 2026](https://xbrl.sec.gov/cef/2026/cef-taxonomy-guide-2026-03-16.pdf) |
| VIP      | Variable Insurance Products                       | [VIP Guide 2026](https://xbrl.sec.gov/vip/2026/vip-taxonomy-guide-2026-03-16.pdf) |
| FND      | Fund Names (Rule 35d-1)                           | [FND Guide 2026](https://xbrl.sec.gov/fnd/2026/fnd-taxonomy-guide-2026-03-16.pdf) |

### Relevant SEC Releases (Rules)

| Release                                                                      | Title                                                               | Date           |
| ---------------------------------------------------------------------------- | ------------------------------------------------------------------- | -------------- |
| [33-9006](https://www.sec.gov/rules/final/2009/33-9006.pdf)                  | Interactive Data for Mutual Fund Risk/Return Summary                | Feb. 11, 2009  |
| [33-10514](https://www.sec.gov/rules/final/2018/33-10514.pdf)                | Inline XBRL Filing of Tagged Data                                   | June 28, 2018  |
| [33-10765](https://www.sec.gov/rules/final/2020/33-10765.pdf)                | Updated Disclosure Requirements for Variable Annuity/Life Insurance | Mar. 11, 2020  |
| [33-10771](https://www.sec.gov/rules/final/2020/33-10771.pdf)                | Securities Offering Reform for Closed-End Investment Companies      | Apr. 8, 2020   |
| [33-11125](https://www.sec.gov/rules/final/2022/33-11125.pdf)                | Tailored Shareholder Reports for Mutual Funds and ETFs              | Oct. 26, 2022  |
| [33-11238](https://www.sec.gov/files/rules/final/2023/33-11238.pdf)          | Investment Company Names                                            | Sept. 20, 2023 |
| [33-11249](https://www.sec.gov/rules-regulations/2024/07/rila#33-11294final) | Registration for Index-Linked Annuities; Form N-4 Amendments        | July 1, 2024   |

---

## 3. Broker-Dealers (Inline XBRL)

Broker-dealers, including OTC derivative dealers, must file certain annual reports and risk assessment disclosures in Inline XBRL.

### Forms Requiring Inline XBRL

| Form Type          | XBRL Scope                         | Rule                    |
| ------------------ | ---------------------------------- | ----------------------- |
| X-17A-5 Part III   | Annual report (except facing page) | Rule 17a-5, Rule 17a-12 |
| Form 17-H (Item 4) | Risk assessment report             | Rule 17h-2T             |

### Relevant SEC Releases

| Release                                                             | Title                                                                           | Date          |
| ------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------- |
| [33-11342](https://www.sec.gov/files/rules/final/2024/33-11342.pdf) | Electronic Submission of Certain Materials Under the Exchange Act; FOCUS Report | Dec. 16, 2024 |

---

## 4. Security-Based Swap Entities (Inline XBRL)

Security-based swap dealers (SBSDs) and major security-based swap participants (MSBSPs) must file certain reports in Inline XBRL.

### Forms Requiring Inline XBRL

| Form Type        | XBRL Scope                             | Rule           |
| ---------------- | -------------------------------------- | -------------- |
| X-17A-5 Part III | Annual report (except facing page)     | Rule 18a-7     |
| CCO Report       | Chief Compliance Officer report (full) | Rule 15Fk-1(c) |

### Relevant SEC Releases

| Release                                                             | Title                                                                           | Date          |
| ------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------- |
| [33-11342](https://www.sec.gov/files/rules/final/2024/33-11342.pdf) | Electronic Submission of Certain Materials Under the Exchange Act; FOCUS Report | Dec. 16, 2024 |

---

## 5. Security-Based Swap Execution Facilities (Inline XBRL)

SBSEFs must submit certain registration, financial, and compliance reports in Inline XBRL.

### Forms Requiring Inline XBRL

| Form Type                   | XBRL Scope                                        |
| --------------------------- | ------------------------------------------------- |
| Form SBSEF                  | Exhibits C-F, H-L, P-S (registration application) |
| Financial resources reports | Required under Regulation SE                      |
| CCO annual report           | Chief Compliance Officer report                   |

### Taxonomy

| Taxonomy | Description         | Guide                                                                             |
| -------- | ------------------- | --------------------------------------------------------------------------------- |
| SBS      | Security-Based Swap | [SBS Guide 2026](https://xbrl.sec.gov/sbs/2026/sbs-taxonomy-guide-2025-12-18.pdf) |

### Relevant SEC Releases

| Release                                                                                                                                                                    | Title                                                                           | Date          |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------- |
| [34-98845](https://www.federalregister.gov/documents/2023/12/15/2023-24587/security-based-swap-execution-and-registration-and-regulation-of-security-based-swap-execution) | Security-Based Swap Execution and Registration/Regulation of SBSEFs             | Nov. 2, 2023  |
| [33-11342](https://www.sec.gov/files/rules/final/2024/33-11342.pdf)                                                                                                        | Electronic Submission of Certain Materials Under the Exchange Act; FOCUS Report | Dec. 16, 2024 |

---

## 6. Self-Regulatory Organizations (Inline XBRL)

Registered national securities exchanges and registered clearing agencies must file certain materials in Inline XBRL.

### Forms Requiring Inline XBRL

| Form Type                                                     | XBRL Scope                      | Entity                                               |
| ------------------------------------------------------------- | ------------------------------- | ---------------------------------------------------- |
| Rule 17Ad-27 annual report                                    | Full report                     | Clearing agencies providing central matching service |
| Form 1 (Exhibits D, E (partial), I)                           | Specified exhibits              | National securities exchanges                        |
| Form CA-1 (Schedule A; Exhibits C, F, H, J, K, L, M, O, R, S) | Specified schedule and exhibits | Clearing agencies                                    |

### Taxonomy

| Taxonomy | Description                  | Guide                                                                                   |
| -------- | ---------------------------- | --------------------------------------------------------------------------------------- |
| SRO      | Self-Regulatory Organization | [SRO Guide 2026](https://xbrl.sec.gov/sro/2026/sro2026q3-taxonomy-guide-2026-02-05.pdf) |

### Relevant SEC Releases

| Release                                                             | Title                                                                           | Date          |
| ------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------- |
| [34-96930](https://www.sec.gov/rules/final/2023/34-96930.pdf)       | Shortening the Securities Transaction Settlement Cycle                          | Feb. 15, 2023 |
| [33-11342](https://www.sec.gov/files/rules/final/2024/33-11342.pdf) | Electronic Submission of Certain Materials Under the Exchange Act; FOCUS Report | Dec. 16, 2024 |

---

## 7. Nationally Recognized Statistical Rating Organizations (XBRL)

NRSROs must disclose credit rating histories using XBRL (standard XBRL, not Inline XBRL). This data is posted on the NRSRO's own website, not filed through EDGAR.

### Taxonomy

| Taxonomy | Description              | Guide                                                                                   |
| -------- | ------------------------ | --------------------------------------------------------------------------------------- |
| ROCR     | Record of Credit Ratings | [ROCR Preparer's Guide](https://xbrl.sec.gov/doc/rocr-publication-guide-2015-03-31.pdf) |

### Relevant SEC Releases

| Release                                                       | Title                              | Date |
| ------------------------------------------------------------- | ---------------------------------- | ---- |
| [34-59342](https://www.sec.gov/rules/final/2009/34-59342.pdf) | NRSROs (original XBRL requirement) | 2009 |
| [34-72936](https://www.sec.gov/rules/final/2014/34-72936.pdf) | NRSROs (amended XBRL requirement)  | 2014 |

---

## Key Reference Links

| Resource                            | URL                                                                                                                  |
| ----------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| Inline XBRL Overview                | https://www.sec.gov/data-research/structured-data/inline-xbrl                                                        |
| Standard Taxonomies                 | https://www.sec.gov/data-research/standard-taxonomies                                                                |
| Operating Company Taxonomies        | https://www.sec.gov/data-research/structured-data/taxonomies-schemas/standard-taxonomies/operating-companies         |
| Investment Company Taxonomies       | https://www.sec.gov/data-research/structured-data/taxonomies-schemas/standard-taxonomies/investment-companies        |
| SRO Taxonomies                      | https://www.sec.gov/data-research/standard-taxonomies/self-regulatory-organizations                                  |
| SBS/SBSEF Taxonomies                | https://www.sec.gov/data-research/standard-taxonomies/security-based-swap-data-repositories-and-execution-facilities |
| NRSRO Taxonomies                    | https://www.sec.gov/data-research/standard-taxonomies/nationally-recognized-statistical-rating-organizations         |
| Taxonomies and Schemas (all)        | https://www.sec.gov/data-research/structured-data/taxonomies-schemas                                                 |
| Technical Specifications            | https://www.sec.gov/submit-filings/technical-specifications                                                          |
| EDGAR Filer Manual                  | https://www.sec.gov/submit-filings/edgar-filer-manual                                                                |
| EDGAR Filer Manual Vol. II          | https://www.sec.gov/files/edgar/filermanual/edgarfm-vol2-v77.pdf                                                     |
| Ch. 6: Interactive Data             | https://www.sec.gov/files/edgar/filermanual/efmvol2-c6.pdf                                                           |
| Structured Disclosure History       | https://www.sec.gov/data-research/structured-data/structured-disclosure-sec-history-rulemaking                       |
| Taxonomy XML Machine-Readable Index | https://www.sec.gov/info/edgar/edgartaxonomies.xml                                                                   |
| XBRL Taxonomy Files (SEC)           | https://xbrl.sec.gov/                                                                                                |
| FASB US GAAP Taxonomy               | https://fasb.org/projects/fasb-taxonomies                                                                            |
| IFRS Taxonomy                       | https://www.ifrs.org/issued-standards/ifrs-taxonomy/                                                                 |
| XBRL-to-JSON Converter              | https://sec-api.io/docs/xbrl-to-json-converter-api                                                                   |
