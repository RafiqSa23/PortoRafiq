# PRD — Website Portofolio Rafiq Setyo Aji

**Versi:** 0.3 · **Tanggal:** 22 Oktober 2026 · **Owner:** Rafiq · **PM:** Claude
**Status:** Keputusan produk & desain terkunci (lihat §14). Siap dieksekusi; menunggu 5 input konten dari Rafiq (lihat §14b).
**Perubahan v0.2 → v0.3:** posisi diperjelas (lamaran kerja dulu, freelance sekunder), situs diposisikan sebagai *proof artifact*, nav dipangkas ke 4 item, halaman `/sertifikat` & form kontak dibuang, estetika jadi *game subtle*, tech stack dikoreksi ke Astro 6 + Tailwind v4 CSS-first, metrik SEO diganti dari "nama di halaman 1" ke query bertagar.

---

## 1. Ringkasan

Website portofolio pribadi satu domain, statis, cepat, dan SEO-friendly, di-hosting di Vercel.

**Fungsi utama: alat melamar kerja** untuk posisi junior fullstack / web developer. **Freelance adalah opsi sekunder** yang ditawarkan lewat CTA — bukan positioning utama, bukan halaman tersendiri.

Situs ini diperlakukan sebagai **proof artifact**, bukan *destination*: penggunanya membuka tautan dari bio/profil lain (README GitHub, LinkedIn, bio marketplace, tanda tangan email) dan menilai dalam **±20 detik**. Karena itu prinsipnya:

- **Satu keputusan per layar** — hubungi, atau lihat proyek.
- **Semua jalur kontak berada di `/kontak`** dan footer; WhatsApp hanya di `/kontak`.
- **Tidak ada fitur yang hanya berguna bagi penghuni situs** (filter kategori, "proyek berikutnya", proyek terkait, pagination).
- **Tidak ada kedalaman yang tidak perlu** — 4 halaman utama, bukan arsitektur portal.

---

## 2. Latar Belakang & Masalah

- Belum ada website portofolio; recruiter hanya melihat CV dan repositori GitHub mentah.
- Banyak proyek belum ter-deploy sehingga sulit dibuktikan "jalan".
- Sudah pernah undergo **PKL/magang** — ada konteks kerja nyata, tetapi belum dirapikan menjadi cerita yang bisa dipindai.
- Dibutuhkan satu tempat yang merangkum siapa saya, apa yang sudah dibuat, bukti kompetensi (sertifikat), dan cara menghubungi — dalam **satu tautan yang bisa ditempel di mana saja**.

---

## 3. Tujuan & Metrik Keberhasilan

| Tujuan | Metrik | Target | Cara Ukur |
|---|---|---|---|
| Mudah ditemukan | P1 Google untuk query bertagar: `Rafiq Setyo Aji fullstack developer`, `portofolio Rafiq Setyo Aji` | ≤ 3 bulan setelah rilis | Google Search Console |
| Konsistensi domain | 1 domain custom + 2 backlink (README GitHub, LinkedIn) | 100% | Manual |
| Cepat dan ringan | Lighthouse mobile Performance / SEO / Accessibility / Best Practices | ≥ 95 / 100 / ≥ 95 / ≥ 95 | Audit manual tiap rilis |
| Relevansi lamaran | Pengunjung yang membuka `/kontak` atau `/cv` | ≥ 15% dari total pengunjung | Vercel Web Analytics |
| Respons nyata | Lamaran masuk | ≥ 1 per minggu | Manual (email) |
| Kredibel | 3 proyek + 1 studi kasus lengkap + 1 pengalaman PKL | 100% | Review QA |
| Ringan dirawat | Menambah proyek/sertifikat tanpa menyentuh kode layout; tidak ada tahun yang ditulis manual | Cukup tambah 1 file konten | Review QA |

> **Perubahan metrik dari v0.2.** Target lama "nama sendiri muncul di halaman 1 Google" dihapus: nama "Rafiq Setyo Aji" adalah nama umum di Indonesia, sehingga halaman 1 dikuasai orang dengan nama sama dan sepenuhnya di luar kendali. Diganti query bertagar yang bisa_FEATURE.ai dan bisa diukur lewat Search Console.

