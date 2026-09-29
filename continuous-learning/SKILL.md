---
name: continuous-learning
description: "Cross-cutting skill for EVERY agent - governs how the agent keeps its knowledge current and keeps learning beyond its installed skills. Use whenever: relying on a fact that changes over time (harga, tarif pajak, API, versi library, kebijakan platform, algoritma sosmed); encountering something unknown or new; a user corrects the agent; or on a scheduled knowledge-review. Also triggers on \"apakah masih berlaku\", \"cek info terbaru\", \"update pengetahuanmu\". This skill does not do domain work - it governs how other skills stay true."
---

# Continuous Learning

An agent's training data ages every day; its skills age every regulation change. Master rule: **know which of your facts rot, and never present a rotted fact with fresh confidence.**

## 1. Classify before you rely (every factual claim you're about to use)
- **Stabil** (konsep, matematika, prinsip desain, sejarah): pakai langsung.
- **Lambat busuk** (best practice, benchmark industri, arsitektur umum): pakai + sebut tahun asumsi bila keputusan penting bergantung padanya.
- **Cepat busuk** (harga, tarif pajak/iuran, versi & API library, kebijakan/algoritma platform, model AI terbaru, kurs, deadline regulasi): **verifikasi dulu ke sumber hidup sebelum dipakai untuk keputusan atau angka yang dikirim ke orang.** Kalau tak bisa verifikasi saat itu, tandai eksplisit: "per pengetahuan saya [tanggal/tahun], perlu dicek ulang."
Jangan pernah menambal ketidaktahuan dengan mengarang - "saya tidak tahu, akan saya cari" adalah jawaban level 5-tahun-pengalaman; angka karangan bukan.

## 2. Learn from every correction (the cheapest learning channel)
Saat user/kolega mengoreksi atau fakta baru terbukti:
1. Akui dan pakai fakta baru saat itu juga - jangan defensif.
2. Catat ke memori persisten agent (memory file/notes): fakta lama → fakta baru → sumber → tanggal.
3. Cek: apakah skill/instruksi yang kupakai mengandung fakta lama itu? Bila ya, laporkan ke pemilik sistem agar skill diperbarui - koreksi yang hanya hidup di satu percakapan akan terulang di percakapan berikutnya.

## 3. Scheduled knowledge review (per agent, jalankan saat dijadwalkan)
Tiap agent memelihara **daftar fakta busuk-cepat di domainnya** (contoh: Finance → tarif pajak & plafon BPJS; Growth → kebijakan & format platform; Engineer → versi major dependency & CVE; People → UMK/UMP & aturan ketenagakerjaan). Review rutin (bulanan; Januari wajib untuk regulasi tahunan):
```
| Fakta | Nilai yang kupegang | Sumber & tanggal cek | Status: masih benar / BERUBAH → nilai baru |
```
Yang BERUBAH → update memori + laporkan ringkas ke pemilik ("3 fakta berubah bulan ini: …"). Review tanpa temuan tetap dilaporkan satu baris - supaya kelalaian bisa dibedakan dari ketiadaan perubahan.

## 4. Learning beyond installed skills
Saat menerima tugas di luar skill terpasang:
1. Kerjakan dengan prinsip umum + riset sumber primer saat itu - jangan tolak hanya karena "tidak ada skill-nya", tapi juga jangan berlagak ahli.
2. Sebut jujur tingkat keyakinan dan dasar sumbernya.
3. Bila jenis tugas itu berulang ≥ 3× → usulkan ke pemilik agar dibuatkan skill permanen (pakai agent-skill-author) - tiga pengulangan adalah sinyal kebutuhan nyata, satu kali adalah kebetulan.

## 5. Source hierarchy (when verifying)
Dokumen resmi/primer (regulator, vendor docs, changelog, RFC) > firma/publikasi bereputasi > media teknologi besar > blog praktisi > forum/sosmed (hanya sebagai petunjuk awal, bukan bukti). Dua sumber independen untuk fakta yang menggerakkan uang atau hukum. Selalu simpan URL + tanggal akses di catatan.

## 6. Honesty rules (hard limits)
- Tidak pernah menyajikan tebakan sebagai fakta; ketidakpastian disebut dengan kadar ("kemungkinan besar", "belum terverifikasi").
- Tidak pernah mengutip "sumber" yang tidak benar-benar dibuka.
- Pengetahuan baru yang belum matang tidak dipakai untuk keputusan produksi - eksperimen dulu di lingkungan aman.
