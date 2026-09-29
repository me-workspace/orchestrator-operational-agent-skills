# Struktur AI Agent & Assignment Skill

Dokumen keputusan: berapa agent yang dibuat untuk 25 skill di pack ini, skill mana ditanam ke agent mana, dan bagaimana operasionalnya di Discord.

## Skill lintas-agent (baseline, ditanam ke SEMUA agent)
`continuous-learning` - disiplin anti-basi: klasifikasi fakta busuk-cepat (wajib verifikasi sebelum dipakai), belajar dari koreksi (catat ke memori + laporkan agar skill diperbarui), review pengetahuan terjadwal per domain, dan aturan kejujuran (tidak pernah menyajikan tebakan sebagai fakta). Skill ini yang membuat 24 skill lainnya tidak membusuk diam-diam. Karena ditanam ke semua agent, hitungan "max skill per agent" di bawah = skill domain + 1 baseline.

## Prinsip pembagian (kenapa tidak 1 agent semua-bisa, dan tidak 1 agent per skill)

1. **Batas konteks & triggering** - metadata (name+description) semua skill yang ditanam selalu duduk di konteks agent. Lebih dari ~6-7 skill per agent: konteks terbebani dan salah-trigger antar skill mulai terjadi (dua skill sama-sama merasa terpanggil).
2. **Kohesi peran** - skill yang sering dipakai dalam SATU alur kerja harus di agent yang sama (mis. review kode → deploy → debug adalah satu nafas engineer; kalender konten → produksi → edit adalah satu nafas tim konten). Memisahkannya memaksa handoff yang mahal.
3. **Pemisahan kepentingan** - peran yang sehat justru DIPISAH: editor yang mengedit tulisannya sendiri kehilangan jarak; auditor yang mengaudit pekerjaannya sendiri kehilangan kredibilitas. PM/auditor sengaja tidak diberi skill implementasi.
4. **Data sensitif** - agent yang memegang gaji, pajak, dan data karyawan (Finance, People) dipisah dari agent yang bicara ke publik/klien (Marketing, Sales) supaya kebocoran konteks antar percakapan tidak mungkin terjadi by design.

## Rekomendasi: 8 agent (1 leader + 7 specialist)

### 0. COO - leader/induk semua agent (proaktif by design)
**Skill (1 + baseline):** `coo-orchestrator` (+ `continuous-learning`)
**Job:** routing semua permintaan ke specialist yang tepat, mengawal rantai lintas-agent sampai selesai, ops pulse harian & ops review mingguan ke #daily-ops, deteksi macet > 24 jam, pengingat deadline 72 jam, eskalasi segera untuk hal kritis, dan pattern watch (usul skill/SOP baru saat pola berulang).
**Sengaja hanya 1 skill domain:** COO yang punya skill specialist akan tergoda mengerjakan sendiri dan jadi bottleneck - tugasnya mendelegasikan lalu menagih. Hard limits di skill: tidak memutuskan hal yang mengikat keluar (kontrak/harga/hiring), tidak melewati guardrail role Discord.
**Di Discord:** pemilik channel `#daily-ops`; juga satu-satunya agent yang boleh disapa di channel umum `#ops` untuk "minta tolong tapi tidak tahu ke siapa" - dia yang merutekan.

### 1. ENGINEER - pelaksana teknis
**Skill (5):** `sdlc-master` · `code-review-hardening` · `secure-deploy-ops` · `incident-debugging` · `uiux-engineer`
**Job:** membangun, me-review, men-deploy, dan menjaga sistem hidup - dari PR sampai produksi, termasuk sisi frontend/UX engineering.
**Catatan:** ini agent yang paling sering dipakai; jangan tambahi skill non-teknis apa pun.

### 2. ARCHITECT - otak teknis senior (pemisah sengaja dari Engineer)
**Skill (5):** `principal-engineering` · `strategic-approach` · `project-audit` · `agent-skill-author` · `tech-scout`
**Job:** keputusan arsitektur & trade-off, memilih pendekatan sebelum eksekusi, audit kesehatan project, merancang/mengaudit skill agent lain (meta), dan tech radar rutin (scouting teknologi baru + CVE/EOL watch untuk stack sendiri).
**Kenapa tech-scout di sini:** intelijen teknologi dan keputusan adopsi harus berdekatan tapi tetap dua langkah terpisah - scout menyajikan radar berskor, principal-engineering/strategic-approach yang memutuskan adopsi. Jadwalkan radar mingguan atau dwi-mingguan sebagai tugas rutin agent ini.
**Kenapa dipisah dari Engineer:** penilai dan pelaksana tidak boleh satu kepala - audit atas kode yang "dia" tulis sendiri tidak kredibel; dan diskusi strategi tidak boleh tergoda langsung ngoding.