---

## 4. Target Pengguna

| Prioritas | Pengguna | Datang dari | Yang dicari dalam 20 detik | Halaman tujuan |
|---|---|---|---|---|
| 1 | **Recruiter / hiring manager** | Tautan di email lamaran, LinkedIn | Nama, peran, ketersediaan, bukti kerja, caraBalas | `/` → `/proyek` → `/kontak` |
| 2 | **Calon klien freelance** | Bio marketplace, Instagram, WhatsApp | Apakah ini orang yang bisa dikerjakankan, apa yang bisa dibuat, cara order cepat | `/` → `/kontak` |
| 3 | **Sesama developer / dosen / rekan** | README GitHub, pencarian | Detail teknis, rekam jejak, sumber | `/proyek/[slug]`, `/tentang` |

---

## 4a. Arah Visual (Ditetapkan — "Game Subtle")

- Tema gelap navy-hitam dengan glow biru; judul kondensed tebal; nav berbentuk pill; tipografi display.
- **Yang dipertahankan:** glow biru, nav pill, Bebas Neue, marker `▸` bergaya menu game, grid kartu.
- **Yang berubah dari v0.2:** hero **tidak** memakai foto cutout dan **tidak** berupa game-menu full-bleed; hero jadi layout 2 kolom dengan foto profesional. Bentuk merah di belakang foto dihapus. Penutup "TERIMA KASIH 2026" (big display) diganti ajakan bertindak.
- Efek visual dengan CSS murah (gradient), bukan gambar atau blur berat.
- Detail lengkap ada di `DESIGN.md`.

---

## 5. Ruang Lingkup

### In scope (MVP)

- **4 halaman utama + 2 pendukung:** Home `/`, Tentang `/tentang`, Proyek `/proyek` (+ 3 halaman detail), Kontak `/kontak`, plus `/cv` dan 404.
- Header (pill 4 item) & footer konsisten.
- Blok **Sertifikat di dalam `/tentang`** (bukan halaman terpisah) + lightbox native.
- **1 studi kasus lengkap** (Whitehouse) + **2 halaman proyek ringkas** (Klasifikasi TB, Inventory).
- 1 OG image default (1200×630) + metadata + JSON-LD per halaman.
- SEO teknis lengkap, performa tinggi, responsif, aksesibel.
- Deploy ke Vercel + CI otomatis dari GitHub (Vercel Git integration).
- Analytics cookieless (Vercel Web Analytics).

### Out of scope (MVP)

- Halaman `/sertifikat` terpisah.
- Form kontak (email + WhatsApp preset sudah cukup; form menambah backend & spam).
- Filter kategori proyek.
- Harga / paket / halaman layanan freelance.
- Blog / CMS berbasis dashboard.
- Versi bahasa Inggris.
- OG image per proyek (Satori/canvas).
- Tema terang, arsip versi lama, testimoni klien, filter, proyek terkait.
- Login / autentikasi, database, backend sendiri.

---

## 6. Rekomendasi Tech Stack (PM)

| Kebutuhan | Pilihan | Alasan |
|---|---|---|
| Framework | **Astro 6** | Output HTML statis, JS ≈ 0 secara default → paling ringan dan SEO terbaik. Butuh Node **≥ 22.23.4** (mesin kerja: v24.16.0 ✓) |
| Interaktivitas | **Tanpa framework island** | Satu-satunya interaksi: menu mobile + lightbox → cukup JavaScript vanilla. React/Preact tidak perlu; PRD v0.2 masih menyebut React, kini dibuang |
| Styling | **Tailwind CSS v4 (CSS-first)** | Token didefinisikan **satu kali** di blok `@theme` pada `src/styles/global.css`. **Bukan** `tailwind.config.mjs` — pada v4 file itu diabaikan diam-diam |
| Konten | **Astro Content Collections (Content Layer)** | `src/content.config.ts` + loader `glob()`, skema Zod. Tambah proyek/sertifikat cukup 1 file Markdown; data tervalidasi saat build |
| Gambar | `astro:assets` | WebP/AVIF otomatis, lazy-load, ukuran responsif, `width`/`height` eksplisit |
| Font | **Bebas Neue (display, 1 bobot) + Inter (variable)**, self-hosted, subset WOFF2, preload **keduanya** | Tanpa request ke Google Fonts; hanya 2 keluarga |
| Form kontak | **Tidak ada form** — `mailto:` + tombol WhatsApp dengan pesan preset | Tetap 100% statis, nol backend, nol spam |
| Analytics | **Vercel Web Analytics** | Cookieless, tanpa cookie banner |
| Hosting | **Vercel (Hobby/gratis)** | CDN global, preview deploy per branch, 301 dari `.vercel.app` ke domain custom saat migrasi |
| Deployment | **Vercel Git integration** (bukan GitHub Actions) | Build & deploy otomatis dari push ke `main` |

