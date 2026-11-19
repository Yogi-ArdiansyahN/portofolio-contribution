# Portfolio Contribution Update

File instruksi Markdown untuk membuat atau memperbarui entri portfolio dari riwayat git repository aktif. File ini bukan script, tidak punya dependency, dan tidak butuh konfigurasi khusus.

Asisten AI apa pun bisa memakainya selama bisa membaca instruksi, menjalankan git, dan menulis file.

## Kapan dipakai

Minta asisten AI memperbarui kontribusi proyek saat Anda ingin:

- memindai commit git dari repo aktif
- membuat draft entri portfolio baru
- memperbarui entri portfolio yang sudah ada
- menghasilkan ringkasan kontribusi bilingual dari commit

File instruksi akan menanyakan target folder, author, rentang tanggal, slug tujuan, dan istilah privat yang harus dihindari. Draft ditampilkan lebih dulu. File hanya ditulis setelah konfirmasi.

## Menyiapkan skill

Unduh file instruksi:

```bash
curl -fsSL https://raw.githubusercontent.com/Yogi-ArdiansyahN/portofolio-contribution/main/catalog/portfolio-contribution-update/portfolio-contribution-update.md -o portfolio-contribution-update.md
```

Simpan file di tempat yang bisa dibaca asisten Anda, atau tempel isinya ke instruksi proyek atau chat. Nama dan lokasi file mengikuti cara kerja asisten yang Anda pakai. Tidak ada alat tambahan atau langkah khusus.

## Katalog

`catalog/index.json` berisi daftar file instruksi dan versinya. Naikkan `version` setiap kali file instruksi berubah supaya pembaruan terdeteksi.

## Struktur katalog

```text
catalog/
├── index.json
└── portfolio-contribution-update/
    └── portfolio-contribution-update.md
```

## Pemakaian

Contoh permintaan:

```text
Update kontribusi proyek dari repo aktif dengan mengikuti file instruksi portfolio-contribution-update.
```

Asisten akan memandu input, memindai git, menyusun draft, dan menunggu konfirmasi sebelum menulis file.

## Lisensi

MIT. Lihat `LICENSE`.