### 3. PRODUCT MANAGER - requirement & jadwal
**Skill (4):** `prd-creator` · `project-timeline-creator` · `strategic-approach` · `admin-ops`
**Job:** ide/diskusi → PRD; PRD → timeline; rapat proyek → notulen detail 2-tier; menjaga scope & kesepakatan tercatat.
**Catatan:** `strategic-approach` sengaja ada di PM dan Architect - PM memakainya untuk scoping produk/MVP, Architect untuk arah teknis; kedua konteks jarang bertabrakan dalam satu agent karena agent-nya beda.

### 4. DESIGNER - mata visual
**Skill (2):** `product-designer` · `uiux-engineer`
**Job:** konsep visual, design system, critique, dan spesifikasi UI yang siap diimplementasi.
**Catatan:** `uiux-engineer` sengaja dobel dengan Engineer - di Designer dipakai sebagai bahasa spesifikasi (5 states, a11y) agar handoff ke Engineer tanpa penerjemahan. Kalau mau hemat, agent ini bisa dilebur ke Engineer (lihat opsi 5-agent).

### 5. FINANCE - uang masuk, keluar, dan kewajiban
**Skill (2):** `finance-analyst` · `accounting-core`
**Job:** pembukuan harian → closing bulanan → analisis (runway, unit economics, pricing) → kalender pajak.
**Catatan:** dua skill ini satu nafas (catat dulu, analisis kemudian) tapi dua topi - deskripsi skill sudah saling meng-exclude sehingga aman satu agent. Hard rule: angka pajak selalu draft-until-verified.

### 6. GROWTH - suara publik brand
**Skill (4):** `marketing-growth` · `social-media-specialist` · `content-creator` · `content-editor`
**Job:** strategi kampanye → kalender & kanal → produksi konten → quality gate sebelum terbit. Pipeline konten lengkap dalam satu agent karena alurnya harian dan bolak-balik.
**Catatan:** kalau volume konten sudah tinggi, pecah `content-editor` ke agent terpisah - mengembalikan "jarak editorial" (penulis bukan penilai). Itu trigger pemecahan pertama untuk agent ini.

### 7. PEOPLE & SALES OPS - manusia & relasi
**Skill (4):** `hr-officer` · `hr-admin` · `sales-pipeline` · `admin-ops`
**Job:** rekrutmen sampai payroll, kualifikasi lead sampai proposal, plus administrasi umum.
**Catatan:** ini satu-satunya agent gabungan lintas-fungsi - layak selama volume HR dan sales masih rendah. Trigger pemecahan: begitu ada > ~10 karyawan ATAU pipeline sales aktif > ~15 deal, pecah jadi agent PEOPLE (hr-officer + hr-admin) dan SALES (sales-pipeline + admin-ops). Data gaji/karyawan bersifat rahasia - jangan pernah pakai agent ini untuk percakapan yang melibatkan pihak eksternal.

## Matriks lengkap

| Skill | ENG | ARC | PM | DSG | FIN | GRW | P&S |
|---|---|---|---|---|---|---|---|
| sdlc-master | X | | | | | | |
| code-review-hardening | X | | | | | | |
| secure-deploy-ops | X | | | | | | |
| incident-debugging | X | | | | | | |
| uiux-engineer | X | | | X | | | |
| principal-engineering | | X | | | | | |
| strategic-approach | | X | X | | | | |
| project-audit | | X | | | | | |
| agent-skill-author | | X | | | | | |
| tech-scout | | X | | | | | |
| prd-creator | | | X | | | | |
| project-timeline-creator | | | X | | | | |
| admin-ops | | | X | | | | X |
| product-designer | | | | X | | | |
| finance-analyst | | | | | X | | |
| accounting-core | | | | | X | | |
| marketing-growth | | | | | | X | |
| social-media-specialist | | | | | | X | |
| content-creator | | | | | | X | |
| content-editor | | | | | | X | |
| sales-pipeline | | | | | | | X |
| hr-officer | | | | | | | X |
| hr-admin | | | | | | | X |

Total: 25 skill (23 domain + coo-orchestrator + continuous-learning baseline di semua agent), 8 agent (1 leader + 7 specialist), maksimal 5 skill domain per agent, 3 skill sengaja dobel (uiux-engineer, strategic-approach, admin-ops) dengan alasan tertulis di atas. `coo-orchestrator` hanya di COO - jangan pernah ditanam ke specialist (dua orkestrator = perang routing).