> Alternatif: Next.js (SSG) — lebih berat dari Astro untuk situs yang pada dasarnya statis, jadi tetap tidak direkomendasikan.

---

## 7. Kebutuhan Fungsional

### 7.1 Header

- Logo monogram "R" (SVG inline) → link ke `/`.
- **Pill nav di tengah, 4 item:** Home · Tentang · Proyek · Kontak. Tab aktif berlatar `--pill-active-bg` dengan teks `--pill-active-text`; `aria-current="page"`.
- Tombol **"Hubungi Saya"** di kanan (desktop).
- Sticky, tinggi ringkas, latar solid semi-transparan (tanpa `backdrop-filter`).
- Mobile: tombol hamburger 44×44 → panel `<dialog>`; tutup dengan `Esc`; fokus dikembalikan ke pemicu.
- Skip link "Lewati ke konten".

### 7.2 Home

**Section 1 — Hero (2 kolom)**
- Kolom kiri: foto profesional (WebP, 4:5, ≤ 60 KB) dengan glow biru di belakang, radius `md`.
- Kolom kanan:
  - Eyebrow "OPEN TO WORK" (Inter, uppercase, letter-spacing lebar, `--text-muted`).
  - H1 display: nama lengkap.
  - Sub-peran: "Fullstack Web Developer" + pill status hijau "Tersedia untuk posisi full-time".
  - 1 kalimat value proposition (gaya personal-profesional).
  - **Baris bukti:** "5 proyek selesai — React, Laravel, Node, Python" (angka wajib akurat).
  - **2 CTA** bergaya menu game dengan marker `▸`: `START` → "Lihat Proyek" → `/proyek`; `CONTACT` → "Hubungi Saya" → `/kontak`.
- Mobile: foto di atas (maks 40 vh), teks & CTA di bawah, CTA menjadi tombol penuh.

**Section 2 — Proyek Unggulan (3)**
- Whitehouse (kartu lebar penuh), Klasifikasi TB, Multi-User Inventory.
- Kartu: cover, badge kategori, H3, ringkasan 2 baris, badge tech, tautan "Lihat studi kasus".
- Link "Lihat semua proyek" → `/proyek`.

**Section 3 — Tech Stack**
- 8–10 ubin ikon 64×64, SVG inline, nama tech di bawah.

**Section 4 — Sertifikat Terbaru**
- 3 sertifikat terbaru + link "Lihat semua di Tentang" → `/tentang#sertifikat`.

**Section 5 — CTA Penutup**
- "Tertarik bekerja sama?" + 1 kalimat + tombol [Lihat Proyek] [Hubungi Saya].
- **Tidak ada** big display "TERIMA KASIH 2026".

### 7.3 Tentang (`/tentang`)

