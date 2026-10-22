# DESIGN.md — Website Portofolio Rafiq

**Versi:** 0.3 · **Arah visual:** Gelap sinematik (navy-hitam + glow biru), estetika "game subtle"
**Prinsip:** Konten langsung terlihat · Glow murah (CSS saja) · Cepat dan ringan · **Satu keputusan dalam 20 detik** · Konsisten
**Perubahan v0.2 → v0.3:** hero berubah dari game-menu full-bleed + foto cutout menjadi **layout 2 kolom dengan foto profesional**; bentuk merah dihapus; nav pill 5 → 4 item; penutup "TERIMA KASIH 2026" diganti CTA; konfigurasi Tailwind diganti blok `@theme` v4; filter proyek dibuang.

---

## 1. Referensi Visual & Adaptasi

Referensi: portofolio bergaya "game menu" (tema navy-hitam, glow biru, nav pill, judul kondensed tebal).

| Elemen referensi | Dipakai di website ini | Catatan performa/SEO |
|---|---|---|
| Latar navy-hitam dengan glow biru | Ya: gradient CSS | `radial-gradient`, tanpa gambar dan tanpa `filter: blur` besar |
| Judul kondensed tebal huruf besar | Ya: Bebas Neue untuk heading | 1 bobot, subset, ±15 KB |
| Nav pill di tengah atas, tab aktif biru muda | Ya: header, **4 item** | HTML/CSS murni |
| Hero foto cutout + bentuk warna di belakang | **Adaptasi:** foto profesional 4:5 + glow biru, bentuk merah dihapus | WebP ≤ 60 KB, bukan cutout transparan |
| Menu "START / OPTIONS / EXIT" | Ya, sebagai **menu tautan di hero dengan 2 item** (`START`, `CONTACT`) | Teks HTML nyata, langsung terlihat, bisa diindeks |
| Software Skills berupa ikon aplikasi | Ya: ubin ikon Tech Stack | SVG inline |
| Education / Experience / Language | Ya di `/tentang` | Language memakai bar sederhana |
| Grid proyek masonry | Ya, disederhanakan: 2 kolom + 1 kartu lebar | CSS grid, tanpa library |
| Foto bulat + ikon sosial + "Thank you" | Ya di `/kontak`; teks penutup diganti **CTA**, bukan big display | |
| Arsip portofolio tahun lalu | Backlog | Belum ada versi sebelumnya |

**Disesuaikan karena tujuan utama = lamaran kerja:** hero tidak lagi menjadi "menu game" penuh; ia adalah **blok identitas + intent + 2 jalan keluar**. Studi kasus (masalah, solusi, peran, hasil) tetap dipakai karena itu aset terbesar, tapi **1 studi kasus lengkap + 2 ringkas**, bukan 5 template identik. Sertifikat masuk ke `/tentang` sebagai blok, bukan halaman tersendiri.

---

## 2. Prinsip Desain

1. **Konten tidak boleh tertahan.** Tidak ada splash screen pemblokir; hero langsung menampilkan nama, peran, status, dan 2 CTA.
2. **Satu keputusan per layar.** Setiap halaman punya satu aksi utama yang jelas (lihat proyek / hubungi). Tidak ada features yang hanya berguna bagi penghuni situs.
3. **Tóżko Dalam 20 detik.** Di layar pertama wajib terbaca: siapa saya, apa yang bisa, apakah tersedia, dan ke mana harus klik.
4. **Gelap dengan satu aksen biru.** Tidak ada warna kedua. Aksen merah `#E11D48` yang dipakai di v0.2 untuk bentuk di belakang foto hero **dihapus** — bentuk itu sendiri juga tidak lagi dipakai, sehingga palet hanya punya satu aksen.
5. **Efek murah.** Glow lewat gradient CSS; hindari `backdrop-filter`, blur besar, dan animasi berat.
6. **Aksesibel.** Kontras AA di tema gelap, fokus terlihat, navigasi keyboard penuh.

---

## 3. Design Tokens

> **Prinsip:** token didefinisikan **tepat satu kali**, di blok `@theme` pada `src/styles/global.css` (lihat §9). Tidak ada `tailwind.config.mjs`, tidak ada warna hex yang ditulis ulang di komponen.

