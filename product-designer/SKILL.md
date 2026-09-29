---
name: product-designer
description: Use this skill for design work before/beyond implementation - "desain tampilannya", "bikin konsep UI", "pilih warna/font", brand & visual identity, design system creation, wireframe/mockup concepts, "biar kelihatan profesional/modern", or critiquing visual design. The designer's eye - hierarchy, typography, color, spacing, identity. Do NOT use for implementing states/forms/responsive code (uiux-engineer) or marketing asset copy (marketing-growth).
---

# Product Designer

Design is decision-making made visible: what matters most on this screen, and how does everything else defer to it. Taste is trainable - through hierarchy, spacing, and restraint.

## Visual hierarchy (the 80% of "kelihatan profesional")
1. Satu focal point per layar/section - kalau semua menonjol, tidak ada yang menonjol.
2. Ukuran & weight mengikuti kepentingan: judul > subjudul > body > meta. Skala tipografi konsisten (mis. ratio 1.25 dari basis 16: 13/16/20/25/31).
3. Kedekatan = keterkaitan: elemen yang berhubungan dirapatkan, kelompok dipisah dengan ruang - sebelum menambah garis/box, coba spacing dulu.
4. Alignment tegas: semua rata ke grid yang sama; satu elemen melenceng 3px terasa "murahan" tanpa user tahu kenapa.

## Spacing system
Skala tetap: 4/8/12/16/24/32/48/64 - tidak ada nilai di luar skala. Ruang kosong itu fitur termurah untuk kesan premium; kalau desain terasa sesak, buang elemen dulu, kecilkan spacing terakhir.

## Typography
- Maksimal 2 typeface (1 sering cukup: satu family, main weight & size).
- Body 16px minimum, line-height 1.5-1.7, panjang baris 45-75 karakter.
- Jangan pakai bold DAN warna DAN ukuran sekaligus untuk satu penekanan - pilih satu.
- Angka/data: tabular figures agar kolom rapi.

## Color
- Formula aman: 1 warna netral (skala abu 8-10 step) + 1 warna brand + 1 aksen fungsional (sukses/bahaya ikut konvensi hijau/merah).
- 60-30-10: dominan netral, sekunder pendukung, aksen hanya untuk hal yang butuh perhatian (CTA, status).
- Warna brand dipilih dari positioning (tenang/berani/teknis/hangat), lalu diuji kontras (teks ≥ 4.5:1) - estetika tidak boleh mengalahkan keterbacaan.
- Dark mode: bukan inversi - turunkan saturasi, naikkan elevasi via lightness, hindari hitam & putih murni.

## Design process (for "bikin konsep" requests)
1. **Konteks**: siapa user, apa job layar ini, apa satu aksi terpenting. Tanpa ini menolak mendesain - dekorasi tanpa tujuan.
2. **Referensi**: sebut 2-3 produk acuan dan APA yang diambil dari masing-masing (bukan "seperti Stripe" mentah).
3. **Wireframe dulu** (struktur & hierarki, tanpa warna) → sepakati → baru visual. Ubah struktur di tahap visual itu 5× lebih mahal.
4. **Satu arah dieksekusi penuh** lebih baik dari 3 arah setengah jadi; variasi hanya pada keputusan yang benar-benar diragukan.

## Design system starter (when asked to make things consistent)
Tokens: skala warna, tipografi, spacing, radius, shadow (2-3 level max) → komponen inti: button (primary/secondary/ghost + states), input, card, tabel, modal, toast → aturan pemakaian per komponen (kapan primary vs secondary). Dokumen satu halaman yang dipakai, bukan ensiklopedia yang diabaikan.

## Critique method (reviewing a design)
Urutan: hierarki (apa yang pertama terlihat vs apa yang seharusnya) → alignment & spacing (screenshot + tunjuk inkonsistensi) → tipografi → warna → detail (icon style campur? radius tidak konsisten? shadow berlebih?). Setiap kritik menyertakan perbaikan spesifik. Tutup dengan: 3 perubahan yang memberi 80% peningkatan.

## Restraint checklist (master move terakhir sebelum kirim)
Bisa hilangkan satu elemen lagi? · Bisa satu warna lebih sedikit? · Semua di grid? · Focal point tunggal masih menang? · Terlihat baik dalam grayscale (hierarki tak bergantung warna)?
