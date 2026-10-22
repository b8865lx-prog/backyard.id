# Backyard.id Landing Page (Fase 1)

Landing page open-play mini soccer Backyard.id. Satu file HTML statis, tanpa backend, tanpa login. Semua konten yang sering berubah ada di satu blok bernama `CONFIG` di dalam `index.html`. **Admin cukup edit blok itu, tidak perlu menyentuh bagian lain.**

## Isi repo

```
index.html          <- halaman utama (konten diedit di blok CONFIG)
README.md           <- panduan ini
assets/
  action-1.jpg ... action-6.jpg   <- foto carousel "In Action"
  og-image.jpg                    <- gambar preview saat link dibagikan (1200x630)
  (foto lain: Photo of the Week, galeri Vol. 1)
```

## Cara edit lewat GitHub (tanpa install apa-apa)

1. Buka repo di GitHub, klik file `index.html`.
2. Klik ikon **pensil** (Edit this file) di kanan atas.
3. Tekan `Ctrl+F` (atau `Cmd+F`), cari kata `OWNER EDIT MINGGUAN` atau `const CONFIG` untuk loncat ke blok konten.
4. Ubah nilainya, lalu klik **Commit changes** di kanan atas, **Commit directly to the main branch**.
5. Tunggu 1-2 menit, lalu buka website dan refresh keras (HP: tutup tab lalu buka lagi; laptop: `Ctrl+Shift+R`).

Untuk upload foto: buka folder `assets`, **Add file** -> **Upload files**, lalu commit.

### Aturan biar kode nggak rusak
- Teks selalu di dalam tanda kutip dua `"..."`. Jangan hapus kutipnya.
- Jangan pakai tanda kutip dua `"` di tengah teks. Pakai kutip tunggal `'` atau tulis ulang kalimatnya.
- Setiap baris dalam daftar diakhiri koma `,` (kecuali baris terakhir boleh tanpa koma).
- Jangan tulis kode HTML di dalam teks, nanti tampil apa adanya.
- Jangan ubah nama field di sebelah kiri titik dua (contoh `title:`). Ubah hanya nilai di kanannya.
- Salah edit? Di GitHub buka **History** pada file lalu kembalikan ke versi sebelumnya.

## Checklist update tiap event (rutin)

Semua ada di blok `event` dan `photoOfTheWeek`:

| Field | Isi | Contoh |
|---|---|---|
| `active` | `true` = tampil jadwal. `false` = tampil "Sesi berikutnya segera hadir" | `true` |
| `title` | Nama sesi | `"Backyard MinSoc Vol. 3"` |
| `dateTime` | Tanggal dan jam | `"Sabtu, 14 November 2026 \| 16:00 - 18:00 WIB"` |
| `venue` | Nama lapangan (otomatis ikut tampil di STEP 02) | `"Nama Lapangan, Jakarta Selatan"` |
| `venueMapUrl` | Link Google Maps lapangan | lihat di bawah |
| `price` dan `priceUnit` | Harga. Format `Rp70.000` | `"Rp70.000"` dan `"/ orang"` |
| `totalSlots` | Total kuota | `20` |
| `remainingSlots` | **Sisa slot. Update manual tiap ada yang bayar** | `8` |
| `photoOfTheWeek` | `caption` dan `imageUrl` (mis. `"assets/potw.jpg"`) | |

Catatan:
- Angka (`20`, `8`) **tanpa tanda kutip**.
- Tanda `\|` di `dateTime` boleh diganti `-` kalau bikin bingung.
- Progress bar otomatis berubah **amber** saat sisa slot di bawah 30%.
- Kalau sesi belum ada, set `active: false`. Semua tombol (navbar, bar bawah di HP, kartu jadwal) otomatis jadi "Gabung Komunitas" ke WhatsApp.

**Cara ambil link Google Maps:** buka lokasi di Google Maps -> **Share/Bagikan** -> **Copy link** -> tempel ke `venueMapUrl`. Kalau dikosongkan, tombol "Lihat Lokasi" tidak muncul.

## Konten lain di CONFIG

| Blok | Fungsi |
|---|---|
| `whatsappNumber` (di `event`) | Nomor WA tujuan booking. Format internasional **tanpa `+` dan tanpa 0 di depan**, mis. `6289654362479` |
| `reclubUrl` (di `event`) | Opsional. Kalau diisi, muncul link kecil Reclub di bawah tombol booking. Saat ini dikosongkan karena Reclub sudah di footer |
| `actionCarousel.photos` | Daftar foto carousel "In Action". Tambah/kurang bebas, tulis path-nya, mis. `"assets/action-7.jpg"`. `autoplayMs` = kecepatan geser otomatis (ms), `0` = mati |
| `gallery` | 6 foto dokumentasi Vol. 1. Slot kosong (`""`) tampil placeholder |
| `testimonials` | Daftar testimoni: `name`, `rating` (1-5), `quote`, `visible` (`true`/`false` buat tampil/sembunyikan) |
| `faq` | Daftar tanya-jawab: `q` (pertanyaan) dan `a` (jawaban). Urutan tampil = urutan di daftar |
| `community` | `whatsappCommunityUrl`, `instagramUrl`, `reclubUrl`, `ayoUrl`. Kosongkan salah satu kalau tidak mau ditampilkan |
| `tracking.metaPixelId` | ID Meta Pixel. Kosong = pixel tidak aktif |
| `hero` | Video hero (opsional, lihat catatan di bawah) |

