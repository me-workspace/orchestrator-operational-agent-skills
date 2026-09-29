---
name: project-audit
description: Use this skill when asked to audit, assess, or health-check an existing software project or codebase - "audit project ini", "kondisi codebase gimana", "layak dilanjut/diambil alih?", due diligence on inherited code, "kenapa project ini lambat terus", or producing a findings report with priorities. Produces a scored, evidence-based audit report. Do NOT use for reviewing a single diff/PR (code-review-hardening) or a live incident (incident-debugging).
---

# Project Audit

An audit is evidence + score + prioritized fixes - never impressions. Every finding cites a file/config/commit; every recommendation has effort and impact.

## Audit dimensions (score each 1-5, with written evidence)

**1. Arsitektur & kode**
Struktur modul jelas dan konsisten? Dependency antar modul searah atau spaghetti? Duplikasi besar (cek dengan grep pola berulang)? Dead code? Ukuran file/fungsi ekstrem? Framework/library versi berapa jauh di belakang?

**2. Keamanan** (pakai lensa code-review-hardening pada skala repo)
Secrets di repo/history (`git log -p | grep -i` untuk key/password/token)? Auth di setiap endpoint sensitif? Input validation di boundary? Dependency dengan CVE dikenal? Konfigurasi produksi (CORS, debug mode, verbose errors)?

**3. Data & migrasi**
Skema terdokumentasi? Migrasi versioned dan reversible? Backup ada, off-box, dan pernah di-restore? Data sensitif terenkripsi/di-mask di log?

**4. Testing & CI**
Coverage alur kritis (bukan angka % global - cek spesifik: auth, pembayaran, data-write utama). CI jalan dan hijau? Berapa lama? Tes flaky? Bisakah orang baru menjalankan tes secara lokal dalam < 30 menit?

**5. Operasional**
Deploy: berapa langkah manual? Rollback pernah dicoba? Logging cukup untuk debug insiden nyata? Monitoring/alerting ada? Single point of failure (satu server, satu orang, satu cron)?

**6. Deliverability (kesehatan proses)**
Dari git history: frekuensi commit/merge, ukuran PR, berapa lama PR menggantung, bus factor (berapa % commit dari 1 orang), TODO/FIXME yang membusuk, issue tracker vs realita kode.

**7. Dokumentasi & onboarding**
README bisa membuat orang baru menjalankan project? Keputusan arsitektur tercatat? Runbook operasional ada?

## Method (in order - don't skip the cheap steps)
1. **Recon**: baca README, struktur folder, file konfigurasi, CI config, dependency manifest. 30 menit ini membentuk peta.
2. **Git archaeology**: `git log --stat`, kontributor, hotspot file (file yang paling sering diubah = pusat risiko), umur branch.
3. **Automated sweep**: dependency audit, grep secrets, hitung LOC/duplikasi, jalankan tes.
4. **Deep dive** hanya pada 3-5 area yang recon tunjuk sebagai berisiko - bukan seluruh repo merata.
5. **Verify findings**: tiap temuan besar dicek ulang di kode aslinya sebelum masuk laporan.

## Report format
```
# Audit <project> - <tanggal>
## Ringkasan eksekutif (≤ 5 kalimat: kondisi umum, risiko terbesar, rekomendasi utama)
## Skor per dimensi (tabel 1-5 + satu kalimat bukti per dimensi)
## Temuan (urut prioritas)
[P1-BLOCKER|P2-HIGH|P3-MEDIUM|P4-LOW] <judul>
  Bukti: <file:line / commit / output perintah>
  Dampak: <apa yang rusak/berisiko, dalam istilah bisnis bila mungkin>
  Rekomendasi: <aksi konkret> | Effort: S/M/L
## Roadmap perbaikan: batch 1 (blocker), batch 2 (high), debt register sisanya
## Yang SUDAH baik (wajib - kalibrasi kepercayaan laporan)
```

## Verdict scale (for "layak dilanjut?" questions)
**Sehat** (lanjut normal) · **Perlu perawatan** (alokasikan 20-30% kapasitas ke perbaikan) · **Kritis** (hentikan fitur baru, stabilisasi dulu) · **Jangan diambil alih / tulis ulang bertahap** - sertakan estimasi biaya tiap jalur. Jangan pernah memberi verdict tanpa menyebut apa yang akan mengubahnya.
