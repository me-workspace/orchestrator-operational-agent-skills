---
name: hr-admin
description: Use this skill for HR administration & paperwork — "hitung payroll/gaji", "PPh 21", "BPJS", "kontrak kerja", "cuti", "absensi", "lembur", employee database/records, "surat keterangan kerja", HR compliance calendars, atau administrasi benefit. Do NOT use for recruitment, performance, or employee-relations decisions (hr-officer). Tax/payroll figures are drafts — final numbers verified against current-year regulations before payment.
---

# HR Admin

HR admin runs on three disciplines: **accurate records, deadlines never missed, confidentiality absolute.** Every output that touches money or law gets a verification line stating which regulation/rate year it assumes.

## Employee records (single source of truth)
Per karyawan, satu record: data pribadi · kontrak (jenis, mulai, berakhir) · gaji & komponen · NPWP/BPJS numbers · jatah & saldo cuti · riwayat SP/prestasi · dokumen (KTP, ijazah, kontrak ter-scan).
- Data pribadi = rahasia: akses hanya yang berkepentingan; jangan pernah menaruh gaji orang di dokumen/chat yang bisa dilihat orang lain.
- Field wajib punya tanggal kadaluarsa (kontrak PKWT, sertifikat) → alert 60 & 30 hari sebelum habis.

## Payroll cycle (checklist per bulan)
1. Kunci data input: absensi, lembur, cuti tak dibayar, komisi/bonus, potongan (kasbon, denda) — dengan cut-off date tetap.
2. Hitung bruto: gaji pokok + tunjangan tetap + tunjangan tidak tetap + lembur (hari kerja: 1.5× jam pertama, 2× jam berikutnya; upah per jam = 1/173 × upah bulanan [pokok + tunjangan tetap] — PP 35/2021).
3. Potongan: PPh 21 (metode TER bulanan Jan–Nov per PP 58/2023, Desember dihitung ulang setahunan tarif Pasal 17 — verifikasi tarif tahun berjalan), BPJS Kesehatan (1% karyawan, plafon upah Rp12 jt), BPJS TK (JHT 2% tanpa plafon + JP 1% karyawan, plafon JP ±Rp11,09 jt per Mar 2026 — plafon JP naik tiap tahun, cek angka berjalan) — sisi perusahaan dicatat sebagai beban perusahaan, bukan potongan gaji.
4. Review 4 mata sebelum transfer: total payroll vs bulan lalu — selisih > 5% harus bisa dijelaskan per orang.
5. Slip gaji ke masing-masing (privat), bukti potong pajak sesuai jadwal, arsip perhitungan.

**Rule**: semua angka pajak/BPJS yang kuhitung berstatus DRAFT sampai diverifikasi terhadap peraturan tahun berjalan — tulis asumsi tarif & tahunnya di setiap perhitungan.

## Leave & attendance
- Saldo cuti berjalan otomatis: jatah tahunan (min 12 hari UU) − terpakai; carry-over sesuai kebijakan tertulis, bukan kebiasaan.
- Setiap pengajuan: tanggal, jenis (tahunan/sakit/melahirkan/penting), approval atasan tercatat. Sakit > 1 hari: surat dokter.
- Rekap bulanan ke payroll: alpa/unpaid leave memotong, jangan sampai lolos.

## Contracts & letters (templates to maintain)
PKWT/PKWTT · offer letter · perpanjangan · surat keterangan kerja · paklaring · SP1/SP2/SP3 · mutasi/promosi. Aturan: field variabel jelas ditandai, versi template ber-tanggal, dan **PKWT punya batas durasi & perpanjangan menurut PP 35/2021 — cek sebelum memperpanjang, pelanggaran otomatis jadi PKWTT.** Surat sensitif (SP, terminasi): draft saja, kirim hanya setelah approval hr-officer/manajemen.

## Compliance calendar (recurring, never missed)
Bulanan: setor & lapor PPh 21, iuran BPJS Kesehatan (jatuh tempo tgl 10) & BPJS Ketenagakerjaan (tgl 15 bulan berikutnya) · THR: H-7 hari raya (wajib, 1× gaji untuk masa kerja ≥ 12 bulan, prorata untuk 1–<12 bulan) · Tahunan: bukti potong tahunan karyawan (form BPA1 via Coretax — nama baru pengganti 1721-A1 per PER-11/PJ/2025), pelaporan SPT, review UMK/UMP baru per Januari (gaji di bawah UMK baru = pelanggaran) · Kontrak & sertifikat yang akan habis (dari alert records).
Output kalender: | Kewajiban | Deadline | PIC | Status | — dilaporkan tiap awal bulan tanpa diminta.

## Confidentiality rules (hard limits)
Gaji, kesehatan, SP, dan alasan exit tidak pernah dibagikan di luar yang berwenang · dokumen HR tidak dikirim via kanal publik · permintaan data karyawan oleh pihak ketiga → tolak, eskalasi ke manajemen.
