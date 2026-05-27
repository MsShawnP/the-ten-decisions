# Cinderhaven Provisions — Ten Decisions: Case Study Findings

**Composite case study.** Cinderhaven Provisions is a fictional ~$25M specialty food brand used
throughout the Lailara LLC portfolio to illustrate the decisions growing brands make blind.
All figures derive from the Cinderhaven synthetic dataset; no real client data is represented.

---

## Decision 1: SKU Rationalization
**Source repo:** `where-the-money-comes-from`, `src/data/channels.json` and `short-ship-cost/web/public/data/cost_by_sku.json`
**Dollar figure:** $1,066,480 — highest-cost single SKU (Extra Virgin Olive Oil, CHP-PS-004) in short-shipping costs alone; bottom-quartile SKUs averaged $710,000 each in the same period
**Finding:** "Cinderhaven's top-performing SKU generated 23 times the short-shipping cost exposure of the lowest — a spread invisible until you model which SKUs are actually driving demand versus which ones are consuming fulfillment capacity."
**Before/After:** N/A — this is a point-in-time analysis of the FY2024–2026 window. The before state is operating without per-SKU cost attribution; the after state is knowing which SKUs to cut or protect before making the next ranging decision.

---

## Decision 2: Product Data Health
**Source repo:** `product-data-health-audit`
**Dollar figure:** $60,000/year ($5,000/month run rate in chargebacks from data defects)
**Finding:** "Cinderhaven's product data failures were generating approximately $60,000 per year in chargebacks — avoidable with a one-time data audit."
**Before/After:** Before: GTIN/UPC failures present across the full catalog, chargebacks accumulating monthly. After: clean data state with verified GS1 registry entries, chargeback run rate drops to near zero.

---

## Decision 3: Deduction Recovery
**Source repo:** `retailer-deduction-recovery`
**Dollar figure:** $1,020,000 in deductions never disputed (9,757 individual deductions); $534,903.85 total annual deduction volume; 16.52% recovery rate
**Finding:** "Cinderhaven had $1.02 million in disputed deductions that were never contested — 83% of deductions went unrecovered because the team lacked the systematic process to fight them."
**Before/After:** Before: 12,604 labor hours (6.06 FTE equivalent) spent on deduction management with 16.52% recovery. After: systematic dispute process with evidence templates and retailer-specific response calendars targeting >50% recovery.

---

## Decision 4: Fulfillment Reliability
**Source repo:** `short-ship-cost`, `web/public/data/cost_summary.json` and `web/public/data/meta.json`
**Dollar figure:** $33,128,550 in total short-shipping costs over three years ($11,042,850/year); 69.19% overall fill rate; $2,055,467 in OTIF fines; $6,422,619 in deauthorization risk
**Finding:** "Cinderhaven was shipping at a 69% fill rate — leaving $11 million in annual cost exposure across lost revenue, OTIF fines, and deauthorization risk that never appeared on a P&L because the original orders had been overwritten."
**Before/After:** Before: fill rate 69.19%, no visibility into cost of shorts because the legacy system overwrote original orders. After: 90% fill rate scenario recovers $20.6M of the $33.1M three-year cost; deauthorization risk drops from $6.4M to $3.7M.

---

## Decision 5: EDI Compliance
**Source repo:** `edi-preflight`, `rules/walmart_856.yaml` and `src/validate_856_walmart.py`
**Dollar figure:** $500 per load for a missing or late ASN; $100 per case for missing or invalid SSCC-18 barcodes; $100 per item for catch-weight violations — exposure scales directly with shipment frequency
**Finding:** "Every ASN Cinderhaven sent without a valid SSCC-18 barcode carried a $100-per-case chargeback that a pre-flight check would have caught in under 60 seconds — no EDI specialist required."
**Before/After:** Before: ASN errors caught only after chargeback arrival, typically 30–60 days post-shipment with a narrow dispute window. After: three-layer pre-flight validation (structural, field-level, retailer-specific) catches blocking and chargeback-causing errors before the trailer gates at the DC.

---