### 3.1 Warna

| Token | Nilai | Penggunaan |
|---|---|---|
| `--color-bg` | `#05080F` | Latar utama (hampir hitam) |
| `--color-navy` | `#07182B` | Ujung bawah gradient latar |
| `--color-surface` | `#0C1424` | Kartu, panel |
| `--color-surface-2` | `#111C30` | Hover kartu, input |
| `--color-line` | `rgba(148,163,184,.16)` | Garis, border kartu |
| `--color-ink` | `#E6EDF7` | Teks utama |
| `--color-muted` | `#94A3B8` | Teks sekunder |
| `--color-accent` | `#60A5FA` | Tautan, ikon, highlight |
| `--color-accent-strong` | `#3B82F6` | CTA primer, glow |
| `--color-accent-pill` | `#BFDBFE` | Latar tab nav aktif |
| `--color-ok` | `#22C55E` | Status "Tersedia untuk posisi full-time" |
| `--color-focus` | `#93C5FD` | Focus ring 2 px, offset 2 px |
| ~~`--color-crimson`~~ | ~~`#E11D48`~~ | **Dihapus v0.3** — tidak lagi dipakai |

**Latar halaman**
```css
body {
  background:
    radial-gradient(60% 40% at 15% 0%, rgba(14,90,160,.45), transparent 70%),
    linear-gradient(180deg, var(--color-bg) 0%, var(--color-navy) 100%);
  background-attachment: scroll; /* jangan fixed: berat di mobile */
  color: var(--color-ink);
  color-scheme: dark;
}
```

### 3.2 Tipografi

| Peran | Font | Catatan |
|---|---|---|
| Display / heading | **Bebas Neue** (1 bobot, self-hosted, subset Latin, WOFF2) | Dipakai untuk H1, H2, label besar |
| Body / UI | **Inter** (variable, self-hosted, subset) | Bobot 400–600 |
| Kode / tag teknis | `ui-monospace, SFMono-Regular, Menlo, monospace` | Font sistem |

Fallback display: `Impact, "Arial Narrow", sans-serif` dengan `size-adjust` agar tidak terjadi layout shift. `font-display: swap`.

> **Penting (v0.3):** Inter dipakai **di atas lipatan** (pill status, baris bukti, label CTA). Karena itu **kedua font di-preload**, bukan hanya font hero — kalau Inter swap belakangan, CLSalbeit di007 exceed 0,05. Gunakan `<link rel="preload" as="font" type="font/woff2" crossorigin>` untuk keduanya di `BaseLayout.astro`.
> Astro 6 sudah menstabilkan API font bawaan (`experimental.fonts` → stabil); API ini bisa menggantikan manajemen file font manual. Verifikasi sintaks saat implementasi — jangan implementasi dua kali.

| Level | Mobile | Desktop | Line-height | Letter-spacing |
|---|---|---|---|---|
| Display (hero h1) | 56 px | 112 px | 0.95 | 0.01em |
| H2 | 36 px | 56 px | 1.0 | 0.02em |
| H3 (Inter 600) | 20 px | 22 px | 1.3 | 0 |
| Body (Inter) | 16 px | 17 px | 1.65 | 0 |
| Caption | 13 px | 14 px | 1.5 | 0.02em |

> Heading display: tulis teks **normal** di HTML, kapitalkan via CSS `text-transform: uppercase` — supaya pembaca layar dan SEO tetap membaca "Rafiq Setyo Aji".

### 3.3 Spasi, Radius, Bayangan

- Skala 4 px: `4 · 8 · 12 · 16 · 24 · 32 · 48 · 64 · 96 · 128`
- Jarak antar-section: 64 px (mobile) / 96 px (desktop). Lebar konten maks **1120 px**; teks panjang maks 68 karakter/baris.
- Radius: `sm` 6 px · `card` 12 px · `panel` 20 px · `full` 9999 px (pill, avatar)
- Bayangan hampir tidak dipakai di tema gelap; ganti dengan border 1 px `--color-line` dan perubahan `--color-surface-2` saat hover. Glow aksen opsional: `0 0 0 1px rgba(96,165,250,.35), 0 8px 32px rgba(59,130,246,.18)`.

