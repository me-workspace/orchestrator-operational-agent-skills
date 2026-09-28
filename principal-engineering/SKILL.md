---
name: principal-engineering
description: Use this skill when engineering judgment above the code level is needed — "menurutmu arsitekturnya gimana", "trade-off nya apa", "kapan refactor", "monolith vs microservice", "build vs buy", technical debt decisions, scaling decisions, mentoring-level explanations of engineering principles, or reviewing a technical direction. The principal-engineer brain: principles, trade-offs, and how to decide. Do NOT use for executing the code itself or for process/lifecycle questions (sdlc-master).
---

# Principal Engineering

A principal engineer's output is not code — it is **decisions that stay correct as the system grows**, and the written reasoning that lets others check them. Always give a recommendation with its trade-offs, never a menu without an opinion.

## Core principles (apply in this priority order)
1. **Correctness before cleverness** — code that is obviously right beats code that is impressively fast. Optimize only after measuring.
2. **Simplicity is a feature with a cost curve** — every abstraction, service, and dependency must pay rent. The question is never "could this help?" but "what breaks or slows down if we add it?"
3. **Reversibility rules decision speed** — reversible decisions (naming, internal structure): decide fast, iterate. Irreversible ones (data model, public API, vendor lock-in, language): slow down, write it up, get review.
4. **Design for deletion** — the best modules are the ones you can rip out. Boundaries > cleverness inside them.
5. **Boring technology wins by default** — new tech must be dramatically better, not marginally cooler. One innovation token per project.
6. **Data outlives code** — schema and stored-data decisions deserve 10× the scrutiny of code decisions; migrations are where systems die.
7. **Make the right thing the easy thing** — if the team keeps doing it wrong, fix the tooling/defaults, not the people.

## Decision framework (for any significant technical choice)
```
Keputusan: <satu kalimat>
Reversible? <ya → putuskan cepat / tidak → tulis lengkap>
Opsi (2–3) — untuk masing-masing:
  biaya sekarang · biaya 12 bulan · risiko terburuk · exit path
Rekomendasi + alasan utama (satu paragraf)
Sinyal untuk meninjau ulang: <metrik/kejadian yang membatalkan keputusan ini>
```

## Standard calls (defaults with the reasoning)
- **Monolith vs microservices**: modular monolith sampai ada bukti butuh pisah (tim > ~8 engineer per domain, atau kebutuhan scaling/deploy yang benar-benar berbeda). Microservices menukar kompleksitas kode dengan kompleksitas operasional — hanya untung kalau punya kapasitas ops-nya.
- **Build vs buy**: buy/pakai open source untuk apa pun yang bukan pembeda bisnis (auth, billing, email, monitoring). Build hanya di area yang jadi moat. Hitung biaya maintain, bukan biaya bikin.
- **Refactor vs rewrite**: rewrite hampir selalu salah untuk sistem yang hidup — strangler pattern (kikis per bagian di balik interface stabil). Rewrite penuh hanya bila platform mati atau biaya perubahan sudah lebih besar dari nilai sistem.
- **Technical debt**: debt itu sah kalau diambil sadar + tercatat + ada rencana bayar. Debt register: item · bunga (apa yang melambat/berisiko tiap sprint) · pemicu wajib bayar. Bayar debt yang bunganya tertinggi, bukan yang paling menyebalkan.
- **Scaling**: ukur dulu. Urutan murah→mahal: index & query fix → caching → read replica → queue untuk beban async → baru sharding/pemecahan service. Kebanyakan "masalah skala" adalah query N+1.

## Estimating like a principal
Estimasi = rentang + asumsi, bukan angka tunggal. Pecah sampai unit ≤ 2 hari; total × 1.5 untuk integrasi & hal tak terduga; sebut eksplisit apa yang TIDAK termasuk. Estimasi yang meleset > 50% = sinyal pemahaman masalah salah — berhenti dan re-scope, jangan lembur menutupi.

## Reviewing a technical direction (someone else's design)
1. Restate the problem in your own words — mismatch here explains most bad designs.
2. Attack the data model first, then failure modes, then the happy path.
3. Ask "what happens at 10× load / 10× data / when X is down?" for each component.
4. Praise what's good explicitly; frame issues as trade-offs, not verdicts; distinguish "harus diubah" vs "preferensiku".

## Communication duty
Every significant decision → short written record (context, options, choice, why). Verbal architecture is a rumor. When explaining to non-engineers: lead with impact and cost in their terms (waktu, uang, risiko), keep mechanism to one sentence unless asked.
