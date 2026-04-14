# Examples for SEC & EDGAR Data Analysis

![banner](https://sec-api.io/v2/media/product/gh-repo-banner-card-1500x400.png)

---

A collection of example notebooks showing how to query, download, extract, and analyze SEC EDGAR filings using the [`sec-api`](https://sec-api.io) Python package.

## Insider Trades

- [Form 4 - Insider Trading API Example](./notebooks/form-4/insider-trading-api-example.ipynb) | [Docs](https://sec-api.io/docs/insider-ownership-trading-api)
- [Form 144 - Restricted and Control Securities Sales](./notebooks/form-144/form-144.ipynb) | [Docs](https://sec-api.io/docs/form-144-restricted-sales-api)

## Ownership Data APIs

- **Form 13F** | [Docs](https://sec-api.io/docs/form-13-f-filings-institutional-holdings-api)
  - [Portfolio Holdings & Cover Pages Python Example](./notebooks/form-13f/form-13f-python-example.ipynb)
  - [Tutorial](./notebooks/form-13f/13f-tutorial.ipynb)
- [Form 13D / 13G - Activist Investor Filings](./notebooks/form-13d-13g/form-13d-13g-api-examples.ipynb) | [Docs](https://sec-api.io/docs/form-13d-13g-search-api)

## Investment Companies

- [Form N-CEN - Annual Reports](./notebooks/form-ncen/form-ncen.ipynb) | [Docs](https://sec-api.io/docs/form-ncen-api-annual-reports-investment-companies)
- [Form N-PX - Proxy Voting Records](./notebooks/form-npx/form-npx-tutorial-website.ipynb) | [Docs](https://sec-api.io/docs/form-npx-proxy-voting-records-api)
- **Form N-PORT** | [Docs](https://sec-api.io/docs/n-port-data-api)
  - [Portfolio Holdings Quick Start](./notebooks/form-nport/quick-start.ipynb)
  - [API Reference](./notebooks/form-nport/form-nport-api.ipynb)
  - [Extract ETF Constituents](./notebooks/form-nport/extract-etf-constituents.ipynb)
  - [Swap Derivative Example](./notebooks/form-nport/swap-derivative-example.ipynb)

## Investment Advisers — IAs, Firms (SEC & State Registered), Individuals, ERAs

- [Form ADV - Python Examples](./notebooks/form-adv/form-adv-python-example.ipynb) | [Docs](https://sec-api.io/docs/investment-adviser-and-adv-api)

## Public Companies Datasets

- [Audit Fees API](./notebooks/audit-fees/audit-fees.ipynb) | [Docs](https://sec-api.io/docs/audit-fees-api)
- [Directors & Board Members API](./notebooks/directors-board-members-api/quick-start.ipynb) | [Docs](https://sec-api.io/docs/directors-and-board-members-data-api)
- **Executive Compensation API** | [Docs](https://sec-api.io/docs/executive-compensation-api)
  - [Quick Start](./notebooks/executive-compensation-api/quick-start.ipynb)
  - [Ticker Lookup](./notebooks/executive-compensation-api/ticker-lookup.ipynb)
  - [Example](./notebooks/executive-compensation-api/example-2.ipynb)
  - [Export to Excel](./notebooks/executive-compensation-api/export-to-excel.ipynb)
- [Subsidiary API (Exhibit 21)](./notebooks/subsidiary-api/subsidiary-api-example.ipynb) | [Docs](https://sec-api.io/docs/subsidiary-api)
- [Float API - Outstanding Shares](./notebooks/float-api/float-api-example.ipynb) | [Docs](https://sec-api.io/docs/outstanding-shares-float-api)
- [Mapping API - Ticker / CIK / CUSIP](./notebooks/mapping-api/map-ticker-cik-cusip.ipynb) | [Docs](https://sec-api.io/docs/mapping-api)

## Form 8-K — Structured Material Events

- [Analyze 8-K Filings & Material Event Disclosure Activity](./notebooks/form-8k/8k-tutorial.ipynb) | [Docs](https://sec-api.io/docs/form-8k-data-search-api)
- [Find Filings by Item Number (8-K, Form D)](./notebooks/form-8k/filings-by-item.ipynb)
- **Item-Specific Tutorials**
  - [Item 4.01 - Auditor and Accountant Changes](./notebooks/form-8k/8k-item-4-01-tutorial-website.ipynb) | [Docs](https://sec-api.io/docs/form-8k-data-item4-1-search-api)
  - [Item 4.02 - Non-Reliance Disclosures](./notebooks/form-8k/8k-item-4-02-tutorial-website.ipynb) | [Docs](https://sec-api.io/docs/form-8k-data-search-api)
  - [Item 5.02 - Change of Directors, Board Members and Compensation Plans](./notebooks/form-8k/8k-item-5-02-tutorial-website.ipynb) | [Docs](https://sec-api.io/docs/form-8k-data-item5-2-search-api)
- **Exhibit Downloads**
  - [Download Press Releases from 8-K Filings](./notebooks/form-8k/download-press-releases.ipynb)
  - [Download Ex-99 Exhibits from 8-K Filings](./notebooks/form-8k/download-ex-99-exhibits.ipynb)

## Offerings & Registration Statements

- [Form C - Crowdfunding Campaigns](./notebooks/form-c/form-c-tutorial-website.ipynb) | [Docs](https://sec-api.io/docs/form-c-crowdfunding-api)
- [Form D - Exempt Offerings & Private Placements](./notebooks/form-d/form-d-tutorial-website.ipynb) | [Docs](https://sec-api.io/docs/form-d-xml-json-api)
- [Form 1A / 1K / 1Z - Regulation A Offering Statements](./notebooks/reg-a/reg-a-tutorial-website.ipynb) | [Docs](https://sec-api.io/docs/reg-a-offering-statements-api)
- **Registration Statements & Prospectuses (S-1, 424B)** | [Docs](https://sec-api.io/docs/form-s1-424b4-data-search-api)
  - [Search S-1 & 424B Filings](./notebooks/registration-statements/registration-statements-prospectus.ipynb)
  - [424B4 Prospectuses by Year](./notebooks/registration-statements/424b4-prospectuses-by-year.ipynb)
  - [Top 20 Largest Offerings by Year](./notebooks/registration-statements/top-20-largest-offerings.ipynb)
  - [Most-Used Law Firms in Securities Offerings](./notebooks/registration-statements/top-law-firms.ipynb)

## Enforcement Actions, Proceedings, AAERs

- [SEC Litigation Releases](./notebooks/sec-litigation-releases/sec_litigation_releases.ipynb) | [Docs](https://sec-api.io/docs/sec-litigation-releases-database-api)
- [SEC Administrative Proceedings](./notebooks/sec-administrative-proceedings/sec-administrative-proceedings.ipynb) | [Docs](https://sec-api.io/docs/sec-administrative-proceedings-database-api)
- [Accounting and Auditing Enforcement Releases (AAERs)](./notebooks/sec-aaers/sec-aaers.ipynb) | [Docs](https://sec-api.io/docs/aaer-database-api)
- [SEC Comment Letters - Download & Analyze](./notebooks/sec-comment-letters/download-sec-comment-letters.ipynb) | [Docs](https://sec-api.io/datasets/sec-comment-letters)

## EDGAR Filing Search & Query

- **Query API** | [Docs](https://sec-api.io/docs/query-api)
  - [Quick Start](./notebooks/query-api/quick-start.ipynb)
  - [Lucene Syntax Tutorial](./notebooks/query-api/lucene-syntax-tutorial.ipynb)
  - [Search Filings by Ticker, Form Type, Date](./notebooks/query-api/search-filings-by-ticker-form-type-date.ipynb)
  - [Locate Filing URLs](./notebooks/query-api/locate-filings-urls.ipynb)
- [Full-Text Search API - Quick Start](./notebooks/full-text-search-api/quick-start.ipynb) | [Docs](https://sec-api.io/docs/full-text-search-api)

## Filing Download, Extraction & Rendering

- **Download API** | [Docs](https://sec-api.io/docs/sec-filings-render-api)
  - [Quick Start](./notebooks/download-api/quick-start.ipynb)
  - [Download XML Files](./notebooks/download-api/download-xml-files.ipynb)
  - [Download SEC Filings from EDGAR](./notebooks/download-api/download-sec-filings-from-edgar.ipynb)
  - [Download Material Contracts (Ex-10)](./notebooks/material-contracts/download-material-contracts.ipynb)
- **PDF Generator API** | [Docs](https://sec-api.io/docs/sec-filings-render-api)
  - [Quick Start](./notebooks/pdf-generator-api/download-filings-as-pdf-quick-start.ipynb)
  - [Download Filings as PDFs](./notebooks/pdf-generator-api/download-filings-as-pdf.ipynb)
- **Extractor API** | [Docs](https://sec-api.io/docs/sec-filings-item-extraction-api)
  - [Quick Start](./notebooks/extractor-api/quick-start.ipynb)
  - [Extract 10-K Sections](./notebooks/extractor-api/extract-sections-10-k.ipynb)
  - [Extract 10-Q Sections](./notebooks/extractor-api/extract-sections-10-q.ipynb)
  - [Extract 8-K Sections](./notebooks/extractor-api/extract-sections-8-k.ipynb)
  - [Download Multiple 10-K Sections](./notebooks/extractor-api/extract-multiple-10-k-sections.ipynb)
  - [Clean Extracted Sections](./notebooks/extractor-api/clean-extracted-sections.ipynb)
  - [Extract Textual Data from 10-K](./notebooks/extractor-api/extract-textual-data-10-k.ipynb)

## XBRL Financial Data

- **XBRL-to-JSON API** | [Docs](https://sec-api.io/docs/xbrl-to-json-converter-api)
  - [XBRL with Python](./notebooks/xbrl-to-json-api/xbrl-with-python.ipynb)
  - [Extract Financial Statements](./notebooks/xbrl-to-json-api/extract-financial-statements.ipynb)
  - [Google Revenue Analysis](./notebooks/xbrl-to-json-api/google-revenue-analysis.ipynb)
- **XBRL Source Files**
  - [Download XBRL Files from EDGAR](./notebooks/xbrl-files/download-xbrl-files.ipynb)
  - [Download XSD URLs](./notebooks/xbrl-files/download-xsd-urls.ipynb)
- [SEC EDGAR Form Types Supporting XBRL](./resources/sec-edgar-form-types-supporting-xbrl/sec-edgar-form-types-supporting-xbrl.ipynb)

## Financial Reports & Bulk Downloads

- **Financial Statements as Excel Files**
  - [Quick Example](./notebooks/financial-reports-excel/download-financial-statements.ipynb)
  - [Full Walkthrough](./notebooks/financial-reports-excel/download-financial-statements-tutorial.ipynb)
- **Russell 3000 - Bulk Download 10-K Filings**
  - [Quick Example](./notebooks/russell-3000/download-10k-filings-russell-3000.ipynb)
  - [Full Walkthrough](./notebooks/russell-3000/download-10k-filings-russell-3000-tutorial.ipynb)

## EDGAR Analytics & Utilities

- [EDGAR Filing Trends 1994–2022](./notebooks/filing-trends/filing-trends-tutorial.ipynb)
- [EDGAR Filer Analysis](./notebooks/filer-analysis/edgar-filer-analysis.ipynb)
- [List Fiscal Period End Dates](./notebooks/fiscal-period/list-fiscal-period-end-dates.ipynb)
- [Export Filing Metadata to CSV](./notebooks/csv-export/csv-export.ipynb)

## Research & Market Data

- [Fama-French Factor Model](./notebooks/research/fama-french-factor-model.ipynb)
- [Testing Statistical Significance in Financial Data](./notebooks/research/testing-statistical-significance.ipynb)
- [Fed Funds Rate Projections](./notebooks/fed-funds/fed-funds-rate-projections.ipynb)