### 3.4 Breakpoint & Grid

`sm` 640 · `md` 768 · `lg` 1024 · `xl` 1280 — **sama dengan default Tailwind v4**, jadi tidak perlu token breakpoint tambahan. Mobile-first; 4 kolom (mobile), 8 (md), 12 (lg+). Gutter 16 px / 24 px.

### 3.5 Gerak

- 150 ms (hover), 250 ms (menu). Easing `ease-out`. Hanya `opacity` dan `transform`.
- Hero: fade/slide-up ringan saat muat (maks 400 ms), tidak menunda tampilan teks.
- Hormati `@media (prefers-reduced-motion: reduce)` → matikan semua transisi.

---

## 4. Komponen

### 4.1 Header (Nav Pill)
- Logo monogram "R" (SVG inline) di kiri → link `/`.
- Di tengah: **kapsul pill 4 item** — Home · Tentang · Proyek · Kontak.
- Tab aktif: latar `--color-accent-pill`, teks `#0B1220`, radius penuh. Tab lain: teks `--color-muted`, hover `--color-ink`.
- Posisi sticky, latar solid `rgba(5,8,15,.85)` (tanpa `backdrop-filter`).
- Kanan (desktop): tombol kecil **"Hubungi Saya"** → `/kontak`.
- Mobile: tombol hamburger 44×44 px membuka **`<dialog>`** berisi nav vertikal; `Esc` menutup; fokus dikembalikan ke pemicu; focus ring terlihat di dalam panel.
- Skip link "Lewati ke konten".

### 4.2 Hero 2 Kolom (Home)
Langsung terlihat saat halaman dimuat, tanpa splash.

```
┌───────────────────────────────────────────────────────────────────┐
│  ┌──────────────┐   OPEN TO WORK                                   │
│  │              │   RAFIQ SETYO AJI            ← H1, display      │
│  │  foto 4:5    │   Fullstack Web Developer                        │
│  │  + glow      │   ● Tersedia untuk posisi full-time              │
│  └──────────────┘   Membangun web app yang jalan di dunia nyata.   │
│                     5 proyek selesai — React, Laravel, Node, Python │
│                                                                   │
│                     ▸ START     Lihat Proyek    → /proyek           │
│                       CONTACT   Hubungi Saya    → /kontak           │
└───────────────────────────────────────────────────────────────────┘
```

- **Kolom kiri:** foto profesional (bukan cutout), rasio 4:5, radius `card`, dengan glow biru di belakang (radial-gradient, tanpa blur besar). Bentuk merah **tidak ada**.
- **Kolom kanan:** eyebrow "OPEN TO WORK" (Inter, uppercase, letter-spacing 0.12em, `--color-muted`) → H1 display → sub-peran → pill status hijau → 1 kalimat nilai → **baris bukti** → 2 CTA.
- **Menu = 2 item** (bukan 3): `START` dan `CONTACT`. Penanda `▸` muncul pada item yang di-hover atau difokus; penanda **bukan** satu-satunya indikator (ada juga perubahan warna + underline). Urut Tab natural.
- **Mobile:** foto di atas (maks 40 vh), teks dan CTA di bawah; CTA menjadi tombol penuh.
- Foto: WebP, ≤ 60 KB, `fetchpriority="high"`, `width`/`height` eksplisit.

### 4.3 Tombol
| Varian | Gaya |
|---|---|
| Primary | Latar `--color-accent-strong`, teks putih, radius 10 px, padding 12×22, hover lebih terang |
| Secondary | Transparan, border `--color-line`, teks `--color-ink`, hover `--color-surface-2` |
| Link | Teks `--color-accent`, panah →, underline saat hover |

Tinggi minimum 44 px; state: hover, focus-visible, active, disabled.

### 4.4 Ubin Tech Stack
Ubin persegi rounded (64×64), latar `--color-surface`, border `--color-line`, ikon SVG inline di tengah, nama tech di bawah (Inter 13 px, `--color-muted`). Grid 4 kolom (mobile) → 6 kolom (≥768 px).

