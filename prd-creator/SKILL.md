---
name: prd-creator
description: Use this skill whenever a product requirement document is needed - "buat PRD", "tulis requirement", "spek fitur", "dokumen produk", turning an idea/chat/meeting into a formal spec, or reviewing an existing PRD for gaps. Produces a complete PRD with measurable acceptance criteria. Do NOT use for the technical design (sdlc-master) or the schedule (project-timeline-creator).
---

# PRD Creator

A PRD's job is to make disagreement visible **before** code is written. It is done when an engineer can build from it without guessing and a tester can verify it without asking.

## Before writing - extract these from the requester (derive from context; ask only what's truly missing)
1. Masalah siapa, dan apa buktinya masalah itu nyata (data, keluhan, kejadian)?
2. Apa yang terjadi kalau TIDAK dibangun? (kalau jawabannya "tidak apa-apa" - tulis itu di PRD, biar keputusan sadar)
3. Definisi sukses dalam angka, dan kapan diukur?
4. Batas waktu/budget yang mengikat scope?

## PRD structure
```
# PRD: <nama fitur/produk>  (v0.x, tanggal, penulis, status: draft/review/approved)

## 1. Masalah & konteks
Siapa penggunanya, apa masalahnya, bukti masalah, biaya masalah hari ini.

## 2. Tujuan & metrik sukses
Max 3 goals; tiap goal → metrik + target + kapan diukur.
"Meningkatkan retensi" (kabur) → "D30 retention naik dari 22% ke 30% dalam 2 bulan setelah rilis" (terukur)

## 3. Non-goals (WAJIB, minimal 3)
Yang sengaja TIDAK digarap versi ini + alasan singkat. PRD tanpa non-goals = scope creep terjadwal.

## 4. User stories & alur
Per persona: "Sebagai X, saya ingin Y, supaya Z."
Alur utama langkah-demi-langkah + alur alternatif/error (pengguna salah input, koneksi putus, pembayaran gagal).

## 5. Requirements
Functional: bernomor (FR-1, FR-2, …), satu perilaku per butir, MoSCoW-tagged (Must/Should/Could).
Non-functional: performa (angka), keamanan, bahasa/lokal, device/browser, aksesibilitas, volume data.

## 6. Acceptance criteria
Per FR utama, format Given/When/Then - bisa dites, tidak ambigu:
"Given user belum bayar, When akses fitur premium, Then tampil paywall dan event `paywall_view` tercatat."

## 7. Ketergantungan & risiko
API eksternal, tim lain, keputusan legal/harga yang menggantung. Risiko + mitigasi.

## 8. Open questions
Daftar hidup; PRD tidak boleh "approved" selagi ada open question yang blocking.

## 9. Riwayat perubahan
Tanggal · apa yang berubah · kenapa - scope yang berubah diam-diam adalah pembunuh timeline nomor satu.
```

## Quality gates before marking "review-ready"
- Setiap requirement bisa dijawab "gimana ngetesnya?" dalam satu kalimat.
- Tidak ada kata karet tanpa angka: "cepat", "mudah", "banyak", "user-friendly", "seamless".
- Error/edge path tertulis, bukan hanya happy path.
- Non-goals terisi dan sudah dikonfirmasi requester.
- Seorang engineer yang tidak ikut diskusi bisa mengestimasi dari dokumen ini saja.

## Reviewing an existing PRD
Report gaps against the structure above, urut dari yang paling berbahaya: metrik sukses tak terukur → non-goals kosong → acceptance criteria hilang → error path hilang → istilah ambigu (kutip kalimatnya, usulkan perbaikannya).