- Layout 2 kolom: foto profil + cerita (3–4 paragraf, gaya personal-profesional, menyebut PKL).
- Blok **Pengalaman**: PKL — perusahaan, durasi, dan 1 hasil konkret.
- Blok **Pendidikan**.
- Blok **Keahlian**: dikelompokkan (Frontend, Backend, Database, Tools, AI/ML).
- Blok **Bahasa**: bar tipis + teks level/percentage (aksesibel).
- Blok **Sertifikat** (`id="sertifikat"`): 7 sertifikat Dicoding + opsional MOS Excel, dikelompokkan Pemrograman / Data-AI / Lainnya. Thumbnail 4:3 lazy-load, lightbox `<dialog>` native, tombol "Verifikasi" → link sumber.
- CTA: tombol unduh CV → `/cv`.

### 7.4 Proyek (`/proyek`)

- Judul + 1 kalimat konteks. **Tanpa filter kategori.**
- Grid: 1 kolom mobile, 2 kolom ≥768px; kartu unggulan pertama `span 2` (lebar penuh).
- 3 proyek: Whitehouse, Klasifikasi TB, Multi-User Inventory.

### 7.5 Detail Proyek (`/proyek/[slug]`)

- Breadcrumb: Home › Proyek › [Judul].
- H1 + ringkasan + badge kategori + badge tech.
- Tombol [Live Demo] [GitHub] — **hanya tampil jika tautannya ada**.
- Cover + galeri screenshot.
- **Format A — lengkap (Whitehouse):** Masalah → Solusi → Peran saya → Tech stack → Hasil/Dampak.
- **Format B — ringkas (Klasifikasi TB, Inventory):** Ringkasan → Masalah & Solusi → Hasil → Tautan (±300 kata, 3 blok).
- CTA penutup → `/kontak`.

### 7.6 Kontak (`/kontak`)

- Foto bulat dengan border aksen.
- Kontak: **email** (`mailto:`), **LinkedIn**, **GitHub**, dan **WhatsApp** (tombol dengan pesan yang sudah terisi otomatis).
- Blok **"Layanan freelance"**: 2–3 layanan spesifik (mis. web company profile, toko online, sistem kasir UMKM).
- Teks ekspektasi: "Balas dalam 24 jam kerja".
- Penutup: ajakan bertindak + tombol [Lihat Proyek] [Hubungi Saya].
- **Tidak ada form kontak.**

### 7.7 Footer

- 3 kolom: identitas (nama + peran + 1 kalimat) · navigasi (4 item) · sosial (GitHub, LinkedIn, email).
- Copyright © dengan **tahun otomatis** dari `new Date().getFullYear()` — tidak pernah ditulis manual.
- Tombol "Kembali ke atas".

### 7.8 Halaman pendukung

- **404 kustom** (gaya sama, 1 kalimat, link ke Home + Proyek).
- `sitemap.xml` (`@astrojs/sitemap`) + `robots.txt`.
- Favicon set: `favicon.ico`, `favicon-512.png`, `apple-touch-icon.png`.
- **`/cv`**: 1 halaman ringkas — foto, nama, 1 kalimat, tombol [Unduh CV (PDF)] dan [Buka di tab baru], catatan "Diperbarui: Oktober 2026" (diisi manual **per revisi**, bukan per tahun).
- `public/og-default.png` 1200×630.

---

## 8. Kebutuhan SEO (Wajib)

- **Metadata per halaman:** `<title>` unik (≤ 60 karakter), meta description (≤ 155 karakter), canonical URL absolut.
- **Open Graph & Twitter Card:** 1 OG image default 1200×630 dipakai lintas halaman; `og:title`/`og:description` ditulis unik per halaman. OG per proyek ditunda ke backlog.
- **Structured data (JSON-LD):** `Person` (Home + Tentang, lengkap dengan `sameAs` GitHub & LinkedIn), `WebSite`, `BreadcrumbList` (detail proyek), `SoftwareSourceCode` (detail proyek).
- **Semantik HTML:** satu `<h1>` per halaman, hierarki heading rapi, `<header> <nav> <main> <footer>`.
- **URL bersih, konsisten berbahasa Indonesia:** `/tentang`, `/proyek`, `/kontak`, `/cv` — tanpa parameter.
- `sitemap.xml` otomatis, `robots.txt`, `lang="id"`.
- Alt text deskriptif untuk semua gambar; teks tautan bermakna.
- Daftarkan ke **Google Search Console** dan **Bing Webmaster**, kirim sitemap.
- `astro.config.mjs` **wajib** menyetel `site` — dipakai sitemap, canonical, dan URL absolut di OG.
- **Strategi domain:** MVP jalan di `.vercel.app`. **URL `.vercel.app` tidak boleh ditulis permanen di README GitHub maupun LinkedIn** sampai domain custom siap. Saat migrasi: beli domain → set `site` di `astro.config.mjs` → set pengalihan 301 dari `.vercel.app` → perbarui 2 backlink.

