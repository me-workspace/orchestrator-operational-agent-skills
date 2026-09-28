---
name: accounting-core
description: Use this skill for bookkeeping and accounting work — "catat transaksi", "jurnal", "buku besar", "rekonsiliasi bank", "laporan laba rugi/neraca", "pajak" (PPh, PPN), "aset & penyusutan/depresiasi", "invoice & piutang", chart of accounts, or closing the books. The record-keeping side of finance. Do NOT use for analysis/metrics/pricing (finance-analyst) or payroll tax administration (hr-admin). Tax computations are drafts to be verified against current regulations / a licensed tax consultant.
---

# Accounting Core

Accounting has one law: **every transaction is recorded twice (debit = credit), with evidence, in the right period.** No figure exists without a source document; no month ends without reconciliation.

## Chart of accounts (starter, adapt to the business)
```
1xxx Aset:    1100 Kas & Bank · 1200 Piutang Usaha · 1300 Uang Muka/Prepaid · 1500 Aset Tetap · 1590 Akm. Penyusutan (kontra)
2xxx Liabilitas: 2100 Utang Usaha · 2200 Utang Pajak · 2300 Pendapatan Diterima Dimuka
3xxx Ekuitas: 3100 Modal · 3200 Laba Ditahan · 3300 Prive
4xxx Pendapatan: per lini produk/jasa (4110 Langganan, 4120 Proyek, …)
5xxx HPP/COGS: biaya langsung (infra per pelanggan, fee payment gateway, komisi)
6xxx Beban Operasional: 6100 Gaji · 6200 Sewa · 6300 Marketing · 6400 Software/Infra umum · 6500 Penyusutan
```
Aturan: akun baru hanya bila kategori benar-benar baru; akun gemuk "Lain-lain" > 5% total beban = wajib dipecah.

## Transaction recording
- Setiap entri: tanggal · deskripsi jelas ("Bayar hosting Netcup Agu 2026", bukan "transfer") · akun debit/kredit · jumlah · **referensi bukti** (nomor invoice/nota/screenshot).
- Basis akrual untuk laporan (pendapatan saat earned, beban saat incurred); catat implikasi kas terpisah.
- Kasus umum yang sering salah:
  - Pendapatan langganan dibayar di muka setahun → 2300 dulu, diakui 1/12 per bulan.
  - Pembelian aset > threshold kapitalisasi (tetapkan, mis. Rp 2 juta) → aset, bukan beban.
  - Uang masuk pribadi pemilik → 3100/3300, bukan pendapatan. Jangan pernah campur dompet pribadi & bisnis di pembukuan.
  - Refund → pengurang pendapatan, bukan beban.

## Reconciliation (monthly, non-negotiable)
1. **Bank**: saldo buku vs rekening koran, item per item; selisih ditelusuri sampai nol atau tercatat sebagai item rekonsiliasi bernama.
2. **Payment gateway** (Midtrans dkk.): gross transaksi − fee − refund = settlement masuk bank. Fee dicatat sebagai beban, bukan dihilangkan diam-diam.
3. **Piutang**: daftar invoice terbuka vs pembayaran masuk; aging 0-30/31-60/>60 hari — yang > 60 hari masuk laporan dengan rencana penagihan.
4. **Utang**: tagihan belum dibayar vs jatuh tempo — jangan bayar denda karena lupa.

## Fixed assets & depreciation
- Register aset: item · tanggal perolehan · harga · umur manfaat · metode · nilai buku berjalan · lokasi/pemegang.
- Metode default: garis lurus. Umur pajak Indonesia (verifikasi ketentuan berlaku): Kelompok 1 (laptop, HP) 4 th · Kelompok 2 (mobil, mesin) 8 th · bangunan permanen 20 th.
- Penyusutan dijurnal bulanan (Dr 6500, Cr 1590). Aset dijual/hilang → hapus dari register + akui laba/rugi pelepasan.

## Tax (Indonesia — always stamp assumption year; DRAFT until verified)
- **PPh final UMKM 0.5%** dari omzet bulanan (omzet ≤ 4.8 M/th) — per **PP 20/2026** hanya untuk orang pribadi, PT Perorangan (tanpa batas waktu lagi), dan koperasi (max 4 th); **PT biasa/CV tidak lagi berhak** → tarif normal badan. Setor bulanan.
- **PPN**: tarif resmi 12%, tapi barang/jasa non-mewah efektif 11% via DPP nilai lain 11/12 (PMK 131/2024); 12% penuh hanya barang mewah kena PPnBM. Wajib bila PKP (omzet > 4.8 M/th → wajib dikukuhkan); pungut di invoice, faktur pajak, lapor bulanan. Jual SaaS ke luar negeri: perlakuan ekspor JKP — flag ke konsultan.
- **PPh 23** dipotong klien atas jasa (2%) → minta bukti potong, itu kredit pajak.
- **PPh 21** karyawan → domain hr-admin; pastikan angkanya nyambung ke jurnal beban gaji.
- Kalender: setor & lapor bulanan sebelum jatuh tempo; SPT Tahunan badan sebelum 30 April. Buat tabel kewajiban | deadline | status tiap awal bulan.

## Monthly close checklist → outputs
Semua transaksi terjurnal + bukti → rekonsiliasi 4 jenis di atas → penyusutan & pengakuan deferred revenue dijurnal → akrual beban yang belum ditagih → kunci periode.
Deliverable: **Laba Rugi** (pendapatan − COGS = gross profit; − opex = operating profit) · **Neraca** (harus balance — kalau tidak, cari selisihnya, jangan dipaksa) · **Arus kas ringkas** (operasi/investasi/pendanaan) · daftar piutang aging · posisi pajak. Anomali vs bulan lalu > 10% per akun = wajib satu kalimat penjelasan.
