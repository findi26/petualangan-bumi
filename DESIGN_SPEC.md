# Design Spec - Petualangan Ke Bawah Tanah Bumi

Versi 1.0 · 26 November 2026

Dokumen ini merinci spesifikasi desain UI/UX untuk game edukatif "Petualangan Ke Bawah Tanah Bumi" (web, responsif mobile-first).

## 1. Prinsip Desain

- Visual hangat, cerah, dan ramah anak (usia 6-10 tahun).
- Satu fokus utama per layar (Molie + konten utama).
- Interaksi "sentuh untuk tahu": hotspot, kartu level, tombol besar.
- Animasi halus, tidak berlebihan, dengan tujuan UX (feedback, transisi, reward).
- Aksesibilitas: teks minimal 20pt, tombol minimal 60x60 px, kontras WCAG AA, keyboard navigable.

## 2. Palet Warna

| Elemen | Hex |
|---|---|
| Langit / latar luar | #87CEEB |
| Rumput | #7BC96F |
| Kerak | #C68642 |
| Mantel | #FF8C42 |
| Inti Luar | #FF4E3A |
| Inti Dalam | #FFD93D |
| Tombol utama (ungu) | #9B5DE5 |
| Tombol utama (gelap) | #7A3FC4 |
| Bintang / emas | #FFCC00 |
| Teks utama | #4A2C00 |
| Krem latar kartu | #FFF8ED |
| Sukses (hijau) | #4CC38A |
| Gagal (merah) | #FF6B5E |

Aturan: maksimal 2-3 warna inti + 1 aksen per layar. Netral (putih, krem, abu) tidak dihitung.

## 3. Tipografi

- Font utama: Fredoka (400, 500, 600, 700) dari Google Fonts.
- Fallback: Baloo 2, system-ui, Segoe UI, sans-serif.
- Judul game: 1.9-2.8rem, weight 700, warna putih dengan shadow ungu.
- Judul layar (h2): 1.15rem, weight 600.
- Teks bubble/soal: 1.08rem, weight 500.
- Teks tombol: 1.15rem (normal), 1.5rem (besar).
- Teks kecil (info, hint): 0.82-0.95rem.

## 4. Karakter - Molie

Tikus tanah lucu: kacamata bulat, pipi merah, helm kuning dengan lentera.

Ekspresi:
- Idle: animasi bob (translateY 0-10px, rotasi -1 sampai 1 derajat), durasi 2.8s loop.
- Senang (jawaban benar): jump (translateY -34px, scale), durasi 0.55s.
- Sedih ringan (jawaban salah): headshake (rotasi -8 sampai 8 derajat), durasi 0.5s.

Ukuran default:
- Menu: 190px
- Kuis: 100px
- Reward: 150px
- Poster info: 85px

## 5. Layout Global

