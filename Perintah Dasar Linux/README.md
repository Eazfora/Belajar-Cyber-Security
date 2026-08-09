# 🐧 Fundamental Linux untuk Ethical Hacking

Sebagai langkah awal belajar *ethical hacking*, Anda wajib menguasai **Linux Fundamental (Perintah Dasar Linux)**. Di dalam lingkungan Linux, hampir seluruh aktivitas peretasan akan berpusat pada eksekusi perintah melalui terminal.

Berikut adalah perintah-perintah dasar paling krusial yang wajib Anda kuasai dan praktikkan di terminal Kali Linux Anda.

---

## 🗺️ 1. Navigasi & Melihat Folder (Mencari Jalan)

*   `pwd` **(Print Working Directory)**
    *   **Fungsi:** Mengetahui jalur absolut dari posisi folder/direktori tempat Anda berada saat ini.
*   `ls` **(List)**
    *   **Fungsi:** Menampilkan daftar file dan folder di lokasi saat ini.
    *   💡 **Tips:** Gunakan `ls -la` untuk menampilkan seluruh file (termasuk yang disembunyikan/ *hidden files*) beserta detail izin aksesnya (*permissions*).
*   `cd [nama_folder]` **(Change Directory)**
    *   **Fungsi:** Berpindah atau masuk ke dalam direktori lain.
    *   **Contoh:** `cd Documents` untuk masuk ke folder Documents, atau `cd ..` untuk mundur satu tingkat ke direktori sebelumnya.

---

## 📁 2. Manajemen File & Folder (Membuat & Memanipulasi)

*   `mkdir [nama_folder]` **(Make Directory)**
    *   **Fungsi:** Membuat folder baru (misalnya untuk menyimpan *tools* atau hasil *scanning*).
*   `touch [nama_file.txt]`
    *   **Fungsi:** Membuat file teks kosong baru (contoh: untuk mencatat IP target).
*   `cat [nama_file.txt]`
    *   **Fungsi:** Membaca dan mencetak seluruh isi dari sebuah file teks langsung ke layar terminal.
*   `rm [nama_file]` **(Remove)**
    *   **Fungsi:** Menghapus sebuah file. 
    *   ⚠️ **Peringatan:** Gunakan `rm -rf [nama_folder]` untuk menghapus sebuah folder beserta seluruh isinya secara permanen.

---

## 👑 3. Kekuasaan Tertinggi (Hak Akses)

*   `sudo [perintah]` **(SuperUser Do)**
    *   **Fungsi:** Menjalankan perintah dengan hak akses tertinggi sebagai Administrator (*Root*). Sistem akan meminta otentikasi *password* Kali Linux Anda.
*   `whoami`
    *   **Fungsi:** Menampilkan status *user* Anda saat ini (untuk memastikan apakah Anda login sebagai *user* biasa atau *root*).

---

## 📝 4. Manipulasi Teks & Pencarian

### `echo` (Menampilkan & Menulis Teks)
Berfungsi untuk mencetak teks ke layar terminal, atau mengarahkan teks ke dalam sebuah file secara instan.
*   **Mencetak ke layar:**
    ```bash
    echo "Saya sedang belajar hacking"
    ```
*   **Menulis ke dalam file (Mengganti/Menimpa isi):**
    Menggunakan tanda `>` akan membuat file baru atau menimpa isi file jika sudah ada.
    ```bash
    echo "IP Target: 192.168.1.1" > target.txt
    ```
*   **Menambah baris baru (Append):**
    Menggunakan tanda `>>` akan menambahkan teks di baris paling bawah tanpa menghapus isi sebelumnya.
    ```bash
    echo "Port Terbuka: 80, 443" >> target.txt
    ```

### `nano` (Editor Teks Terminal)
Editor teks bawaan Linux yang beroperasi langsung di dalam terminal (mirip Notepad). Sangat berguna untuk mengedit *script* atau menulis catatan panjang.
*   **Cara membuka/membuat file:**
    ```bash
    nano target.txt
    ```
*   **Cara menyimpan dan keluar:** 
    Setelah selesai mengetik, tekan `Ctrl + O` lalu `Enter` (untuk Save), kemudian tekan `Ctrl + X` (untuk Exit).

### `grep` (Penyaring & Pencari Kata)
Sangat berguna untuk menyaring ribuan baris data hasil *scanning* dan hanya menampilkan baris yang mengandung kata kunci spesifik.
*   **Contoh:** Mencari kata "Port" dari sebuah file teks menggunakan kombinasi *pipe* (`|`).
    ```bash
    cat target.txt | grep "Port"
    ```

---

## 🐍 5. Menjalankan Skrip Eksploitasi (Python)

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

## 🚀 Tantangan Praktik

### Misi 1: Membuat Lab Kecil
Coba jalankan urutan perintah ini satu per satu di terminal Anda:
```bash
pwd
mkdir belajar_hacking
cd belajar_hacking
touch target.txt
ls

### Misi 2: Satukan Semua Kekuatan! 🔥
Ketik urutan perintah gabungan ini untuk melihat bagaimana manipulasi teks dan pencarian bekerja secara berdampingan:
```bash
echo "Target 1: Linux" > lab.txt
echo "Target 2: Windows" >> lab.txt
cat lab.txt | grep "Windows"