## Operasional di Discord (rumah semua agent)

Semua agent hidup di satu Discord server; manusia (kamu dan tim) berinteraksi lewat channel. Prinsip desain:

**1. Satu channel per agent, bukan satu channel rame-rame.**
`#engineer` `#architect` `#product` `#design` `#finance` `#growth` `#people-sales` - channel = konteks percakapan agent. Mencampur semua agent di satu channel membuat routing kacau (semua merasa terpanggil) dan konteks tercampur.

**2. Channel terbatas untuk data sensitif.**
`#finance` dan `#people-sales` wajib private (role-restricted) - gaji, pajak, data karyawan, dan nego deal tidak boleh terbaca anggota server umum. Ini pasangan dari prinsip isolasi data di pembagian agent.

**3. Channel broadcast: `#radar` dan `#daily-ops`.**
- `#radar`: ARCHITECT memposting tech radar terjadwal + alert CVE/EOL - semua orang membaca, tidak ada yang bertanya di sana (diskusi ke #architect).
- `#daily-ops`: ringkasan harian/mingguan tiap agent (satu pesan pendek per agent: apa dikerjakan, apa butuh keputusan manusia) - supaya pemilik bisa memantau 7 agent dalam satu scroll.

**4. Handoff antar agent tetap lewat artifact, bukan lintas-channel.**
Agent tidak membaca channel agent lain. PRD/timeline/notulen/design doc disimpan di penyimpanan bersama (repo/drive) dan link-nya diserahkan manusia (atau bot router) ke channel agent berikutnya. Ini disengaja: mencegah rantai halusinasi antar agent dan menjaga manusia tetap di titik keputusan.

**5. Guardrail aksi di Discord.**
Pesan Discord = input tak terpercaya: agent hanya menuruti perintah dari role yang diizinkan (owner/admin), bukan sembarang member - hard-rule di sistem, bukan cuma di prompt. Aksi eksternal (kirim email/WA ke klien, transfer, posting sosmed, deploy) selalu butuh konfirmasi eksplisit di channel dari manusia ber-role, dengan ringkasan apa yang akan dilakukan.

**6. Tugas terjadwal.**
Cron per agent memicu tugas rutinnya dan hasilnya diposting ke channel-nya: FINANCE → closing bulanan & kalender pajak (tiap awal bulan) · ARCHITECT → tech radar (mingguan) + review pengetahuan continuous-learning (bulanan, Januari wajib untuk regulasi tahunan) · GROWTH → review metrik konten (mingguan) · PEOPLE → kalender compliance HR (awal bulan). Hasil kosong tetap dilaporkan satu baris - absennya laporan harus berarti ada masalah, bukan ambigu.

## Opsi hemat: 5 agent (kalau kapasitas server/biaya terbatas)
1. **ENGINEER+** = ENGINEER + DESIGNER (7 skill - sudah di batas atas)
2. **ARCHITECT** tetap (4)
3. **PM** tetap (4)
4. **FINANCE+OPS** = FINANCE + hr-admin + admin-ops (5) - semua yang sifatnya pembukuan & administrasi
5. **GROWTH+SALES** = GROWTH + sales-pipeline + hr-officer pindah ke PM (6)
Trade-off: ENGINEER+ berat, dan Growth+Sales mencampur suara publik dengan negosiasi 1-on-1. Pakai hanya sebagai fase transisi.

## Alur kerja antar agent (contoh: fitur baru end-to-end)
Ide → **PM** (PRD + notulen kickoff) → **ARCHITECT** (pendekatan + design review) → **PM** (timeline) → **DESIGNER** (spek UI) → **ENGINEER** (build/review/deploy) → **ARCHITECT** (audit berkala) → **GROWTH** (launch content) → **FINANCE** (catat revenue, ukur unit economics).
Handoff antar agent selalu lewat artifact tertulis (PRD, design doc, timeline, notulen) - bukan "lanjutkan dari chat sebelah", karena antar agent tidak berbagi konteks.

## Rollout yang disarankan
Jangan nyalakan 7 sekaligus. Urutan: ENGINEER → PM → FINANCE (tiga alur paling sering) → sisanya menyusul setelah 1-2 minggu observasi triggering. Tiap agent baru: uji 5-10 prompt nyata, catat salah-trigger, pertajam negative triggers di description sebelum lanjut.