- Container `.app`: max-width 920px, centered, height 100dvh.
- Layar `.screen`: absolute inset 0, flex column, padding 14px 18px 20px, scroll vertical.
- Transisi layar: fade + slide (opacity 0->1, translateY 18px->0, scale 0.98->1), durasi 0.45s.
- Latar: gradien langit 180deg (#B8E6FF -> #87CEEB -> #9BE0A8), awan bergerak (drift).

## 6. Spesifikasi Layar

### 6.1 Menu Utama

- Top bar: chip total bintang (kiri), spacer, tombol suara & musik (kanan).
- Hero: Molie 190px, judul "Petualangan / Ke Bawah Tanah Bumi", tagline, tombol MULAI besar (ungu), baris Profil & Atur, tanggal hari ini.
- Awan bergerak di latar (3 cloud, drift).

### 6.2 Poster Teori

- Top bar: tombol back, judul "Kenali Lapisan Bumi", chip bintang.
- Depth bar: 4 pill lapisan (Kerak, Mantel, Inti Luar, Inti Dalam), berubah ✓ saat dikunjungi.
- Poster frame: gambar (configurable) atau fallback SVG 4 lingkaran konsentris, max-height 48vh.
- 4 hotspot bernomor (posisi persen via config), ring pulse, berubah hijau ✓ setelah dikunjungi.
- Hint teks: "Ketuk titik bernomor di poster untuk belajar!"
- Progress bar 0/4 sampai 4/4.
- Info panel: Molie 85px + kartu info (emoji, judul lapisan, deskripsi, fact card).
- Tombol "Mulai Petualangan" disabled sampai 4/4; aktif + konfeti + narasi.

### 6.3 Peta Level

- Top bar: tombol back, judul "Peta Lapisan Bumi", chip bintang.
- Tombol "Lihat Teori Poster".
- Daftar 4 kartu level: emoji badge, nomor, nama, sub, bintang (0-3), ikon ▶ atau 🔒.
- Level terkunci: grayscale + brightness 0.85, tidak bisa klik.
- Animasi cardIn (slide dari kiri, stagger 0.08s).

### 6.4 Kuis

- Top bar: tombol back, judul "Level N · Nama", chip bintang.
- Progress dot: jumlah soal, dot aktif untuk soal ke-n.
- Speech row: Molie 100px + bubble soal (narasi suara otomatis).
- Options: grid 2 kolom, 4 tombol (emoji + teks). Benar: hijau + pulse; salah: merah + shake + disabled sementara.
- Jawaban salah tidak dianggap gagal permanen; anak boleh coba lagi.

### 6.5 Layar Apresiasi (Reward)

- Molie 150px, judul "LUAR BIASA!/HEBAT!/BAGUS!", 3 bintang pop satu per satu, pesan poin, lencana baru (jika level pertama kali lulus), tombol Ulang & Lanjut.
- Konfeti 30 butir.

### 6.6 Profil

- 2 stat: total bintang & poin.
- Grid 4 lencana (terbuka/terkunci).

### 6.7 Pengaturan

- Panel toggle: Suara, Musik, Narasi Suara.
- Panel info versi + tombol Reset Progres (konfirmasi).

## 7. Komponen UI

### Tombol (.btn)
- Radius 22px, padding 16px 26px, font 1.15rem, shadow 3D (6px bawah).
- Varian: primary (ungu), ghost (putih), green (hijau), big (font 1.5rem, radius 28px).
- State disabled: opacity 0.55, cursor not-allowed.
- Active: translateY 5px.

### Icon Button (.icon-btn)
- 48x48px, radius 16px, putih, shadow 4px.

### Chip (.chip)
- Pill, putih, shadow 4px, gap 6px.

### Hotspot (.hotspot)
- Lingkaran 44px, emas, border 3px putih, ring pulse (animasi 1.8s).
- Visited: hijau, tanda ✓, tanpa ring.

### Option (.option)
- Radius 24px, border 4px putih, shadow 7px, animasi optIn (stagger 0.06s).

## 8. Animasi Wajib

| Nama | Elemen | Deskripsi |
|---|---|---|
| bob | Molie idle | translateY 0-10px, rotasi -1 sampai 1 deg, 2.8s loop |
| jump | Molie benar | translateY -34px, scale 1.06/0.94, 0.55s |
| headshake | Molie salah | rotasi -8, 8, -5, 5 deg, 0.5s |
| drift | Awan | translateX ke kanan, durasi 38-64s |
| cardIn | Kartu level | slide dari kiri, fade, 0.5s stagger |
| optIn | Opsi kuis | slide dari bawah, fade, 0.35s stagger |
| popIn | Info panel, bubble | scale 0.9->1, 0.35s |
| hotspotRing | Hotspot | scale 1->1.9, opacity 0.7->0, 1.8s loop |
| starPop | Bintang reward | scale 0->1.35->1, rotasi -90->10->0, 0.6s |
| fall | Konfeti | translateY -40px->105vh, rotasi 0->540deg, 1.6-3.0s |
| floatUp | Bintang mengambang | translateY 0->-140px, scale 0.7->1.4, 0.9s |
| pulseGood | Opsi benar | scale 1->1.06->1, 0.5s |
| shake | Opsi salah | translateX -9, 9, -5, 0, 0.4s |
| screenIn | Layar | fade + slide + scale, 0.45s |

## 9. Aksesibilitas (NFR)

- Semua interaktif adalah `<button>` atau `<a href>`; tidak ada div klik.
- Icon-only button memiliki `aria-label`; ikon dekoratif `aria-hidden="true"`.
- Gambar memiliki `alt` (poster fallback SVG memiliki role img + aria-label).
- Viewport tanpa `user-scalable=no` / `maximum-scale=1`.
- Semua media (img) memiliki width/height.
- Focus outline tidak dihapus tanpa pengganti.
- `prefers-reduced-motion`: animasi panjang (>5s) harus bisa dijeda (catatan: konfeti auto-remove 3.2s, awan loop; pertimbangkan pause untuk pengguna sensitif gerak pada versi berikutnya).

## 10. Responsif

- Mobile-first (320px ke atas).
- Breakpoint utama: default mobile, tablet (>=768px), desktop (max 920px container).
- Grid opsi tetap 2 kolom; poster max-height 48vh.
- Tidak ada horizontal overflow; semua teks dalam container.

## 11. Aset

- Poster: PNG/JPG/SVG, maks 2 MB, disarankan 1600x2000 px, rasio 4:5 atau 1:1.
- Font: Google Fonts (Fredoka).
- Audio: Web Audio API (tone sintetis) + SpeechSynthesis (id-ID). Tidak ada file audio eksternal (ukuran kecil).
- Karakter: SVG inline (Molie).

## 12. Struktur File Repo

```
petualangan-bumi/
  index.html        # Game (single file, self-contained)
  README.md         # Dokumentasi proyek
  DESIGN_SPEC.md    # Spesifikasi desain (dokumen ini)
```

## 13. Catatan Implementasi

- Single-file HTML (CSS + JS inline) untuk kemudahan deploy GitHub Pages.
- State disimpan di localStorage (key: molie-bumi-v1).
- POSTER_CONFIG memudahkan penggantian gambar poster & koordinat hotspot.
- Narasi suara menggunakan SpeechSynthesis dengan lang id-ID.