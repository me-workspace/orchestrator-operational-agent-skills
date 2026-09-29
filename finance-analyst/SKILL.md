---
name: finance-analyst
description: Use this skill for any finance/accounting work - "laporan keuangan", "cashflow", "runway", "harga/pricing", "unit economics", "MRR/ARR/churn", budgeting, invoice/AR review, forecasting, or evaluating whether a business/product is profitable. Covers SaaS metrics, cashflow analysis, and pricing models. Do NOT use for tax filing advice or audited financial statements - flag those for a licensed accountant.
---

# Finance Analyst

Numbers first, narrative second. Every claim must trace to a source figure; state assumptions explicitly and separately from data.

## Ground rules
- Never mix currencies silently; state currency and period on every figure.
- Use consistent period buckets (calendar month) before comparing.
- Distinguish **cash** (money moved) vs **accrual** (earned/owed) - say which basis you're on.
- Round in presentation only, never mid-calculation. Money math: integers in smallest unit or decimal type, never float.

## SaaS / subscription metrics (definitions to use verbatim)
- **MRR** = sum of active subscriptions' monthly-normalized price. New / expansion / contraction / churned MRR reported separately.
- **Churn (logo)** = customers lost ÷ customers at period start. **Revenue churn** uses MRR. Report both.
- **ARPU** = MRR ÷ active customers. **LTV** ≈ ARPU × gross margin ÷ monthly revenue churn (state this is an approximation).
- **CAC** = full sales+marketing spend ÷ new customers. Healthy: LTV/CAC ≥ 3, CAC payback ≤ 12 months.
- **Runway** = cash ÷ average monthly net burn (last 3 months, not best month).

## Standard deliverable - monthly finance snapshot
```
# Snapshot <bulan>
Kas akhir: X | Net burn: X | Runway: X bulan
MRR: X (new +a, expansion +b, contraction -c, churn -d) | Growth MoM: x%
Pelanggan aktif: N | Logo churn: x% | ARPU: X
Top 3 pengeluaran: ...
Perhatian: <anomali, pelanggan telat bayar, biaya naik tak wajar>
Asumsi & sumber data: ...
```

## Pricing / unit economics analysis
1. Compute true unit cost: infra + payment fees + support time + COGS per unit/customer.
2. Contribution margin per tier; flag any tier with margin < 50% for a software product.
3. Price recommendation: anchor to value delivered and competitor range, not cost-plus alone. Give 2-3 scenarios with break-even volume each.

## Red flags to always surface
Negative gross margin customers · churn trending up 2+ months · one customer > 25% of revenue · AR older than 60 days · spend category growing faster than revenue · runway < 6 months.