---

## 9. Kebutuhan Non-Fungsional

### Performa (budget)

| Aspek | Batas |
|---|---|
| LCP | < 1,8 dtk (4G) |
| CLS | < 0,05 |
| INP | < 200 ms |
| JavaScript per halaman | **< 5 KB (gzip)** — 0 KB di halaman statis; ± 3 KB di `/tentang` & `/kontak` (menu mobile + lightbox) |
| Total halaman Home | < 500 KB |
| Gambar | WebP/AVIF, `width`/`height` eksplisit, `loading="lazy"` kecuali hero; foto hero ≤ 60 KB; cover proyek ≤ 120 KB |
| Efek | Glow lewat gradient CSS; tanpa `backdrop-filter`, blur besar, atau `background-attachment: fixed` |
| Font | 2 keluarga (Bebas Neue 1 bobot + Inter variable), WOFF2 + subset, **preload keduanya** |

### Aksesibilitas

- Kontras WCAG AA (termasuk teks di atas area glow), navigasi keyboard penuh, focus ring terlihat; menu hero tetap berupa tautan nyata.
- `prefers-reduced-motion` dihormati; target sentuh ≥ 44 px.
- Skip-to-content link.

### Responsif

- Mobile-first; breakpoint 640 / 768 / 1024 / 1280 px.

### Keamanan & Privasi

- HTTPS (otomatis Vercel), header dasar (CSP, X-Content-Type-Options, Referrer-Policy) via `vercel.json`.
- Tanpa form → tanpa endpoint dan tanpa spam. Email cukup ditulis apa adanya (kontak profesional, bukan data sensitif).
- Analytics tanpa cookie.

### Perawatan

- **Tidak ada tahun yang ditulis manual** di mana pun (kecuali baris "Diperbarui: …" di `/cv`, yang di-update per revisi).
- Menambah proyek = 1 file `.md`; menambah sertifikat = 1 file `.md`.

---

## 10. Struktur Informasi & Konten Awal

```
/                    Home
/tentang             Tentang (termasuk blok Sertifikat, anchor #sertifikat)
/proyek              Daftar proyek
/proyek/[slug]       Detail proyek (3)
/kontak              Kontak
/cv                  Unduh CV
/404                 Not found
```

**Proyek MVP (3):**
1. `whitehouse` — Next.js + Supabase, klien nyata → **studi kasus lengkap**
2. `klasifikasi-tb` — Klasifikasi tuberkulosis MobileNetV2 (React + Flask), skripsi → ringkas
3. `inventory-management` — Multi-User Inventory Management System (Laravel, React, Inertia.js, PostgreSQL) → ringkas

**Sertifikat awal (8):** 7 sertifikat Dicoding (Python, SQL, Data Science, AI, Pemrograman Web, JavaScript, Front-End Web) + opsional MOS Excel.

> Proyek yang belum ter-deploy sebaiknya di-deploy gratis (Vercel / Neon / Supabase free tier) atau dilengkapi video demo/GIF agar tetap "bisa dibuktikan". Bila belum ada demo, kartu ditandai eksplisit — jangan link yang tidak ada.

---

## 11. Rencana Rilis (Milestone)

