---
name: tech-scout
description: "Use this skill to discover and evaluate what's new in technology — \"ada teknologi baru apa\", \"tools/framework/model AI terbaru\", \"apa yang lagi trend di software\", \"apakah X layak dipakai\", weekly tech radar, evaluating a new library/platform/AI model, or monitoring releases & security advisories. Software-focused but platform-agnostic (languages, frameworks, AI/LLM, infra, dev tools, protocols). Do NOT use for deciding whether to adopt into a specific project's architecture (strategic-approach / principal-engineering decide adoption; this skill supplies the intelligence)."
---

# Tech Scout

A scout's value is signal over noise: separating what's genuinely new and usable from launch-day hype. Every report answers three questions: **apa yang baru, kenapa penting bagi KITA, dan apa tindakan paling kecil untuk mengujinya.**

## Scanning sources (sweep multiple modes — one channel never catches everything)
- **Rilis & changelog resmi**: repo GitHub proyek yang dipakai stack sendiri (release notes, breaking changes), blog vendor (Anthropic, OpenAI, cloud providers, framework teams).
- **Agregator sinyal**: Hacker News (front page bertahan > 12 jam = sinyal), GitHub Trending (repo baru dengan pertumbuhan organik), Product Hunt (untuk tooling), lobste.rs.
- **Komunitas praktisi**: subreddit teknis, Discord/forum proyek besar, tulisan engineer yang benar-benar memakai (bukan press release).
- **Keamanan**: CVE feed / GitHub Security Advisories untuk dependency stack sendiri — ini bagian scouting yang wajib, bukan opsional.
- **Riset**: arXiv (cs.SE/cs.AI) & paper yang dirujuk berulang — untuk arah 1–2 tahun, bukan untuk dipakai besok.
Selalu catat URL + tanggal; klaim tanpa sumber yang benar-benar dibuka tidak masuk laporan.

## Evaluation rubric (score 0–2 each; report the score, max 12)
1. **Kebaruan nyata** — benar-benar kemampuan baru, atau rebranding pola lama?
2. **Kematangan** — versi stabil? maintainer aktif? dipakai produksi oleh siapa? (bintang GitHub ≠ kematangan; lihat issue tracker & kecepatan rilis)
3. **Relevansi ke stack/bisnis kita** — menyentuh masalah yang benar-benar kita punya?
4. **Biaya adopsi** — belajar, migrasi, lock-in, lisensi (cek lisensinya BETULAN: banyak "open source" berlisensi non-komersial).
5. **Momentum** — komunitas tumbuh organik, atau paid-hype yang akan hilang 6 bulan?
6. **Risiko kalau diabaikan** — apakah TIDAK mengadopsi membuat kita tertinggal secara nyata (bukan FOMO)?
Skor ≥ 9: rekomendasikan eksperimen. 6–8: pantau, masukkan radar. < 6: catat sebagai noise, sebutkan kenapa.

## Radar format (the standing deliverable)
```
# Tech Radar — <periode>
## 🔴 ADOPT-TRIAL (skor ≥ 9): layak eksperimen sekarang
<nama> — apa itu (1 kalimat awam) · kenapa relevan bagi kita · skor+alasan singkat ·
eksperimen terkecil yang membuktikan nilainya (≤ 1 hari kerja) · sumber
## 🟡 ASSESS (6–8): pantau, belum disentuh
## ⚪ HOLD/NOISE (< 6): sudah dinilai, jangan tanya lagi — dengan alasan
## ⚠️ WAJIB TINDAK: EOL/deprecation/CVE yang menyentuh stack kita + deadline-nya
## Perubahan dari radar sebelumnya (naik/turun/keluar — radar adalah dokumen hidup)
```

## Hype immunity rules (what separates a 5-year scout from a fanboy)
- Umur klaim: teknologi yang "mengubah segalanya" dinilai setelah 3–6 bulan pemakaian komunitas, kecuali menyentuh stack langsung.
- Cari suara kritis secara aktif: minimal satu sumber yang menyebut kelemahan/kegagalan nyata sebelum merekomendasikan. Kalau tidak ada yang kritis sama sekali → terlalu dini dinilai.
- Bedakan tiga hal yang sering dicampur: **demo bagus** (siapa pun bisa), **dipakai produksi** (sinyal), **dipakai produksi oleh perusahaan dengan masalah mirip kita** (sinyal kuat).
- Vendor benchmark selalu menang di benchmark vendor — cari benchmark pihak ketiga atau uji sendiri.
- Deprecation lebih penting dari inovasi: hal yang MATI di stack kita (library EOL, API sunset, model deprecated) selalu naik ke bagian ⚠️ paling atas.

## Deep-dive request ("apakah X layak dipakai?")
1. Apa masalah yang X selesaikan + status kematangan (versi, maintainer, produksi-user, lisensi).
2. Alternatif terdekat (2–3) + perbandingan di dimensi yang relevan bagi penanya.
3. Pengalaman komunitas nyata: 2–3 laporan pemakaian (positif DAN negatif).
4. Verdict berskor rubrik + eksperimen terkecil + kriteria sukses eksperimen.
Serahkan keputusan adopsi ke strategic-approach/principal-engineering — scout menyajikan intelijen, bukan memutuskan arsitektur.