Foto yang path-nya belum ada filenya otomatis tampil placeholder, bukan gambar rusak.

### Tips foto
- Format JPG atau WebP, lebar sekitar 1200-1600 px, usahakan **di bawah 300 KB per foto** supaya halaman ringan di HP.
- Foto carousel paling pas rasio portrait 4:5. Foto lain bebas, otomatis dipotong rapi.
- Nama file huruf kecil, tanpa spasi (pakai tanda `-`).

### Video hero
Saat ini hero menampilkan placeholder. Kalau mau diisi, `hero.videoUrl` hanya mendukung **link langsung file video (.mp4)**, **bukan link YouTube**. Dukungan embed YouTube belum ada dan perlu penambahan kode.

## Gambar preview link (og-image)

Gambar yang muncul saat link dibagikan di WhatsApp, IG, Facebook, dan X.
- Ukuran **1200 x 630 px**, JPG, di bawah 300 KB.
- Simpan di `assets/og-image.jpg`.
- Isi: satu foto action terbaik + logo dan tagline di tengah. Hindari teks kecil, harga, atau tanggal (cepat basi).
- Kalau gambar baru belum muncul saat dibagikan, itu cache. Tes ulang lewat **Facebook Sharing Debugger**.

## Meta Ads dan tracking

Setelah `metaPixelId` diisi, halaman otomatis mengirim:
- `PageView` saat halaman dibuka
- `ViewContent` saat bagian Jadwal terlihat
- `Lead` saat tombol booking diklik, dengan parameter `source` = `whatsapp`, `reclub`, atau `ayo`

Parameter UTM dari link iklan ikut tercatat di event `Lead`. Pakai format link iklan seperti ini:

```
https://backyard.id/?utm_source=meta&utm_medium=paid_social&utm_campaign=vol3&utm_content=video1
```

Ganti `utm_campaign` dan `utm_content` per iklan supaya kelihatan iklan mana yang menghasilkan booking.

**Cara cek:** pasang ekstensi Chrome **Meta Pixel Helper**, buka website, dan lihat apakah event-nya muncul. Pixel baru jalan setelah `metaPixelId` terisi.

## Deploy dan domain

- Hosting: **GitHub Pages** (Settings -> Pages -> Deploy from a branch -> `main` / root).
- Setiap commit ke `main` otomatis terbit dalam 1-2 menit.
- Domain `backyard.id`: isi di Settings -> Pages -> **Custom domain**, lalu atur DNS di pengelola domain sesuai dokumentasi GitHub Pages. Setelah aktif, centang **Enforce HTTPS**.
- Selama belum pakai domain sendiri, ganti `canonical`, `og:image`, dan `twitter:image` di bagian `<head>` ke alamat `github.io` kalau mau tes preview share.

## Masalah umum

| Masalah | Penyebab dan solusi |
|---|---|
| Halaman putih atau konten hilang setelah edit | Biasanya kutip atau koma terhapus di CONFIG. Buka **History**, kembalikan ke versi sebelumnya |
| Perubahan belum kelihatan | Tunggu 2 menit, lalu refresh keras |
| Tombol WA tidak jalan atau salah nomor | Cek `whatsappNumber`: tanpa `+`, tanpa 0 di depan, diawali `62` |
| Tombol "Lihat Lokasi" tidak ada | `venueMapUrl` kosong |
| Foto tampil kotak putus-putus | File belum diupload, atau nama/path di CONFIG tidak sama dengan nama file (perhatikan huruf besar-kecil) |
| Event tidak muncul | `active` bernilai `false` |
| Link share tampil tanpa gambar | `og-image.jpg` belum ada, atau URL `og:image` di `<head>` belum sesuai domain |

## Hal yang perlu keputusan manajemen

- 5 FAQ tambahan (cara bayar, refund/pindah jadwal, hujan, batas usia, lokasi/parkir) masih draft sementara. Cari komentar `Sementara OK, masih dibahas di manajemen` di CONFIG untuk finalisasi.
- Klaim "lebih dari 80% peserta datang sendirian" divalidasi dari data event 1 dan 2. Cek ulang berkala supaya tetap benar.

## Rencana Fase 2

Admin dashboard (edit konten tanpa menyentuh kode) akan dibangun terpisah. Struktur `CONFIG` sengaja dibuat rapi supaya nanti tinggal disambungkan ke backend.