## Decision 6: Channel Profitability
**Source repo:** `channel-profitability-analysis` (also cross-referenced in `where-the-money-comes-from`, `src/data/channels.json`)
**Dollar figure:** 3.01 margin points between Whole Foods (82.65%) and Costco (79.64%) — the best and worst retail channels; distributors blended at 90.16% vs. retail blended at 81.1%; $90,844 more contribution on the same $1M invested in distribution vs. retail
**Finding:** "Cinderhaven's best-performing retail channel delivered 3 margin points more than the worst — a gap invisible without per-channel contribution accounting."
**Before/After:** Before: capital allocation driven by gross revenue rank (Walmart #1). After: contribution-margin ranking reveals distributor channels at 90¢/dollar vs. retail at 81¢/dollar — an 11.2% difference in returns on the same incremental dollar invested.

---

## Decision 7: Revenue Lifecycle
**Source repo:** `contract-to-cash`
**Dollar figure:** $2,178,000 in combined leakage; 86.5¢ per dollar invoiced reaches cash; B2B leakage 12.5%; time-to-cash 22–29 days
**Finding:** "Cinderhaven was losing 13.5 cents on every dollar invoiced — $2.178M in combined leakage — between invoice generation and cash receipt."
**Before/After:** Before: leakage measured only as the difference between gross revenue and bank deposits, with no attribution to deductions, timing, or process gaps. After: full invoice-to-cash waterfall mapped by leakage type, enabling targeted intervention at the highest-value gaps.

---

## Decision 8: Retail Readiness
**Source repo:** `retail-readiness-scorecard`, `scoring_engine/retailers/walmart.yaml` and `scoring_engine/score.py`
**Dollar figure:** 3% of COGS per non-compliant PO (Walmart OTIF penalty); 8–12 weeks remediation time for a Red EDI dimension; GFSI certification failure = hard rejection at Whole Foods (complete launch block regardless of all other scores)
**Finding:** "When Cinderhaven ran the retail readiness scorecard before their Walmart pitch, a Red score on EDI capability revealed an 8-to-12-week gap they would have discovered on their first failed delivery — not before signing the PO."
**Before/After:** Before: readiness assessed informally by the sales team; EDI, FSMA 204, and GDSN gaps discovered reactively after buyer commitment. After: structured 8-dimension assessment (Product Data, Syndication, EDI, Fulfillment, Financial, Production, Compliance, Team) with gate questions that surface hard launch blockers before the retailer conversation.

---

## Decision 9: Launch Economics
**Source repo:** `cost-of-saying-yes`
**Dollar figure:** Year 1 net = -$36,320; peak cash trough Month 4 = -$165,000; break-even Month 9; working capital required $165,000
**Finding:** "When Cinderhaven modeled their Walmart launch, the first-year economics showed a $165,000 peak cash requirement and a break-even that didn't arrive until Month 9."
**Before/After:** Before: launch decision made on gross margin and velocity projections without modeling the full cash flow waterfall (slotting, 60-day terms, trade spend, OTIF reserve). After: full 12-month P&L and cash flow model showing peak trough, break-even timeline, and minimum working capital before saying yes to the buyer.

---

## Decision 10: Weekly Pulse
**Source repo:** `monday-morning-report`
**Dollar figure:** Cash position range $1.5M–$2.5M over 12 weeks; disputed AR declined from $195,000 to $88,000 (a $107,000 reduction); recovered shelf position worth $80,000–$150,000 in annual velocity
**Finding:** "In the 12 weeks after Cinderhaven implemented the Monday Morning Report, disputed AR fell from $195,000 to $88,000 — a $107,000 reduction driven by consistent weekly attention to the right three numbers."
**Before/After:** Before: weekly management meeting reviewed revenue and shipments; disputed AR, deduction pipeline, and at-risk shelf positions had no dedicated owner or cadence. After: 12-week rolling report surfaces cash position, disputed AR, and shelf velocity weekly — three numbers that compound if ignored and recover quickly with attention.

---

*All figures are from the Cinderhaven Provisions composite case study. Sources cited are Lailara LLC portfolio repos. Dollar amounts are specific to the synthetic dataset parameters documented in each repo.*