| Fase | Isi | Durasi | Target |
|---|---|---|---|
| **M0 – Discovery** | Jawab 5 input (§14b); kumpulkan aset (foto profesional, CV, screenshot 3 proyek, detail PKL) | 3 hari kerja | 22–26 Okt 2026 |
| **M1 – Desain** | Review `DESIGN.md` v0.3; mockup hero (Figma opsional) | 1 hari | 27 Okt 2026 |
| **M2 – Fondasi** | Astro 6 + Tailwind v4, `src/content.config.ts`, layout, header/footer, deploy pertama | 2 hari | 28–29 Okt 2026 |
| **M3 – Halaman** | Home, Tentang, Proyek (+ 3 detail), Kontak, `/cv` | 6 hari kerja | 30 Okt – 6 Nov 2026 |
| **M4 – SEO & Performa** | Metadata, JSON-LD, OG, sitemap, optimasi gambar, audit Lighthouse | 2 hari | 9–10 Nov 2026 |
| **M5 – QA & Rilis** | QA lintas perangkat, aksesibilitas, Search Console, deploy final, backlink (README + LinkedIn) | 3 hari | 11–13 Nov 2026 |

**Total ± 17 hari kerja dalam 3,5 minggu** (22 Okt → 13 Nov). Target rilis **28 November 2026**, dengan buffer ±2 minggu untuk collection konten, revisi, dan pembelian domain custom.

---

## 12. Risiko & Mitigasi

| Risiko | Dampak | Mitigasi |
|---|---|---|
| Aset konten (foto, CV, screenshot) terlambat | Jadwal mundur | Kumpulkan di M0; mulai dari 3 proyek |
| Detail PKL tidak jelas | Halaman `/tentang` lemah | Tulis minimal 1 hasil konkret per peran |
| Angka "5 proyek" ternyata tidak akurat | Langsung merusak kredibilitas | Verifikasi jumlah sebelum menulis (§14b) |
| Proyek belum ter-deploy | Kredibilitas turun | Deploy tier gratis atau video demo; tandai eksplisit di kartu |
| URL `.vercel.app` sempat tersebar di backlink | Backlink putus saat migrasi | Jangan tulis URL di README/LinkedIn sebelum domain custom siap; 301 saat migrasi |
| Halaman jadi berat karena gambar | Skor performa turun | `astro:assets`, budget ukuran, audit tiap rilis |
| Terlalu banyak fitur | Tidak selesai-selesai | Patuhi scope MVP; sisanya backlog |
| Copy terasa generik / seperti marketing | Kredibilitas turun | Nada personal-profesional, angka konkret, tanpa jargon |
| Spam di kontak | Gangguan | Tidak ada form → tidak ada endpoint spam |

---

## 13. Backlog (Pasca-MVP)

Domain custom + pengalihan 301 · blog/catatan teknis (bagus untuk SEO jangka panjang) · versi bahasa Inggris · OG image per proyek (Satori) · halaman `/layanan` + harga · testimoni klien · arsip versi portofolio tahun lalu · toggle tema terang · filter kategori proyek · proyek terkait · proyek ke-4 ke atas (KantongVura, POS UMKM) · halaman layanan freelance terpisah.

---

## 14. Keputusan yang Dikunci (v0.3)

