# agent-skills — Skill pack untuk AI Agent (Hermes dkk.)

Paket skill mengikuti spec Agent Skills resmi Anthropic (agentskills.io):
satu folder per skill, `SKILL.md` wajib (frontmatter `name` + `description` trigger-rich
dengan negative triggers), body < 500 baris, prosedur/rubrik/quality-gate — bukan prosa.

## Scope A — Software & AI Environment (SDLC penuh)
| Skill | Fungsi |
|---|---|
| `sdlc-master` | Lifecycle end-to-end: fase + gate, tech design doc, DoD, branching, testing strategy |
| `principal-engineering` | Judgment level principal: prinsip, trade-off, decision framework, standard calls |
| `strategic-approach` | Memilih pendekatan: framing, 3 opsi beragam, rekomendasi + kill criteria, MVP scoping |
| `prd-creator` | PRD lengkap: goals terukur, non-goals wajib, acceptance criteria Given/When/Then |
| `project-timeline-creator` | Timeline: breakdown ≤ 2 hari, dependency, buffer 1.5×, critical path, protokol slip |
| `project-audit` | Audit project: 7 dimensi berskor, metode evidence-based, laporan berprioritas + verdict |
| `code-review-hardening` | Review kode: correctness + security, verifikasi sebelum lapor, rubrik severity |
| `secure-deploy-ops` | Deploy VPS: backup pra-deploy, diff live vs staged, smoke test, hardening baseline |
| `incident-debugging` | Debugging produksi: evidence-first, hipotesis diskriminatif, fix minimal, write-up |
| `uiux-engineer` | UI/UX engineering: 5 states wajib, forms, responsive, a11y, metode usability review |
| `product-designer` | Mata desainer: hierarki, tipografi, warna, spacing system, design system, critique |
| `agent-skill-author` | Meta-skill: menulis & mengaudit skill/SOUL agent lain, quality bar 12 poin |
| `tech-scout` | Radar teknologi software (lintas platform): sumber sweep, rubrik 6 dimensi, hype immunity, CVE/EOL watch |

## Leader & lintas-agent
| Skill | Fungsi |
|---|---|
| `coo-orchestrator` | Leader agent (COO): routing, mengawal rantai lintas-agent, ops pulse harian + review mingguan proaktif, eskalasi, accountability register — hanya untuk agent COO |
| `continuous-learning` | Baseline SEMUA agent — anti-basi: klasifikasi fakta busuk-cepat + verifikasi wajib, belajar dari koreksi, review pengetahuan terjadwal, aturan kejujuran |

## Scope B — Operational
| Skill | Fungsi |
|---|---|
| `finance-analyst` | Analisis: metrik SaaS, runway, unit economics, pricing, snapshot bulanan, red flags |
| `accounting-core` | Pembukuan: jurnal double-entry, CoA, rekonsiliasi, aset & penyusutan, pajak (draft), closing |
| `sales-pipeline` | Kualifikasi lead berskor, discovery, proposal + scope exclusions, cadence, nego |
| `marketing-growth` | Brief kampanye, copywriting rules, SEO checklist, eksperimen growth, funnel review |
| `social-media-specialist` | Grammar per platform, content calendar + pilar, repurposing chain, metrics review |
| `content-creator` | Produksi: hook patterns, struktur per format (artikel/script/newsletter/thread), storytelling |
| `content-editor` | Quality gate 4 pass: struktur → clarity → style → correctness; verdict + kill criteria |
| `admin-ops` | SOP, notulen 2 tier (ringkas + notulen proyek sangat detail), triase email, konvensi dokumen |
| `hr-officer` | Rekrutmen berbasis rubrik, onboarding 30 hari, performance, kasus sensitif, kompensasi |
| `hr-admin` | Payroll + PPh21/BPJS (draft-until-verified), cuti/absensi, kontrak PKWT/PKWTT, compliance calendar |

## Cara pakai
- **Claude Code**: salin folder skill ke `.claude/skills/` (project) atau `~/.claude/skills/` (global).
- **Hermes / agent lain**: tanam folder ke direktori skill agent; metadata (name+description)
  selalu di konteks, body dimuat saat terpicu.
- Loadout per persona agent: pilih subset (mis. agent "PM" = sdlc-master + prd-creator +
  project-timeline-creator + admin-ops), jangan tanam semuanya ke satu agent bila tak perlu —
  metadata 21 skill tetap memakan konteks.
- Angka pajak/hukum (accounting-core, hr-admin, hr-officer) berstatus DRAFT sampai diverifikasi
  regulasi tahun berjalan / konsultan berlisensi — aturan ini juga tertulis di dalam skill-nya.
- Audit isi `scripts/` skill pihak ketiga sebelum ditanam (supply-chain risk).