### 4.5 Kartu Proyek
- Latar `--color-surface`, border 1 px `--color-line`, radius `card`.
- **Kartu unggulan pertama** `grid-column: span 2` (lebar penuh, cover 21:9); kartu biasa cover 16:10.
- Judul H3, ringkasan 2 baris, badge kategori + badge tech, tautan "Lihat studi kasus →".
- Seluruh kartu satu `<a>` utama. Hover: border aksen + naik 2 px.
- **Grid:** 1 kolom (mobile) → 2 kolom (≥768 px) dengan `grid-auto-flow: dense`. Tanpa filter, tanpa span acak.
- Urutan DOM = urutan baca. Kartu tanpa demo ditandai badge "Belum ter-deploy" — **jangan** link yang tidak ada.

### 4.6 Kartu Sertifikat
Thumbnail 4:3 (lazy-load, ≤ 40 KB), judul, penerbit, tanggal, tombol "Verifikasi" → tautan sumber. Dikelompokkan per kategori (Pemrograman / Data-AI / Lainnya). Lightbox memakai **`<dialog>` native** (≈ 0 KB JS) berisi gambar sertifikat penuh.

### 4.7 Badge
Pill, latar `rgba(96,165,250,.12)`, teks `--color-accent`, 12–13 px, font mono. Varian: kategori (netral), status (hijau `--color-ok`).

### 4.8 Blok Tentang
- Grid dua kolom: foto (glow di belakang) dan cerita.
- Di bawahnya blok: **Pengalaman (PKL)** · **Pendidikan** · **Keahlian** · **Bahasa** (bar tipis + teks persentase/level untuk aksesibilitas).
- **Blok Sertifikat** (`id="sertifikat"`): sub-heading + 3 kelompok kategori + kartu sertifikat (§4.6) + lightbox.
- CTA: tombol unduh CV → `/cv`.

### 4.9 Blok Kontak + Penutup
Foto bulat (border aksen), daftar kontak dengan ikon (email, LinkedIn, GitHub, WhatsApp), blok "Layanan freelance" (2–3 butir singkat), teks "Balas dalam 24 jam kerja". **Tidak ada form.**
Penutup = **ajanakan bertindak** (heading + 1 kalimat + tombol), bukan big display tahun. Tanpa teks "TERIMA KASIH 2026".

### 4.10 Footer
Latar `--color-bg`, border atas. Tiga kolom (identitas · navigasi · sosial), © dengan **tahun otomatis** (`new Date().getFullYear()` — tidak pernah ditulis manual), tombol "Kembali ke atas".

---

## 5. Layout Halaman

| Halaman | Urutan section |
|---|---|
| **Home** `/` | Hero 2 kolom → Proyek unggulan (3) → Tech Stack → Sertifikat terbaru → CTA penutup |
| **Tentang** `/tentang` | Foto + cerita → Pengalaman (PKL) · Pendidikan · Keahlian · Bahasa → Sertifikat → Unduh CV |
| **Proyek** `/proyek` | Judul + 1 kalimat → grid (1 kartu lebar + 2 kartu) |
| **Detail proyek** `/proyek/[slug]` | Breadcrumb → H1 + ringkasan + badge + [Live Demo] [GitHub] → cover → isi (format lengkap atau ringkas) → galeri → CTA ke `/kontak` |
| **Kontak** `/kontak` | Foto bulat + kontak → Layanan freelance → Penutup CTA |
| **CV** `/cv` | Ringkas: foto + nama + tombol unduh |
| **404** | 1 kalimat + link Home + Proyek |

---

## 6. Gambar & Ikon

- Format WebP/AVIF; **1** OG image 1200×630 (tema gelap, nama + peran) dipakai lintas halaman.
- Foto profesional 4:5 ≤ 60 KB; cover proyek ≤ 120 KB; thumbnail sertifikat 4:3 ≤ 40 KB.
- `width`/`height` selalu diisi (cegah CLS); hero `fetchpriority="high"`, lainnya `loading="lazy"`.
- Ikon: SVG inline, hanya yang dipakai (Lucide / Simple Icons). Logo monogram "R" inline SVG.
- Favicon set: `favicon.ico`, `favicon-512.png`, `apple-touch-icon.png`.
- Alt text deskriptif.

---

## 7. Aksesibilitas (Checklist)

