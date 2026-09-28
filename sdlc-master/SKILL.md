---
name: sdlc-master
description: Use this skill for any software development lifecycle question or execution — "mulai project baru", "proses development yang benar", "best practice", "dari ide sampai rilis", branching/release strategy, definition of done, code quality standards, testing strategy, or when orchestrating a feature from requirement to production. The umbrella skill for HOW software gets built end-to-end. Do NOT use for writing the PRD itself (prd-creator), the schedule (project-timeline-creator), or auditing an existing project (project-audit).
---

# SDLC Master

Software is built in a loop, not a line: every phase produces an artifact the next phase consumes, and every artifact has an owner and an exit gate. Skipping a gate is a decision — record it as accepted risk, never as an accident.

## The lifecycle and its gates

| Fase | Artifact keluar | Gate untuk lanjut |
|---|---|---|
| 1. Discovery | Problem statement + evidence | Masalah nyata, terukur, dan layak digarap (bukan solusi mencari masalah) |
| 2. Requirement | PRD (pakai prd-creator) | Scope, non-goals, dan acceptance criteria disetujui |
| 3. Design | Tech design doc + desain UI (bila ada UI) | Reviewed oleh minimal 1 engineer lain; risiko besar teridentifikasi |
| 4. Plan | Timeline + breakdown (pakai project-timeline-creator) | Estimasi punya buffer; dependency terpetakan |
| 5. Build | Kode + tes, via PR kecil | CI hijau, review lolos, DoD terpenuhi per PR |
| 6. Verify | Test report + staging sign-off | Acceptance criteria PRD terbukti, bukan diasumsikan |
| 7. Release | Deploy + rollback plan | Smoke test produksi lolos; monitoring aktif |
| 8. Operate | Metrics + incident log | Feedback masuk ke Discovery berikutnya |

## Tech design doc (fase 3) — struktur wajib
```
Konteks & masalah | Goals / Non-goals
Desain yang diusulkan (diagram + alur data)
Alternatif yang ditolak + alasannya  ← bagian paling bernilai
Skema data & kontrak API (breaking change? migrasi?)
Keamanan, skala, failure mode
Rencana rollout & rollback
Open questions
```
Rule: kalau desain tidak bisa dijelaskan dalam 2 halaman, sistemnya terlalu rumit atau pemahamannya belum matang.

## Definition of Done (per PR — tidak bisa dinego sebagian)
1. Perilaku baru punya tes (unit untuk logika, integrasi untuk alur); tes lama tetap hijau.
2. Error path ditangani — bukan hanya happy path.
3. Tidak ada secret/credential/debug flag ikut ter-commit.
4. Migrasi DB reversible atau punya rencana rollback tertulis.
5. Dokumentasi tersentuh bila perilaku publik berubah (README, API doc, changelog).
6. Di-review orang/agent lain — self-merge hanya untuk perubahan trivial yang disepakati kategorinya.

## Branching & release (default yang terbukti)
- Trunk-based: branch pendek per issue → PR kecil (< ~400 baris diff efektif) → merge ke main → main selalu deployable.
- Rilis = tag + changelog. Fitur setengah jadi disembunyikan di balik flag, bukan ditahan di branch berumur panjang.
- Hotfix: branch dari tag produksi, fix, tag baru, lalu merge balik ke main — jangan cherry-pick liar.

## Testing strategy (piramida, alokasi kasar)
- 70% unit (cepat, logika murni), 20% integrasi (DB, API antar modul), 10% end-to-end (alur kritis: auth, pembayaran, data-write utama).
- Tes ditulis untuk perilaku, bukan implementasi — refactor tidak boleh mematahkan tes yang perilakunya tak berubah.
- Setiap bug produksi yang lolos = tes regresi baru sebelum fix di-merge. Tanpa kecuali.

## Anti-pattern yang harus dihentikan saat terlihat
Big-bang PR ribuan baris · "nanti tesnya nyusul" · scope membengkak tanpa update PRD/timeline · branch hidup > 1 minggu · deploy Jumat sore tanpa alasan kuat · fitur dirilis tanpa cara mengukur keberhasilannya · desain diputuskan di chat lalu hilang (selalu tulis ke doc).

## Kapan memanggil skill lain
Requirement → `prd-creator` · jadwal → `project-timeline-creator` · keputusan arsitektur/pendekatan → `strategic-approach` · review kode → `code-review-hardening` · deploy → `secure-deploy-ops` · produksi rusak → `incident-debugging` · menilai kesehatan project berjalan → `project-audit`.
