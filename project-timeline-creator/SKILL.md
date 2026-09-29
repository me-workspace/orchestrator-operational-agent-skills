---
name: project-timeline-creator
description: Use this skill when a project schedule is needed - "buat timeline", "kapan selesai", "susun milestone", "roadmap", work breakdown, estimating a project, sprint planning, or re-planning after a slip. Produces a dependency-aware timeline with buffers and a critical path. Do NOT use for writing requirements (prd-creator) or tracking meeting decisions (admin-ops).
---

# Project Timeline Creator

A timeline is a chain of dependencies with buffers - not a wish list with dates. Its quality is measured by how early it predicts a slip, not by how optimistic it looks.

## Build order (never skip 1-3 to jump to dates)
1. **Breakdown**: pecah scope (dari PRD) jadi work item ≤ 2 hari kerja. Item > 2 hari = belum dipahami, pecah lagi. Sertakan item non-kode: desain, review, testing, deploy, dokumentasi, approval pihak lain.
2. **Dependency map**: per item, apa yang harus selesai duluan? Tandai dependency eksternal (API pihak ketiga, keputusan klien, konten dari tim lain) - ini sumber slip terbesar dan harus dikejar paling awal, bukan paling akhir.
3. **Estimate**: per item, optimis & realistis (jam/hari). Pakai realistis. Total fase × **1.5 buffer** (integrasi, bolak-balik review, hal tak terduga). Jangan sembunyikan buffer di tiap item - taruh eksplisit sebagai baris buffer per fase, supaya terlihat saat dimakan.
4. **Critical path**: rantai terpanjang item yang saling menunggu = durasi minimum proyek. Sebut eksplisit item mana yang di critical path - item ini tidak boleh menunggu resource.
5. **Milestones**: 3-7 titik yang bisa diverifikasi ("staging bisa dipakai klien uji", bukan "development 80%"). Tiap milestone punya demo/bukti.

## Output format
```
# Timeline <project> - v1 (tanggal, asumsi kapasitas: X orang/jam per minggu)

## Milestones
| M | Deliverable (bisa didemo) | Target | Gate |
## Breakdown per fase
| Item | Estimasi | Dependency | PIC | Critical path? |
| Buffer fase | (1.5× eksplisit) |
## Dependency eksternal & tanggal butuhnya (kejar sekarang)
## Risiko jadwal (top 3) + mitigasi
## Asumsi (kapasitas, scope beku per PRD vX, tanggal mulai)
```

## Rules of master-level scheduling
- **Student syndrome & Parkinson**: deadline per milestone, bukan hanya deadline akhir - kerja mengembang mengisi waktu yang diberikan.
- Jangan menjadwalkan utilisasi 100%; 70-80% kapasitas. Sisanya termakan interupsi, itu fakta bukan kegagalan.
- Fitur berisiko/gelap dikerjakan **paling awal** (de-risk dulu), bukan yang paling gampang dulu.
- Satu sumber kebenaran: timeline hidup di satu dokumen; update tercatat dengan tanggal & alasan.
- Tanggal yang dijanjikan keluar (ke klien) = tanggal internal + buffer komunikasi; jangan pernah janjikan tanggal critical-path mentah.

## When it slips (it will)
1. Deteksi dini: milestone meleset ≥ 20% → re-plan sekarang, jangan "kejar di fase berikutnya" (fase berikutnya sudah punya bebannya sendiri).
2. Pilihan yang jujur, tawarkan eksplisit ke pemilik keputusan: kurangi scope (default terbaik) / geser tanggal / tambah orang (hampir selalu paling lambat efeknya - Brooks's law).
3. Catat penyebab slip di dokumen timeline - pola slip adalah input estimasi proyek berikutnya.

## Re-planning report format
Apa yang berubah · kenapa · dampak ke milestone & tanggal akhir · opsi + rekomendasi · keputusan yang dibutuhkan dan dari siapa, kapan.