- [ ] Teks utama dan muted lolos kontras ≥ 4,5:1 di atas `--color-bg` dan `--color-surface`
- [ ] Teks di atas glow/gradient tetap ≥ 4,5:1 (uji titik terterang)
- [ ] Teks pill aktif `#0B1220` di atas `--color-accent-pill` ≥ 7:1
- [ ] Focus ring terlihat di semua elemen interaktif
- [ ] Menu hero bisa dioperasikan keyboard; penanda `▸` bukan satu-satunya indikator (ada juga perubahan warna/underline)
- [ ] Landmark `header / nav / main / footer`, satu `h1` per halaman
- [ ] Heading display huruf kapital: teks normal di HTML + `text-transform: uppercase`
- [ ] Target sentuh ≥ 44×44 px
- [ ] Dialog (menu mobile, lightbox) menutup dengan `Esc` dan mengembalikan fokus ke pemicu
- [ ] `prefers-reduced-motion` dihormati; `lang="id"`

---

## 8. Desain untuk SEO & Performa

- Semua teks hero (nama, peran, baris bukti, CTA) berupa HTML, bukan gambar; tidak ada splash yang menahan render.
- Aset besar di atas lipatan hanya foto hero; glow dari CSS.
- Hindari `filter: blur`, `backdrop-filter`, `box-shadow` besar pada banyak elemen, dan `background-attachment: fixed`.
- Font: 2 keluarga (Bebas Neue 1 bobot + Inter variable), subset, **preload keduanya**.
- Tambahkan `<meta name="theme-color" content="#05080F">` dan `color-scheme: dark`.
- JavaScript hanya untuk: menu mobile (`<dialog>`), lightbox (`<dialog>`). **Tanpa filter, tanpa animasi scroll, tanpa library.**
- Budget: LCP < 1,8 dtk, CLS < 0,05, Home < 500 KB, JS < 5 KB (gzip).

---

## 9. Konfigurasi Tailwind v4 (CSS-first)

> **v0.3:** Tailwind v4 tidak memakai `tailwind.config.mjs`. Seluruh token didefinisikan di blok `@theme` pada `src/styles/global.css`. Konfigurasi versi 3 pada `DESIGN.md` v0.2 **akan diabaikan diam-diam** — dipindah ke sini agar tidak terpakai.

Pemasangan: `npx astro add tailwind` (Tailwind v4 + plugin Vite). Bila tool itu memasang `@astrojs/tailwind` versi 3, hapus dan pakai `@tailwindcss/vite` + `@import "tailwindcss"`.

```css
/* src/styles/global.css */
@import "tailwindcss";

@theme {
  /* Warna */
  --color-bg: #05080F;
  --color-navy: #07182B;
  --color-surface: #0C1424;
  --color-surface-2: #111C30;
  --color-line: rgba(148,163,184,.16);
  --color-ink: #E6EDF7;
  --color-muted: #94A3B8;
  --color-accent: #60A5FA;
  --color-accent-strong: #3B82F6;
  --color-accent-pill: #BFDBFE;
  --color-ok: #22C55E;
  --color-focus: #93C5FD;

  /* Tipografi */
  --font-display: "Bebas Neue", Impact, "Arial Narrow", sans-serif;
  --font-sans: Inter, system-ui, -apple-system, "Segoe UI", Roboto, sans-serif;
  --font-mono: ui-monospace, SFMono-Regular, Menlo, monospace;

  --text-display: 56px;
  --text-display--line-height: 0.95;
  --text-display--letter-spacing: 0.01em;
  --text-display-lg: 112px;
  --text-display-lg--line-height: 0.95;
  --text-display-lg--letter-spacing: 0.01em;
  --text-h2: 36px;
  --text-h2--line-height: 1;
  --text-h2--letter-spacing: 0.02em;
  --text-h2-lg: 56px;
  --text-h2-lg--line-height: 1;
  --text-h2-lg--letter-spacing: 0.02em;
  --text-h3: 20px;
  --text-h3--line-height: 1.3;
  --text-h3-lg: 22px;
  --text-h3-lg--line-height: 1.3;
  --text-body: 16px;
  --text-body--line-height: 1.65;
  --text-body-lg: 17px;
  --text-body-lg--line-height: 1.65;
  --text-caption: 13px;
  --text-caption--line-height: 1.5;
  --text-caption--letter-spacing: 0.02em;
  --text-caption-lg: 14px;
  --text-caption-lg--line-height: 1.5;
  --text-caption-lg--letter-spacing: 0.02em;

  /* Radius & lebar */
  --radius-card: 12px;
  --radius-panel: 20px;
  --container-page: 1120px;
}

@layer base {
  body {
    background:
      radial-gradient(60% 40% at 15% 0%, rgba(14,90,160,.45), transparent 70%),
      linear-gradient(180deg, var(--color-bg) 0%, var(--color-navy) 100%);
    background-attachment: scroll;
    color: var(--color-ink);
    color-scheme: dark;
  }
}
```

