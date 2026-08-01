# Cinderhaven Provisions — Ten Decisions: Case Study Findings

**Composite case study.** Cinderhaven Provisions is a fictional ~$25M specialty food brand used
throughout the Lailara LLC portfolio to illustrate the decisions growing brands make blind.
All figures derive from the Cinderhaven synthetic dataset; no real client data is represented.

---

## Decision 1: SKU Rationalization
**Source repo:** `where-the-money-comes-from`, `src/data/channels.json` and `short-ship-cost/web/public/data/cost_by_sku.json`
**Dollar figure:** $215,000 over three years — highest-cost single SKU (CHP-PS-009, Maple Syrup Grade A), driven primarily by forgone revenue on shorted units
**Finding:** "Cinderhaven's top-performing SKU generated 23 times the short-shipping cost exposure of the lowest — a spread invisible until you model which SKUs are actually driving demand versus which ones are consuming fulfillment capacity."
**Before/After:** N/A — this is a point-in-time analysis of the FY2024–2026 window. The before state is operating without per-SKU cost attribution; the after state is knowing which SKUs to cut or protect before making the next ranging decision.

---

## Decision 2: Product Data Health
**Source repo:** `product-data-health-audit`
**Dollar figure:** $93,000 a year in retailer chargebacks traced directly to product data defects
**Finding:** "~$93K/yr in chargeback cost attributable to data-quality defects — avoidable with a one-time catalog audit."
**Before/After:** Before: GTIN failures present across 24% of SKUs, chargebacks concentrated in worst-quality products. After: clean data state with verified GS1 registry entries, chargeback run rate drops to near zero.

---

## Decision 3: Deduction Recovery
**Source repo:** `retailer-deduction-recovery`
**Dollar figure:** $1.35M in deductions across 16,917 line items over 36 months; ~15% of deduction dollars recovered; ~42% win rate per disputed dollar, but only ~35% of deductions are ever disputed; 3,357 chargebacks (2,873 retailer + 484 distributor); ~$380K/yr operational deduction waste
**Finding:** "Cinderhaven wins 42% of the disputes it files. The problem isn't winning — it's filing. Two-thirds of deductions are written off without a fight."
**Before/After:** Before: ~15% of deduction dollars recovered — not because disputes fail, but because most are never filed; ~65% of deductions go uncontested ($877,620 in silent write-offs); 3,357 chargebacks over 36 months. After: systematic dispute process with evidence templates and retailer-specific response calendars targeting >50% recovery.

---

## Decision 4: Fulfillment Reliability
**Source repo:** `short-ship-cost`, `web/public/data/validation.json`
**Dollar figure:** $894K in total fulfillment shortfall costs over 36 months at 99.2% retailer / 99.5% distributor fill — $523,326 in forgone revenue, $164,543 in compliance fines, $118,814 in chargebacks, $87,490 in deductions; ~$298K/yr across four dimensions
**Finding:** "99% unit fill still costs $300K/yr — the gap between unit fill and in-full is where the money hides. Cinderhaven's internal fill rate looks like excellence; retailers score them at 85%."
**Before/After:** Before: no visibility into cost of shorts because the legacy system overwrote original orders with shipped quantities. After: 99.2% retailer fill rate costs ~$298K/yr — every dollar traces to a platform event or a published fine schedule. Internal fill 99.2%; retailer-scored OTIF 88.2% blended; the 14.8-pt gap is Walmart-specific (99.2 vs. 84.5, computed on unrounded rates); $57K/yr in OTIF exposure ($23,697 fines + $33,500 velocity damage).

---

## Decision 5: EDI Compliance
**Source repo:** `edi-preflight`, `rules/walmart_856.yaml` and `src/validate_856_walmart.py`
**Dollar figure:** $500 per load for a missing or late ASN; $100 per case for missing or invalid SSCC-18 barcodes; $100 per item for catch-weight violations — exposure scales directly with shipment frequency
**Finding:** "Every ASN Cinderhaven sent without a valid SSCC-18 barcode carried a $100-per-case chargeback that a pre-flight check would have caught in under 60 seconds — no EDI specialist required."
**Before/After:** Before: ASN errors caught only after chargeback arrival, typically 30–60 days post-shipment with a narrow dispute window. After: three-layer pre-flight validation (structural, field-level, retailer-specific) catches blocking and chargeback-causing errors before the trailer gates at the DC.

---

## Decision 6: Channel Profitability
**Source repo:** `channel-profitability-analysis` (also cross-referenced in `where-the-money-comes-from`, `src/data/channels.json`)
**Dollar figure:** 3.01 margin points between Whole Foods (82.65%) and Costco (79.64%) — the best and worst retail channels. Two different metrics, opposite directions: distributors realize 90.16 cents of cash per invoiced dollar vs. retail's 81.1 (fewer deductions), but on contribution after COGS and trade, retail runs 51.0% vs. distribution's 45.6% — worth ~$54,000 more contribution per $1M of revenue routed through retail.
**Finding:** "Cinderhaven's best-performing retail channel delivered 3 margin points more than the worst — a gap invisible without per-channel contribution accounting."
**Before/After:** Before: capital allocation driven by gross revenue rank (Walmart #1). After: the ranking splits by metric — distributors realize more cash per invoiced dollar (90¢ vs. 81¢), but contribution after COGS and trade runs the other way (retail 51.0% vs. distribution 45.6%), worth ~$54,000 per $1M of revenue routed. Per revenue dollar, not a return on capital.

---

## Decision 7: Revenue Lifecycle
**Source repo:** `contract-to-cash`
**Dollar figure:** 87¢ per dollar invoiced reaches cash; B2B leakage 12.8%; time-to-cash 24–28 days (combined leakage dollar figure pending fresh pull from contract-to-cash — pipeline lumps recoverable layers into one unclassified bucket)
**Finding:** "Cinderhaven was losing ~13 cents on every dollar invoiced between invoice generation and cash receipt."
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
**Dollar figure:** Year 1 net = -$36,320; peak cash trough Month 1 = -$156,352; working capital required $156,352
**Finding:** "When Cinderhaven modeled their Walmart launch, the first-year economics showed a $156,352 peak cash requirement hitting in the very first month."
**Before/After:** Before: launch decision made on gross margin and velocity projections without modeling the full cash flow waterfall (slotting, Net-30 terms, trade spend, OTIF reserve). After: full 12-month P&L and cash flow model showing peak trough and minimum working capital before saying yes to the buyer.

---

## Decision 10: Weekly Pulse
**Source repo:** `monday-morning-report`
**Dollar figure:** Cash position range $1.5M–$2.5M over 12 weeks; disputed AR declined from $195,000 to $88,000 (a $107,000 reduction); recovered shelf position worth $80,000–$150,000 in annual velocity
**Finding:** "In the 12 weeks after Cinderhaven implemented the Monday Morning Report, disputed AR fell from $195,000 to $88,000 — a $107,000 reduction driven by consistent weekly attention to the right three numbers."
**Before/After:** Before: weekly management meeting reviewed revenue and shipments; disputed AR, deduction pipeline, and at-risk shelf positions had no dedicated owner or cadence. After: 12-week rolling report surfaces cash position, disputed AR, and shelf velocity weekly — three numbers that compound if ignored and recover quickly with attention.

---

*All figures are from the Cinderhaven Provisions composite case study. Sources cited are Lailara LLC portfolio repos. Dollar amounts are specific to the synthetic dataset parameters documented in each repo.*
