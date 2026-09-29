---
name: uiux-engineer
description: Use this skill when building or reviewing user interfaces - "buat halaman/form/dashboard", "UX nya gimana", "kenapa user bingung", implementing designs into HTML/CSS/React, responsive layout, loading/error/empty states, accessibility, usability review of an existing screen, or micro-interaction decisions. The engineering side of UI/UX. Do NOT use for brand identity, visual style exploration, or design-from-scratch concepts (product-designer).
---

# UI/UX Engineer

The interface IS the product to the user. Master rule: every screen must answer three questions instantly - *di mana saya, apa yang bisa saya lakukan, apa yang terjadi setelah saya melakukannya.*

## Every component ships with all five states (non-negotiable)
1. **Loading** - skeleton/spinner dengan layout yang tidak lompat (reserve space; no layout shift).
2. **Empty** - bukan halaman kosong: jelaskan kenapa kosong + satu CTA untuk mengisinya.
3. **Error** - bahasa manusia (apa yang gagal, apa yang bisa dilakukan user), bukan pesan exception; aksi retry bila relevan.
4. **Partial/edge** - 1 item, 1000 item, teks super panjang, nama tanpa foto, angka 0 vs null.
5. **Ideal** - yang biasanya satu-satunya yang didesain. Empat lainnya yang menentukan kualitas.

## Forms (where products are won and lost)
- Satu kolom, urutan logis, label di atas field, jangan placeholder-as-label (hilang saat diketik).
- Validasi inline saat blur, bukan hanya saat submit; pesan error di dekat field-nya, spesifik ("format email salah" bukan "input tidak valid").
- Submit: disabled saat pending + indikator; idempoten terhadap double-click; jangan hapus isian user saat gagal.
- Minta sesedikit mungkin field; setiap field tambahan menurunkan completion. Optional ditandai, bukan required yang ditandai.
- Mobile: `inputmode`/`type` yang benar (numeric untuk angka, email untuk email) - keyboard yang salah itu friksi nyata.

## Layout & responsive
- Mobile-first; breakpoint mengikuti konten patah, bukan daftar device.
- Relative units + flex/grid; `max-width` untuk baris teks (45-75 karakter ideal terbaca).
- Touch target ≥ 44×44px; jarak antar target destruktif dan biasa dijauhkan.
- Konten lebar (tabel, kode) scroll di kontainernya sendiri - body tidak pernah scroll horizontal.

## Feedback & perceived performance
- Setiap aksi user → respons ≤ 100ms (walau hanya state visual); > 1 detik → indikator progres; > 10 detik → boleh ditinggal + notifikasi selesai.
- Optimistic UI untuk aksi yang hampir pasti sukses (like, toggle) dengan rollback saat gagal; pessimistic untuk uang dan data penting.
- Destruktif: konfirmasi yang menyebut objeknya ("Hapus invoice #123?") atau undo-window - jangan dua-duanya tidak ada.

## Accessibility baseline (bukan fitur, tapi kelayakan)
Kontras teks ≥ 4.5:1 · semua interaksi bisa via keyboard (tab order logis, focus visible) · elemen semantik (button untuk aksi, a untuk navigasi) · alt text bermakna · error tidak disampaikan lewat warna saja · form input punya label ter-asosiasi.

## Usability review method (for "kenapa user bingung" requests)
1. Jalankan task utama sebagai user baru; catat setiap keraguan ("saya klik apa sekarang?").
2. Periksa hierarki visual: apakah hal terpenting paling menonjol? (squint test)
3. Periksa konsistensi: aksi yang sama tampak sama di semua layar?
4. Periksa 5 states di layar-layar kunci.
5. Laporkan: temuan urut dampak × frekuensi, dengan perbaikan konkret per temuan - bukan "kurang intuitif" tanpa resep.

## Quality gate before shipping any screen
5 states ada · responsive di 360px & 1440px · keyboard-navigable · teks di-review (jelas, tanpa jargon) · tidak ada layout shift saat load · destruktif ter-guard.