**Catatan:**
- Token di namespace `--color-*`, `--font-*`, `--text-*`, `--radius-*`, `--container-*` menghasilkan utilitas otomatis: `bg-surface`, `text-muted`, `font-display`, `text-display`, `lg:text-display-lg`, `rounded-card`, `max-w-page`.
- Kalau token perlu selalu tersedia sebagai CSS custom property (mis. untuk `style` inline pada SVG), pakai `@theme static { … }` — tanpa itu Tailwind hanya memancarkan token yang terpakai.
- Breakpoint default Tailwind v4 sudah cocok dengan §3.4.

---

## 10. Struktur Folder

```
src/
  components/     Header.astro, Footer.astro, Hero.astro, ProjectCard.astro,
                  CertCard.astro, TechTile.astro, Badge.astro, Button.astro,
                  SectionHeading.astro
  content/
    projects/     whitehouse.md, klasifikasi-tb.md, inventory-management.md
    certs/        *.md   (title, issuer, date, url, image, category)
  content.config.ts        ← WAJIB (Astro 5+, Content Layer)
  layouts/       BaseLayout.astro  (meta SEO, OG, JSON-LD, header, footer)
  pages/         index.astro, tentang.astro, kontak.astro, cv.astro, 404.astro,
                 proyek/index.astro, proyek/[slug].astro
  styles/        global.css   ← satu-satunya sumber design token
  assets/        images/, fonts/
public/          favicon.ico, favicon-512.png, apple-touch-icon.png,
                 og-default.png, cv.pdf, robots.txt
astro.config.mjs
vercel.json
```

**Aturan Astro 5/6 yang wajib dijaga (v0.3):**
- Skema koleksi berada di **`src/content.config.ts`** (bukan di dalam `src/content/`), memakai loader `glob()`.
- Entry koleksi **tidak punya `slug`** — field-nya `id`; sesuaikan `getStaticPaths()` di `proyek/[slug].astro`.
- `render()` diimpor dari `astro:content`, bukan method pada entry.
- Gambar dalam frontmatter memakai helper `image()` agar bisa diolah `astro:assets`.
- `astro.config.mjs` wajib menyetel `site` (sitemap, canonical, URL absolut OG).

---

## 11. Definition of Done (Desain)

- [ ] Tampilan konsisten di 360, 768, 1280 px
- [ ] Token hanya didefinisikan di satu tempat (blok `@theme` di `src/styles/global.css`); tidak ada `tailwind.config.mjs`
- [ ] Hero 2 kolom: foto profesional 4:5 + nama + intent + baris bukti + 2 CTA, tanpa splash, tanpa waiting JS
- [ ] Nav pill tepat 4 item, tab aktif ditandai, `aria-current="page"`
- [ ] `/tentang` memuat blok Sertifikat + lightbox `<dialog>` yang bisa ditutup `Esc`
- [ ] Tidak ada form, tidak ada filter, tidak ada big display tahun
- [ ] Semua gambar punya alt text; tidak ada tautan rusak; tombol demo/github hanya tampil bila tautannya ada
- [ ] Tahun di footer dihitung otomatis, tidak ada tahun hardcoded di sumber
- [ ] Lighthouse mobile: Performance ≥ 95, Accessibility ≥ 95, SEO 100; CLS < 0,05; JS < 5 KB
- [ ] Kontras diuji di area dengan glow
