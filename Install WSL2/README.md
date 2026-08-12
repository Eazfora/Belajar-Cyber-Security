# 🐉 Panduan Migrasi dan Instalasi Kali Linux di WSL2 ( Windows 10/11 )

> ⚠️ **DISCLAIMER:** Jangan menggunakan WSL2 untuk keperluan eksploitasi yang tidak sah. Panduan ini dibuat murni untuk tujuan edukasi dan *Ethical Hacking*.

Mengunduh Kali Linux melalui Microsoft Store terkadang sering mengalami kegagalan atau *error*. Berdasarkan pengalaman, cara yang paling andal dan efektif adalah melakukan instalasi langsung melalui Command Prompt atau PowerShell.

---

## 📑 Daftar Isi
- [1. Proses Instalasi Utama](#1-proses-instalasi-utama)
- [2. Setup Akun Pengguna](#2-setup-akun-pengguna)
- [3. Instalasi Tools Hacking](#3-instalasi-tools-hacking)
- [4. Menjalankan Mode Grafis (GUI)](#4-menjalankan-mode-grafis-gui)
- [5. WSL2 vs VirtualBox](#5-wsl2-vs-virtualbox)

---

## 1. Proses Instalasi Utama

Langkah pertama adalah menginstal *environment* Kali Linux ke dalam Windows Anda menggunakan PowerShell.

1. Buka **Start Menu** Windows.
2. Ketik **PowerShell**, klik kanan pada aplikasinya, lalu pilih **Run as Administrator**.
3. Jalankan perintah berikut:

```bash
wsl --install -d kali-linux
```

---

## 2. Setup Akun Pengguna

Setelah proses unduhan pada PowerShell selesai, sebuah jendela terminal (layar hitam) akan terbuka secara otomatis untuk proses konfigurasi awal.

1. **Buat Username:** Masukkan *username* pilihan Anda (gunakan huruf kecil semua, contoh: `hacker`), lalu tekan `Enter`.
2. **Buat Password:** Masukkan *password* yang Anda inginkan, lalu tekan `Enter`.

> 💡 **Catatan:** Saat Anda mengetik *password*, layar tidak akan menampilkan karakter apa pun demi alasan keamanan. Tetap ketik *password* Anda seperti biasa, lalu tekan `Enter`.

---

## 3. Instalasi Tools Hacking

Secara *default*, Kali Linux di WSL2 hadir dalam versi *barebone* (kosong tanpa *tools*). Anda perlu menginstal *tools* sesuai kebutuhan. Pilih salah satu paket di bawah ini:

### 📦 Opsi A: Paket Default (Rekomendasi)
Menginstal ribuan *tools hacking* standar bawaan Kali Linux.
```bash
sudo apt update && sudo apt install -y kali-linux-default
```

### 🪶 Opsi B: Paket Ringan (Top 10 Tools)
Lebih hemat ruang (hanya ratusan MB) namun sudah mencakup *tools* esensial dan legendaris seperti **Nmap, Wireshark, Metasploit, John the Ripper, dan Hydra**.
```bash
sudo apt update && sudo apt install -y kali-linux-top10
```

---

## 4. Menjalankan Mode Grafis (GUI)

Jika tutorial atau pekerjaan Anda membutuhkan aplikasi antarmuka grafis (seperti Burp Suite, Wireshark, atau Maltego), WSL2 dilengkapi dengan fitur integrasi GUI bernama **Win-KeX**.

**1. Install Win-KeX:**
```bash
sudo apt install -y kali-win-kex
```

**2. Jalankan Mode GUI:**
Perintah ini akan membuat *desktop* Kali Linux menyatu dengan Windows Anda:
```bash
kex --esm --sound
```
*(Jika perintah di atas mengalami error, gunakan alternatif: `kex --win --sound`)*

**3. Menghentikan Sesi:**
Untuk mematikan sesi Win-KeX yang menggantung (*hanging*):
```bash
kex --stop
```

---

## ⚖️ WSL2 vs VirtualBox: Kapan Harus Pindah?

Untuk tahap awal belajar *ethical hacking* (seperti *Linux fundamental, information gathering, web pentesting*, hingga eksplorasi *database*), **WSL2 jauh lebih ringan, cepat, dan nyaman digunakan.**

Namun, WSL2 memiliki keterbatasan fisik yaitu **berbagi Network Card dengan Windows**. 

**🚨 Kapan Anda wajib beralih ke VirtualBox?**
Anda harus menggunakan VirtualBox (atau *booting* langsung) jika materi belajar Anda sudah masuk ke ranah **Wireless Hacking (Bobol Wi-Fi)**. Materi ini membutuhkan kontrol penuh atas perangkat keras tambahan (seperti USB Wi-Fi Adapter eksternal) untuk mengubah jaringan ke *Monitor Mode*.