| # | Topik | Keputusan | Alasan singkat |
|---|---|---|---|
| 1 | Posisi | Lamaran kerja dulu; freelance = CTA sekunder | Dua audiens, dua situs. Konten & kredibilitas hanya satu |
| 2 | Peran situs | Proof artifact, bukan destination | Datang dari tautan bio/profil lain, dinilai ±20 detik |
| 3 | Navigasi | Header pill = satu-satunya nav; hero = 2 CTA | Contact sebelumnya muncul 3× di Home |
| 4 | Sertifikat | Blok di `/tentang`; hapus `/sertifikat`; nav 4 item | 7 sertifikat = bukti tier terlemah, tidak layak 1/5 slot nav |
| 5 | Bahasa | Indonesia penuh; label game `START`/`CONTACT` kept | Konsistensi; label game tetap jadi signature visual |
| 6 | Hero | Nama + intent melamar + 2 CTA + 1 baris bukti | Dalam 20 detik harus jelas: siapa, mau kerja, jalan keluarnya |
| 7 | Kontak publik | Email + LinkedIn + GitHub; WA hanya di `/kontak` | Nomor WA = vektor spam utama; "freelance" shouldn't dominate |
| 8 | 3 unggulan | Whitehouse, Klasifikasi TB, Inventory | 1 klien nyata, 1 AI/ML, 1 fullstack enterprise |
| 9 | Detail proyek | 1 lengkap + 2 ringkas | Volume tulis ~1/3; kualitas bukti tetap tinggi |
| 10 | Estetika | "Game subtle" | Pembeda visual tetap, sinyal "serius" naik |
| 11 | Baris bukti | "5 proyek selesai — React, Laravel, Node, Python" | Jumlah = terbukti; stack = kemampuan |
| 12 | Foto hero | Foto profesional 4:5, layout 2 kolom | Cutout + bentuk merah = terlalu "creative" untuk lamaran |
| 13 | Form kontak | Dibuang | Nol backend, nol spam, WA preset lebih rendah friksi |
| 14 | Penutup | Ajakan bertindak, bukan big display "TERIMA KASIH 2026" | Tahun hardcode = situs basi tiap Januari |
| 15 | Styling | Tailwind v4 CSS-first, satu blok `@theme` | Config v3 diabaikan diam-diam oleh v4; token satu tempat |
| 16 | OG image | 1 default statis untuk semua halaman | Preview link = "layar pertama" recruiter; 6+ desain tidak masuk milestone |
| 17 | Interaksi | Filter dibuang; lightbox `<dialog>` native dipertahankan | Filter untuk 5 item = UI tanpa manfaat; lightbox native ≈ 0 KB |
| 18 | Analytics | Vercel Web Analytics (cookieless) | Cukup untuk proxy "minat"; tanpa cookie banner |
| 19 | Domain | `.vercel.app` dulu → domain custom + 301 | Backlink belum ada, biaya migrasi ≈ 2 URL |
| 20 | Riwayat | PKL/magang = tulang punggung `/tentang` | Satu-satunya konteks kerja non-proyek |
| 21 | Nada | Personal-profesional | Orang, bukan template; angka konkret, tanpa jargon marketing |
| 22 | Freelance | 2–3 layanan disebut di `/kontak` + WA preset | Klien tahu apa yang bisa dipesan tanpa halaman terpisah |
| 23 | Rilis | Akhir November 2026 | 17 hari kerja + buffer |
| 24 | Pemangkasan | `/sertifikat`, filter, form, harga, blog, versi EN | Semuanya masuk backlog |
| 25 | Output | PRD + DESIGN ditulis ulang ke v0.3 | Satu sumber kebenaran |

### 14b. Input yang Masih Dibutuhkan dari Rafiq (blocking, ±30 menit)

1. **Detail PKL:** perusahaan, durasi, 1 hasil konkret.
2. **Jumlah proyek** untuk baris bukti — 5 atau 3? (Hero menulis "5 proyek selesai".)
3. **Aset siap?** foto profesional (4:5) + CV PDF terbaru.
4. **2–3 layanan freelance** yang mau disebut di `/kontak`.
5. **Kandidat nama domain** custom (dicek availability saat penulisan).

---

## 15. Definition of Done (Produk)

- [ ] 4 halaman utama + 3 detail proyek + `/cv` + 404 selesai
- [ ] 1 studi kasus lengkap + 2 halaman ringkas
- [ ] Blok sertifikat di `/tentang` + lightbox native berfungsi
- [ ] Tidak ada form, tidak ada filter, tidak ada harga
- [ ] 1 OG image default dipakai di semua halaman
- [ ] JSON-LD `Person` / `WebSite` / `BreadcrumbList` / `SoftwareSourceCode` valid (Google Rich Results Test)
- [ ] `sitemap.xml` + `robots.txt` + canonical benar, `site` terisi
- [ ] Tidak ada tahun hardcoded
- [ ] README GitHub & LinkedIn menuju domain final (bukan `.vercel.app`)
- [ ] Search Console + Bing Webmaster terpasang, sitemap dikirim
- [ ] Lighthouse mobile ≥ 95 / 100 / ≥ 95 / ≥ 95
- [ ] Semua gambar punya alt text; tidak ada tautan rusak
