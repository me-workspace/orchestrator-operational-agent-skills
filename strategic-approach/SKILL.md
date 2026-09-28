---
name: strategic-approach
description: Use this skill when choosing HOW to attack a problem before executing — "pendekatannya gimana", "strategi implementasi", "mulai dari mana", "opsi kita apa saja", build-vs-buy at project level, MVP scoping, migration strategy, platform choice, or any fork-in-the-road decision on a project or product. Produces compared options with a recommendation and kill criteria. Do NOT use for detailed scheduling (project-timeline-creator) or code-level architecture calls (principal-engineering).
---

# Strategic Approach

Strategy = choosing what NOT to do, on evidence, with a written way to know you chose wrong. An approach without kill criteria is a bet you can't lose gracefully.

## Framework — five steps, always in writing

**1. Frame the real problem**
Tulis ulang masalah dalam satu kalimat tanpa menyebut solusi apa pun. Kalau kalimatnya mengandung solusi ("kita butuh aplikasi mobile") — mundur satu langkah ("pengguna tidak bisa X saat Y"). Sebut juga: untuk siapa, seberapa sakit, dan bukti sakitnya.

**2. Constraints & assets (jujur, sebelum ideasi)**
Waktu · uang · orang/skill yang benar-benar ada · teknologi existing yang bisa dipakai ulang · hal yang tidak boleh dilanggar (kontrak, regulasi, komitmen). Aset yang sudah dimiliki sering mengubah pendekatan terbaik — inventaris dulu.

**3. Generate 3 genuinely different approaches**
Bukan 3 variasi ukuran dari ide yang sama. Paksa keragaman dengan lensa:
- **Minimal/manual-first**: versi paling kecil yang menguji asumsi inti — sering non-software (proses manual, spreadsheet, concierge).
- **Leverage**: pakai/rakit yang sudah ada (existing codebase, SaaS, open source) — beli waktu dengan uang atau ketidaksempurnaan.
- **Bangun benar**: solusi penuh untuk jangka panjang — mahal sekarang, murah nanti.

**4. Compare on the dimensions that matter**
```
| Dimensi | Opsi A | Opsi B | Opsi C |
| Waktu ke sinyal pertama (bukan ke "selesai") |
| Biaya total 6–12 bulan (bangun + rawat) |
| Risiko terburuk & seberapa mungkin |
| Reversibilitas / exit path |
| Kecocokan dengan aset & skill yang ada |
```
Dimensi pemenang biasanya **waktu ke sinyal pertama**: pendekatan yang paling cepat membuktikan/mematahkan asumsi terpenting.

**5. Recommend + kill criteria**
Satu rekomendasi tegas + alasan utama (satu paragraf). Lalu WAJIB:
- **Asumsi terpenting** yang jadi taruhan pendekatan ini.
- **Kill criteria**: sinyal terukur + tenggat ("bila dalam 4 minggu belum ada 5 user aktif → hentikan, pindah ke opsi B"). Tanpa ini, proyek gagal akan diperpanjang selamanya oleh sunk cost.
- **Langkah pertama minggu ini** — strategi tanpa langkah pertama adalah esai.

## MVP scoping rule
MVP menguji **satu** asumsi paling berbahaya, bukan versi kecil dari semua fitur. Pertanyaan pemandu: "apa hal termurah yang, kalau gagal, membuat sisa rencana tidak relevan?" Itu yang dibangun/diuji duluan. Semua yang lain masuk backlog tanpa rasa bersalah.

## Migration/replacement strategy (system A → B)
Default: **strangler & dual-run** — B dibangun di samping A, traffic/data dipindah bertahap per segmen, A tetap jadi fallback sampai B terbukti di segmen itu. Big-bang cutover hanya bila dual-run mustahil secara teknis, dan wajib dengan rehearsal + rollback yang sudah dilatih. Urutan pemindahan: segmen paling kecil risikonya dulu, segmen paling bernilai kedua (bukti nilai), sisanya menyusul.

## Review cadence
Setiap keputusan strategis dicatat (konteks · opsi · pilihan · kill criteria) dan dijadwalkan tinjauannya pada tanggal kill-criteria — bukan "nanti kalau ingat".
