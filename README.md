<div align="center">

# 🎬 CinemaXXV

### Sistem Reservasi Tiket Bioskop — Console App (C++)

![C++](https://img.shields.io/badge/C++-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-Windows%20Console-0078D6?style=for-the-badge&logo=windows&logoColor=white)
![Status](https://img.shields.io/badge/Status-Active-success?style=for-the-badge)
![Kelompok](https://img.shields.io/badge/Kelompok-20-orange?style=for-the-badge)

*Pesan tiket bioskop favoritmu langsung dari terminal — pilih film, pilih kursi, bayar lewat QRIS, cetak tiket. Semua dari console.*

</div>

---

## 📋 Daftar Isi

- [Tentang Proyek](#-tentang-proyek)
- [Fitur Utama](#-fitur-utama)
- [Alur Aplikasi](#-alur-aplikasi)
- [Batasan & Aturan Data](#-batasan--aturan-data)
- [Cara Menjalankan](#-cara-menjalankan)
- [Akun Default](#-akun-default)
- [Pratinjau Tampilan](#-pratinjau-tampilan)
- [Anggota Kelompok](#-anggota-kelompok)

---

## 🎯 Tentang Proyek

**CinemaXXV** adalah sistem reservasi tiket bioskop berbasis **C++ (console application)**. Aplikasi ini mensimulasikan proses bisnis bioskop secara end-to-end: admin mengelola film, jadwal, dan promo, sementara customer bisa memesan tiket, memilih kursi secara visual, membayar dengan QRIS dummy, hingga mencetak tiket dan melihat riwayat pemesanan.

> 💡 **Kenapa menarik?** Semua dikerjakan tanpa database eksternal — murni array & struct di memori, dengan validasi input yang cukup ketat (bentrok jadwal, kursi duplikat, kode promo, dll).

---

## ✨ Fitur Utama

<details>
<summary><b>🔐 Autentikasi (Sign Up / Sign In)</b></summary>
<br>

- Sign Up dengan validasi: username tidak boleh kosong, mengandung spasi, sama dengan `admin`, atau duplikat
- Sign In mendukung akun **admin tetap** maupun **customer terdaftar**
- Bisa membatalkan input kapan saja dengan mengetik `exit`

</details>

<details>
<summary><b>🛠️ Panel Admin</b></summary>
<br>

| Modul | Kemampuan |
|---|---|
| 🎞️ **Manajemen Film** | Tambah (ID auto-increment mulai `1001`), edit, hapus *(ditolak jika masih dipakai jadwal)*, lihat daftar diurutkan dari tiket terjual terbanyak |
| 🗓️ **Manajemen Jadwal** | Tambah (ID auto-increment mulai `2001`), edit, hapus *(ditolak jika sudah ada tiket terjual)*, dengan **validasi bentrok** studio + tanggal + jam |
| 🏷️ **Manajemen Promo** | Tambah kode promo unik, atur diskon 1–100%, aktif/nonaktifkan, hapus |
| 📊 **Laporan Penjualan** | Total tiket terjual, total transaksi, total pendapatan, daftar transaksi |

</details>

<details>
<summary><b>🎟️ Sisi Customer</b></summary>
<br>

- **Beranda** — lihat daftar film yang tersedia
- **Reservasi Tiket** — pilih jadwal, lihat layout kursi visual (5 baris × 8 kolom), pilih kursi format `A1`–`E8`, dengan validasi kursi terisi/duplikat
- **Pembayaran** — ringkasan pesanan → input kode promo (opsional) → tampilan QR dummy → konfirmasi → ID transaksi & kode tiket otomatis
- **Cetak Tiket** — tampilkan detail tiket dari transaksi terakhir
- **Riwayat Pemesanan** — semua transaksi milik user yang sedang login

</details>

---

## 🔄 Alur Aplikasi

```mermaid
flowchart TD
    A([Mulai]) --> B{LOGIN}
    B -->|Sign Up| C[Buat Akun Baru]
    B -->|Sign In| D{Validasi Akun}
    B -->|Exit| Z([Keluar])
    C --> B
    D -->|Admin| E[📊 Menu Admin]
    D -->|Customer| F[🎟️ Menu Customer]

    E --> E1[Manajemen Film]
    E --> E2[Manajemen Jadwal]
    E --> E3[Manajemen Promo]
    E --> E4[Laporan Penjualan]
    E --> B

    F --> F1[Beranda]
    F --> F2[Reservasi Tiket]
    F2 --> F2a[Pilih Jadwal & Kursi]
    F2a --> F3[Pembayaran QRIS]
    F3 --> F4[Cetak Tiket]
    F --> F5[Riwayat Pemesanan]
    F --> B
```

---

## 📐 Batasan & Aturan Data

| Aspek | Aturan |
|---|---|
| Maks. User | 30 |
| Maks. Film | 20 |
| Maks. Jadwal | 30 |
| Maks. Promo | 10 |
| Maks. Transaksi | 50 |
| Jumlah Studio | 3 |
| Kursi per Studio | 40 (5 baris `A–E` × 8 kolom) |
| ID Film | Auto increment, mulai `1001` |
| ID Jadwal | Auto increment, mulai `2001` |
| Durasi Film | 40–360 menit |
| Harga Tiket | Rp25.000 – Rp300.000 |
| Genre | Action / Horror / Comedy / Drama / Animasi |
| Rating Usia | SU / 13+ / 17+ / 21+ |
| Tanggal Tayang | Juni–Desember 2026 (Juni mulai tanggal 23) |
| Metode Bayar | QRIS (visual dummy, simulasi) |

---

## ⚙️ Cara Menjalankan

> ⚠️ Program ini menggunakan `<conio.h>` (`getch()`), sehingga **hanya berjalan di Windows** (atau via MinGW/CodeBlocks di Windows). Untuk tampilan warna ANSI, gunakan **Windows Terminal** atau cmd/PowerShell modern.

```bash
# Compile dengan g++ (MinGW)
g++ -o CinemaXXV main.cpp

# Jalankan
CinemaXXV.exe
```

Atau buka langsung di **Code::Blocks** / **Visual Studio** lalu *Build & Run*.

---

## 🔑 Akun Default

| Role | Username | Password |
|---|---|---|
| Admin | `admin` | `admin123` |

Akun customer dibuat sendiri melalui menu **Sign Up**.

> 🎬 Saat program pertama dijalankan, 2 film, 2 jadwal, dan 2 kode promo dummy (`DISKON10`, `DISKON20`) otomatis tersedia untuk uji coba.

---

## 🖥️ Pratinjau Tampilan

<details>
<summary><b>Lihat contoh layout kursi (klik untuk buka)</b></summary>
<br>

```
          [ LAYAR BIOSKOP ]

      1  2  3  4  5  6  7  8
============================================================
  A  [O][O][X][O][O][O][O][O]
  B  [O][O][O][O][X][O][O][O]
  C  [O][O][O][O][O][O][O][O]
  D  [O][X][O][O][O][O][O][O]
  E  [O][O][O][O][O][O][O][O]
============================================================
  Keterangan: [O] Tersedia   [X] Terisi
```

</details>

---

## 👥 Anggota Kelompok

| Nama | NIM |
|---|---|
| I Putu Reynanda Putra Dynatha | F1D02510115 |
| Lalu Reza Pramandika | F1D02510013 |
| Naira Almira | F1D02510085 |
| Silva Sazkia Damayanti | F1D02510026 |
| Alya Zulfadila | F1D02510102 |
| Putri Riyona Ibtisaamah | F1D02510131 |
| Yohanes Ibrani | F1D02510142 |

<div align="center">

---

Dibuat dengan ❤️ oleh **Kelompok 20** — CinemaXXV 🎬🍿

</div>
