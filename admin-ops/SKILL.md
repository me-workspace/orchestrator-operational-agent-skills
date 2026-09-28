---
name: admin-ops
description: Use this skill for administrative/operational work — "buat SOP", "notulen rapat", "notulen project", "rangkum meeting", "dokumentasi rapat detail", "triase email", "susun jadwal", document filing/naming, vendor/asset tracking, or turning messy operational info (transcripts, chats, voice notes) into structured documents. Do NOT use for finance analysis (finance-analyst) or HR-specific documents (hr-officer/hr-admin).
---

# Admin & Operations

Turn chaos into documents people actually use: short, structured, owner-and-deadline on everything.

## SOP writing
```
# SOP: <nama proses>  (v1.0, tanggal, pemilik)
Tujuan & kapan dipakai | Prasyarat (akses/alat)
Langkah: bernomor, satu aksi per langkah, imperatif
  — sertakan perintah/klik persis, bukan "lakukan konfigurasi"
Jika gagal: gejala umum → penanganan → eskalasi ke siapa
Checklist verifikasi selesai
```
Test rule: a competent person who has never done the task must be able to follow it without asking. Steps that need judgment get a decision table, not vague prose.

## Meeting minutes — two tiers; pick deliberately

**Tier 1 — Notulen ringkas** (rapat rutin/internal): keputusan + action items + isu terbuka saja.
```
# Notulen <topik> — <tanggal>, hadir: ...
Keputusan: (hanya keputusan final, satu baris each)
Action items: | Aksi | PIC | Deadline |
Isu terbuka / parkir: ...
```

**Tier 2 — Notulen proyek detail** (rapat proyek, klien, atau keputusan penting — default bila diminta "notulen project"). Tujuannya: orang yang TIDAK hadir bisa memahami bukan hanya apa yang diputuskan, tapi **kenapa**, dan dokumen ini bisa dipakai menyelesaikan sengketa "dulu kita sepakatnya apa" enam bulan kemudian.
```
# Notulen Proyek: <nama proyek> — <topik rapat>
Tanggal/waktu/tempat/kanal | Hadir (nama + peran) | Tidak hadir yang relevan | Notulis
Referensi: notulen sebelumnya, dokumen yang dibahas (PRD vX, timeline vX)

## 1. Agenda & tujuan rapat (apa yang harus diputuskan hari ini)

## 2. Pembahasan per agenda — per item:
   Konteks singkat (kenapa dibahas)
   Poin/posisi tiap pihak yang substansial (nama → argumen inti, netral, tanpa opini notulis)
   Opsi yang dipertimbangkan + alasan opsi yang DITOLAK  ← bagian yang paling sering hilang dan paling bernilai
   ➤ KEPUTUSAN: <final, satu kalimat, tebal> — diputuskan oleh <siapa>
   Dasar keputusan: <alasan utama>

## 3. Rekap keputusan (tabel: # | Keputusan | Pengambil keputusan | Dampak ke scope/timeline/biaya)

## 4. Action items (tabel: # | Aksi spesifik | PIC | Deadline | Dependensi | Status)
   — aksi ditulis operasional ("kirim draft kontrak revisi pasal 3 ke klien", bukan "follow up kontrak")

## 5. Perubahan terhadap kesepakatan sebelumnya (scope/timeline/biaya yang bergeser + siapa menyetujui)
## 6. Isu terbuka & parkir (isu | pemilik | target kapan dibahas)
## 7. Risiko baru yang muncul di rapat
## 8. Rapat berikutnya: tanggal, agenda draft
```
Aturan tier 2:
- Tangkap **keputusan + alasan + siapa memutuskan** — bukan transkrip. Percakapan basa-basi dan debat yang tidak mengubah apa pun tidak dicatat.
- Kutip angka/tanggal/komitmen PERSIS seperti diucapkan; kalau ambigu di rapat ("secepatnya", "sekitar 50 juta"), tandai `[KLARIFIKASI]` dan kejar kepastiannya sebelum notulen didistribusikan.
- Netral total: notulis mencatat posisi orang, tidak menilai. Ketidaksepakatan yang belum selesai dicatat sebagai isu terbuka, bukan dihaluskan seolah sepakat.
- Distribusi ≤ 24 jam ke semua hadirin + koreksi window 48 jam ("bila tidak ada koreksi, notulen dianggap disetujui") — notulen yang disetujui = kontrak ringan.
- Action item tanpa PIC dan deadline tidak dicatat — kejar keduanya di rapat, itu tugas notulis.
- Simpan berurutan (`YYYY-MM-DD_notulen_<proyek>`), dan bagian "perubahan kesepakatan" selalu merujuk notulen sebelumnya — rantai ini adalah riwayat proyek.

**Dari bahan mentah** (transkrip/rekaman/chat): ekstrak dulu semua kalimat keputusan & komitmen apa adanya → kelompokkan per agenda → baru tulis notulen; jangan merangkum langsung dari ingatan satu kali baca — komitmen yang terlewat di notulen hilang selamanya.

## Email/task triage (default rules)
1. **Urgent+important** (money, outage, deadline < 48h, klien marah): surface immediately with a suggested response.
2. **Important not urgent**: schedule; propose a slot.
3. **Delegable**: draft the delegation message with context included.
4. **Noise**: batch summary; propose unsubscribe/filter rules for recurring noise.
Never auto-send anything external without explicit approval; drafts only.

## Document & file conventions
- Names: `YYYY-MM-DD_<jenis>_<topik>` — sortable, greppable.
- One source of truth per topic; new versions supersede in place, no `final_v2_fix` chains.
- Every tracker (vendor, aset, lisensi, kontrak) has columns: item · owner · biaya · tanggal jatuh tempo/perpanjangan · status. Flag anything expiring within 30 days.

## Recurring ops hygiene
When asked to "rapikan" any operational area: inventory what exists → identify duplicates/stale items → propose the minimal structure → migrate → write the one-paragraph SOP that keeps it clean. Always show the proposed structure before mass-moving anything.
