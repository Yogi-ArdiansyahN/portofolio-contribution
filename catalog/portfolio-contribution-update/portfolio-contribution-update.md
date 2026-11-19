---
name: portfolio-contribution-update
description: Update portfolio project contribution entries from the active git repository. Use when the user asks to scan git history, refresh project contributions, regenerate a portfolio entry, or update portfolio markdown from commits. Asks for target folder, author, date range, slug, and private terms, then drafts before writing.
---

# Portfolio Contribution Update

Buat atau perbarui satu entri portfolio dari riwayat git repo aktif. File instruksi ini hanya prosedur, bukan script. Gunakan kemampuan baca, eksekusi git, dan tulis yang tersedia pada asisten Anda, lalu tulis file hanya setelah konfirmasi.

## Input wajib

Tanya semua hal ini dalam satu pesan singkat. Jangan menebak.

- target folder portfolio, misalnya `portfolio/`
- author atau email untuk filter git
- tanggal mulai dan tanggal akhir
- slug file tujuan, dan apakah akan menimpa file yang ada
- istilah privat yang harus dihindari, misalnya nama klien, host internal, atau produk internal

Jika target folder tidak disebut, cek apakah `portfolio/` ada. Jika ada, usulkan folder itu dan tetap minta konfirmasi.

## Pemeriksaan awal

1. Jalankan `git rev-parse --show-toplevel`. Jika bukan repo git, berhenti dengan pesan yang jelas.
2. Baca isi target folder. Cari file markdown existing yang bisa dipakai sebagai contoh format.
3. Jika slug tujuan sudah ada, baca file lama dan siapkan diff.
4. Jika tidak ada file contoh, pakai format fallback di bawah ini, lalu minta konfirmasi sebelum melanjutkan.
5. Deteksi struktur dari file existing: frontmatter keys, heading, jumlah bullet, dan pola bahasa. Jangan mengubah struktur project tanpa konfirmasi.

## Scan git

Gunakan pola ini, isi placeholder dari jawaban user:

```bash
git log --no-merges --date=short --pretty=format:"%H%x1f%ad%x1f%an <%ae>%x1f%s" --since="TANGGAL_MULAI" --until="TANGGAL_AKHIR" --author="AUTHOR"
```

Jika tidak ada commit, laporkan dan jangan menulis file.

## Filter commit

- ambil hanya subject yang cocok dengan `^(feat|fix|refactor)(\([^)]+\))?(!)?:`
- buang chore, docs, test, merge, dan noise lain
- deduplikasi subject yang sama, simpan tanggal terbaru
- ambil scope dari tanda kurung pada subject atau dari trailer `scope:`
- jika semua scope kosong, minta user menentukan scope atau usulkan `general`
- jangan mengarang perubahan yang tidak ada di commit

## Tech stack

Deteksi kandidat tech stack dari file yang benar-benar ada di repo:

- `package.json`
- `composer.json`
- `requirements.txt`
- `go.mod`
- `pom.xml`
- `README*`

Jangan menambahkan teknologi yang tidak muncul di sumber tersebut.

## Format fallback

Pakai format ini hanya jika target folder belum punya contoh. Tetap minta konfirmasi sebelum menulis.

```text
---
title: "Generic system name"
title_id: "Nama sistem generik"
role: "Role"
scope: "Responsibility in English"
scope_id: "Tanggung jawab dalam bahasa Indonesia"
experience: "Company or engagement"
tech_stack: ["Technology"]
---

## Business Context
One short paragraph in English.

## Role & System Flow
* First contribution.
* Second contribution.
* Third contribution.

## Technical Notes
One short paragraph in English.

## Konteks Bisnis
Satu paragraf pendek dalam bahasa Indonesia.

## Peran & Alur Sistem
* Kontribusi pertama.
* Kontribusi kedua.
* Kontribusi ketiga.

## Highlight Teknis
Satu paragraf pendek dalam bahasa Indonesia.
```

## Validasi isi

Sebelum menampilkan draft, pastikan tidak ada:

- em dash, URL, email, `TODO`, `.env`, atau `/Users/`
- host internal atau alamat IP
- nama klien, produk internal, atau istilah privat yang diberikan user
- teknologi yang tidak ditemukan di repo

Gunakan nama sistem generik. Fokus pada fungsi sistem, alur kerja, dan teknologi.

## Draft dan konfirmasi

1. Tampilkan draft lengkap di chat.
2. Jika file tujuan sudah ada, tampilkan diff terhadap file lama.
3. Tanya konfirmasi eksplisit sebelum menulis.
4. Setelah user menyetujui, tulis file markdown di target folder.
5. Jalankan `npm run check && npm run build` jika script tersebut ada.
6. Laporkan hasilnya. Jangan commit.

## Aturan keras

- Jangan menulis file sebelum konfirmasi.
- Jangan menebak author, tanggal, slug, atau format.
- Jangan menambah dependency, command, atau script baru.
- Jangan mengubah file lain tanpa diminta.
- Jangan mengubah deskripsi proyek lama kecuali user menyetujui diff.
