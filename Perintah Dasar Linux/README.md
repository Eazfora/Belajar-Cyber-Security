# 🐧 Fundamental Linux untuk Ethical Hacking

Sebagai langkah awal belajar *ethical hacking*, Anda wajib menguasai **Linux Fundamental (Perintah Dasar Linux)**. Di dalam lingkungan Linux, hampir seluruh aktivitas peretasan akan berpusat pada eksekusi perintah melalui terminal.

Berikut adalah perintah-perintah dasar paling krusial yang wajib Anda kuasai dan praktikkan di terminal Kali Linux Anda.

---

## 📌 Daftar Isi
1. [Navigasi & Melihat Folder](#-1-navigasi--melihat-folder-mencari-jalan)
2. [Manajemen File & Folder](#-2-manajemen-file--folder-membuat--memanipulasi)
3. [Manajemen Sistem & Hak Akses](#-3-manajemen-sistem--hak-akses)
4. [Manipulasi Teks & Pencarian](#-4-manipulasi-teks--pencarian)
5. [Struktur Direktori Penting Linux](#-5-struktur-direktori-penting-linux)
6. [Menjalankan Skrip Eksploitasi (Python)](#-6-menjalankan-skrip-eksploitasi-python)
7. [🧠 Quiz Evaluasi Perintah Linux](#-quiz-evaluasi-perintah-linux)
8. [🚀 Tantangan Praktik Mandiri](#-tantangan-praktik-mandiri)

---

## 🗺️ 1. Navigasi & Melihat Folder (Mencari Jalan)

*   `pwd` **(Print Working Directory)**
    *   **Fungsi:** Menampilkan direktori atau folder kerja saat ini.
    *   **Contoh:** `pwd`
*   `ls` **(List)**
    *   **Fungsi:** Menampilkan daftar isi dari sebuah folder.
    *   **Contoh:** `ls` atau `ls -la` (menampilkan seluruh file tersembunyi beserta detail hak aksesnya).
*   `cd` **(Change Directory)**
    *   **Fungsi:** Berpindah direktori atau masuk ke folder lain.
    *   **Contoh:** `cd Ani` untuk masuk ke folder bernama Ani.
*   `cd ..`
    *   **Fungsi:** Kembali mundur satu tingkat ke folder sebelumnya.
    *   **Contoh:** `cd ..`

---

## 📁 2. Manajemen File & Folder (Membuat & Memanipulasi)

*   `mkdir [nama_folder]` **(Make Directory)**
    *   **Fungsi:** Membuat folder baru.
    *   **Contoh:** `mkdir proyek`
*   `rmdir [nama_folder]` **(Remove Directory)**
    *   **Fungsi:** Menghapus folder yang sudah kosong.
    *   **Contoh:** `rmdir proyek`
*   `touch [nama_file.txt]`
    *   **Fungsi:** Membuat file baru kosong.
    *   **Contoh:** `touch target.txt`
*   `rm [nama_file]` **(Remove)**
    *   **Fungsi:** Menghapus file.
    *   **Contoh:** `rm file.txt`
*   `cp [sumber] [tujuan]` **(Copy)**
    *   **Fungsi:** Menyalin file dari satu lokasi ke lokasi lain.
    *   **Contoh:** `cp file.txt /home/kali/berkas/`
*   `mv [sumber] [tujuan]` **(Move)**
    *   **Fungsi:** Memindahkan file atau mengubah nama file (rename).
    *   **Contoh:** `mv file.txt data.txt` (mengubah nama file).

---

## 👑 3. Manajemen Sistem & Hak Akses

*   `sudo [perintah]` **(SuperUser Do)**
    *   **Fungsi:** Menjalankan perintah sebagai administrator (*root*).
    *   **Contoh:** `sudo apt update`
*   `apt update`
    *   **Fungsi:** Memperbarui daftar paket/repositori aplikasi sistem.
    *   **Contoh:** `sudo apt update`
*   `apt upgrade`
    *   **Fungsi:** Memperbarui seluruh paket/aplikasi sistem yang terinstal ke versi terbaru.
    *   **Contoh:** `sudo apt upgrade -y`
*   `clear`
    *   **Fungsi:** Membersihkan seluruh tampilan layar terminal.
    *   **Contoh:** `clear`
*   `whoami`
    *   **Fungsi:** Menampilkan nama pengguna (*user*) yang sedang aktif digunakan saat ini.

---

## 📝 4. Manipulasi Teks & Pencarian

*   `cat [nama_file]` **(Concatenate)**
    *   **Fungsi:** Menampilkan seluruh isi dari sebuah file teks ke layar.
    *   **Contoh:** `cat info.txt`
*   `nano [nama_file]`
    *   **Fungsi:** Membuka teks editor berbasis terminal untuk mengedit atau membuat file berkas teks.
    *   **Contoh:** `nano catatan.txt`
*   `echo "[teks]"`
    *   **Fungsi:** Mencetak teks ke layar terminal atau mengarahkannya ke dalam file berkas.
    *   **Contoh:** `echo "IP Target: 192.168.1.1" > target.txt`
*   `grep "[kata_kunci]"`
    *   **Fungsi:** Menyaring data teks dan mencari kata kunci tertentu secara spesifik.
    *   **Contoh:** `cat target.txt | grep "IP"`

---

## 📂 5. Struktur Direktori Penting Linux

Penting bagi seorang *ethical hacker* untuk memahami tempat disimpannya file-file sistem di Linux:

| Direktori | Fungsi Utama | Contoh Isi / Berkas |
| :--- | :--- | :--- |
| `/` | **Root** direktori (akar utama sistem). Tempat awal dari semua folder. | Semua folder sistem berada di bawah direktori ini. |
| `/home` | Folder pengguna (*user* biasa). | `/home/kali`, `/home/admin` |
| `/root` | Folder utama khusus untuk pengguna administrator tertinggi (*Root*). | Berkas konfigurasi pribadi milik user *root*. |
| `/etc` | Tempat menyimpan seluruh file konfigurasi sistem dan aplikasi. | `/etc/hosts`, `/etc/passwd` |
| `/bin` | Berisi perintah dasar dan aplikasi utama sistem (*binaries*). | File eksekusi untuk perintah `ls`, `cp`, `mv`, `rm` |

---

## 🐍 6. Menjalankan Skrip Eksploitasi (Python)

Hampir 80% *tools* peretasan dan skrip eksploitasi (*exploit scripts*) di internet ditulis menggunakan bahasa Python. 
*   **Mengecek versi Python:**
    ```bash
    python3 --version
    ```
*   **Menjalankan skrip Python:**
    Jika Anda memiliki *tools* bernama `scanner.py`, eksekusi dengan:
    ```bash
    python3 scanner.py
    ```

---

## 🧠 Quiz Evaluasi Perintah Linux

Jawablah pertanyaan-pertanyaan berikut untuk menguji pemahaman teori Anda. *(Kunci jawaban ada di bagian paling bawah dokumen)*.

### Pertanyaan 1
Jika Anda sedang tersesat di dalam tumpukan folder terminal dan ingin tahu jalur absolut lokasi folder tempat Anda berada sekarang, perintah apa yang harus digunakan?
*   A. `ls`
*   B. `pwd`
*   C. `whoami`
*   D. `cd ..`

### Pertanyaan 2
Anda mengunduh sebuah skrip *exploit* bernama `attack.py` dari internet. Perintah manakah yang tepat untuk mengeksekusi skrip tersebut di dalam terminal Kali Linux?
*   A. `nano attack.py`
*   B. `cat attack.py`
*   C. `python3 attack.py`
*   D. `sudo apt upgrade attack.py`

### Pertanyaan 3
Folder manakah di dalam struktur direktori Linux yang digunakan khusus untuk menyimpan berkas-berkas konfigurasi sistem seperti berkas `hosts` atau daftar kata sandi?
*   A. `/home`
*   B. `/bin`
*   C. `/root`
*   D. `/etc`

### Pertanyaan 4
Anda ingin mengubah nama sebuah file hasil rekaman pemindaian dari nama `hasil_scan.txt` menjadi `report_final.txt`. Perintah manakah yang benar?
*   A. `cp hasil_scan.txt report_final.txt`
*   B. `mv hasil_scan.txt report_final.txt`
*   C. `mkdir hasil_scan.txt report_final.txt`
*   D. `rm hasil_scan.txt report_final.txt`

---

## 🚀 Tantangan Praktik Mandiri

Nyalakan terminal Kali Linux Anda di VirtualBox, lalu selesaikan 2 skenario tugas praktik di bawah ini tanpa menggunakan GUI (murni menggunakan terminal):

### 🎯 Tugas 1: Skenario Pengumpulan Informasi (Reconnaissance)
1. Periksa nama *user* aktif Anda saat ini untuk memastikan hak akses Anda menggunakan perintah yang sesuai.
2. Buatlah sebuah folder baru bernama `cyber_lab`.
3. Masuklah ke dalam folder `cyber_lab` tersebut.
4. Buatlah sebuah file teks baru kosong bernama `subdomain.txt`.
5. Isilah file `subdomain.txt` tersebut dengan teks `"://target.com"` menggunakan perintah pengarah teks (`echo`).
6. Tampilkan isi file teks tersebut ke layar terminal untuk memastikan teks berhasil tersimpan.

### 🎯 Tugas 2: Skenario Pembersihan Jejak (Log Clearing)
1. Salin (*copy*) file `subdomain.txt` ke dalam folder yang sama dengan nama baru yaitu `backup_subdomain.txt`.
2. Hapus file asli yang bernama `subdomain.txt`.
3. Mundur satu tingkat keluar dari folder `cyber_lab`.
4. Bersihkan seluruh tampilan layar terminal Anda hingga kosong dan bersih kembali menggunakan perintah yang tepat.

---
<details>
<summary>🔑 <b>Klik di sini untuk melihat Kunci Jawaban Quiz</b></summary>

1. **B. pwd** (Print Working Directory menampilkan lokasi folder aktif saat ini).
2. **C. python3 attack.py** (Eksekusi skrip python menggunakan interpreter python3).
3. **D. /etc** (Direktori khusus yang menampung file-file konfigurasi sistem).
4. **B. mv hasil_scan.txt report_final.txt** (Perintah `mv` selain memindahkan juga berfungsi untuk mengubah nama berkas).
</details>
