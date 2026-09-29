# Agent Skills untuk Bisnis dan Engineering

> 25 skill portabel yang mengubah asisten AI generik menjadi satu tim kerja: bangun software dari hulu ke hilir dan jalankan bisnis di sekelilingnya, dari PRD dan code review sampai finance, marketing, dan HR.

![Skills](https://img.shields.io/badge/skills-25-2563eb)
![License](https://img.shields.io/badge/license-MIT-16a34a)
![Spec](https://img.shields.io/badge/spec-Agent%20Skills-111827)
![Claude Code](https://img.shields.io/badge/works%20with-Claude%20Code-8b5cf6)
![PRs welcome](https://img.shields.io/badge/PRs-welcome-f59e0b)

Sebuah **Skill** adalah folder berisi file `SKILL.md`: prosedur terfokus dan bisa dipakai ulang yang dimuat agen hanya saat relevan. Repo ini kumpulan kurasi skill semacam itu, ditulis mengikuti [standar terbuka Agent Skills](https://github.com/anthropics/skills) dari Anthropic, jadi bisa langsung dipasang di Claude Code, Claude Agent SDK, atau runtime agen apa pun yang membaca `SKILL.md`.

Ini lebih dari sekadar tumpukan prompt. Tiap skill adalah checklist, rubrik, atau pohon keputusan dengan quality gate, dan [`AGENTS.md`](./AGENTS.md) menunjukkan cara menyusunnya jadi perusahaan 8 agen (COO plus tujuh spesialis) tanpa skill saling berebut konteks.

---

## Kenapa pack ini

- **Prosedur, bukan prosa.** Skill menghasilkan output yang konsisten dan bisa diperiksa, bukan teks bebas.
- **Deskripsi kaya pemicu.** Tiap `SKILL.md` menyatakan persis kapan harus menyala, dan kapan TIDAK, sehingga salah-trigger berkurang saat banyak skill terpasang.
- **Hemat konteks.** Hanya name dan description yang duduk di konteks; body dimuat saat dibutuhkan. Pasang belasan skill tanpa membanjiri jendela konteks.
- **Jujur secara desain.** Skill yang menyentuh pajak, hukum, atau uang membawa aturan draft-until-verified di dalam skill itu sendiri.
- **Portabel.** Kalau agen Anda bisa membaca `SKILL.md`, ia bisa memakai skill ini.

---

## Mulai cepat (Claude Code)

```bash
git clone https://github.com/me-workspace/orchestrator-operational-agent-skills.git
cd orchestrator-operational-agent-skills

# Satu skill, lingkup project
cp -r marketing-growth  /path/ke/project-anda/.claude/skills/

# Atau pasang satu loadout peran, global
cp -r prd-creator project-timeline-creator strategic-approach admin-ops  ~/.claude/skills/
```

Saat berikutnya ada permintaan yang cocok ("tulis campaign brief", "buat PRD", "review diff ini"), agen memuat skill-nya otomatis.

> Jangan pasang semua 25 ke satu agen. Metadata tiap skill yang terpasang tetap duduk di konteks. Pilih loadout per peran. Lihat [`AGENTS.md`](./AGENTS.md) untuk desain lengkapnya.

---

## Daftar skill

### Software dan AI (SDLC penuh)
| Skill | Fungsi |
|---|---|
| [`sdlc-master`](./sdlc-master) | Lifecycle end-to-end: fase dan gate, tech design doc, Definition of Done, branching, testing strategy |
| [`principal-engineering`](./principal-engineering) | Judgment level principal: prinsip, trade-off, decision framework, standard calls |
| [`strategic-approach`](./strategic-approach) | Memilih pendekatan: framing, tiga opsi beragam, rekomendasi plus kill criteria, MVP scoping |
| [`prd-creator`](./prd-creator) | PRD lengkap: goals terukur, non-goals wajib, acceptance criteria Given/When/Then |
| [`project-timeline-creator`](./project-timeline-creator) | Timeline: breakdown 2 hari atau kurang, dependency, buffer 1.5x, critical path, protokol slip |
| [`project-audit`](./project-audit) | Audit project: 7 dimensi berskor, metode evidence-based, laporan berprioritas plus verdict |
| [`code-review-hardening`](./code-review-hardening) | Review kode: correctness dan security, verifikasi sebelum lapor, rubrik severity |
| [`secure-deploy-ops`](./secure-deploy-ops) | Deploy: backup pra-deploy, diff live vs staged, smoke test, hardening baseline |
| [`incident-debugging`](./incident-debugging) | Debugging produksi: evidence-first, hipotesis diskriminatif, fix minimal, write-up |
| [`uiux-engineer`](./uiux-engineer) | UI/UX engineering: lima state wajib, forms, responsive, aksesibilitas, usability review |
| [`product-designer`](./product-designer) | Mata desainer: hierarki, tipografi, warna, spacing system, design system, critique |
| [`agent-skill-author`](./agent-skill-author) | Meta-skill: menulis dan mengaudit skill agen lain terhadap quality bar 12 poin |
| [`tech-scout`](./tech-scout) | Radar teknologi: source sweep, rubrik 6 dimensi, hype immunity, CVE dan EOL watch |

### Operasional
| Skill | Fungsi |
|---|---|
| [`finance-analyst`](./finance-analyst) | Metrik SaaS, runway, unit economics, pricing, snapshot bulanan, red flags |
| [`accounting-core`](./accounting-core) | Jurnal double-entry, chart of accounts, rekonsiliasi, aset dan penyusutan, draft pajak, closing |
| [`sales-pipeline`](./sales-pipeline) | Kualifikasi lead berskor, discovery, proposal plus scope exclusions, cadence, negosiasi |
| [`marketing-growth`](./marketing-growth) | Brief kampanye, copywriting rules, SEO checklist, eksperimen growth, funnel review |
| [`social-media-specialist`](./social-media-specialist) | Grammar per platform, content calendar dan pilar, repurposing chain, metrics review |
| [`content-creator`](./content-creator) | Produksi: hook patterns, struktur per format (artikel, script, newsletter, thread), storytelling |
| [`content-editor`](./content-editor) | Quality gate 4 pass: struktur, clarity, style, correctness; verdict plus kill criteria |
| [`admin-ops`](./admin-ops) | SOP, notulen dua tier, triase email, konvensi dokumen |
| [`hr-officer`](./hr-officer) | Rekrutmen berbasis rubrik, onboarding 30 hari, performance, kasus sensitif, kompensasi |
| [`hr-admin`](./hr-admin) | Payroll dan potongan wajib (draft-until-verified), cuti dan absensi, kontrak, compliance calendar |

### Lintas-agen
| Skill | Fungsi |
|---|---|
| [`coo-orchestrator`](./coo-orchestrator) | Leader agent: routing, mengawal rantai lintas-agen, ops pulse harian, review mingguan, eskalasi, accountability register |
| [`continuous-learning`](./continuous-learning) | Baseline tiap agen: klasifikasi fakta busuk-cepat dengan verifikasi wajib, belajar dari koreksi, review pengetahuan terjadwal, aturan kejujuran |

> Skill pajak dan kepatuhan (`accounting-core`, `hr-admin`, `hr-officer`) memuat spesifik yang berorientasi Indonesia dan berstatus draft-until-verified terhadap regulasi tahun berjalan atau profesional berlisensi. Sesuaikan dengan yurisdiksi Anda.

---

## Susun jadi satu tim

[`AGENTS.md`](./AGENTS.md) adalah desain lengkap: skill mana di agen mana, kenapa peran dipisah seperti itu (auditor tidak mengaudit pekerjaannya sendiri; data finance terisolasi dari agen yang menghadap publik), dan cara menjalankannya sehari-hari. Ada juga opsi ramping 5 agen. (Versi Indonesia: [AGENTS.id.md](./AGENTS.id.md).)

## Cara skill bekerja

```
skill-name/
└── SKILL.md    # front matter (name + description) + prosedurnya
```

```markdown
---
name: marketing-growth
description: Use this skill for marketing work, campaigns, SEO, ads, copywriting,
  landing pages, funnels. Do NOT use for one-to-one sales (use sales-pipeline).
---

# Marketing and Growth
Tidak ada deliverable tanpa: target audience, satu pesan, metrik terukur...
```

Agen menyimpan `description` tiap skill di konteks dan membaca body hanya saat tugas cocok. Itu yang membuat pack besar tetap praktis.

## Kontribusi

Skill baru, pemicu yang lebih tajam, dan metodologi yang lebih baik disambut. Lihat [CONTRIBUTING.md](./CONTRIBUTING.md). Jaga skill tetap prosedural, jaga deskripsi tetap kaya pemicu.

## Lisensi

[MIT](./LICENSE) (c) 2026 Wira Darma. Pakai, fork, rilis.

Versi Inggris: [README.md](./README.md).

---

<p align="center"><b>Kalau pack ini menghemat waktu Anda, satu bintang membantu orang lain menemukannya.</b></p>
