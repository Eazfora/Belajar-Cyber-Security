# 🕵️‍♂️ Pengintaian Pasif dalam Pengujian Penetrasi (Passive Reconnaissance)

Pengintaian pasif bukan hanya langkah pertama dalam pengujian penetrasi, tetapi fondasi dari setiap serangan di dunia nyata. Dengan mengumpulkan intelijen OSINT (*Open-Source Intelligence*) secara diam-diam, Anda dapat memetakan titik lemah suatu organisasi tanpa pernah menyentuh sistem mereka secara langsung.

---

## 📑 Daftar Isi
1. [Alat Pengintaian Pasif Utama](#-alat-pengintaian-pasif-utama)
2. [Teknik OSINT Lanjutan (Di Luar Alat Khusus)](#-teknik-osint-lanjutan-di-luar-alat-khusus)
3. [Contoh Alur Kerja: Dari WHOIS ke Subdomain](#-contoh-alur-kerja-dari-whois-ke-pemetaan-subdomain)
4. [Studi Kasus Singkat](#-studi-kasus-singkat)
5. [Mengapa Pengintaian Pasif Penting?](#-mengapa-pengintaian-pasif-sangat-penting-bagi-pentester)
6. [Tips Profesional](#-tips-profesional-dari-lapangan)

---

## 🛠️ Alat Pengintaian Pasif Utama

Berikut adalah perangkat penting yang dibutuhkan oleh setiap *pentester*, digabungkan dengan detail fungsi dan cara penggunaannya:

### 1. `whois` — Kecerdasan Domain
* **Fungsi:** Mengumpulkan informasi pendaftaran dan kepemilikan domain (OSINT pasif) dengan menampilkan detail registrar, tanggal pembuatan/kedaluwarsa domain, serta informasi kontak pemilik jika tidak disembunyikan. Dapat memberikan petunjuk mengenai hubungan infrastruktur antar-domain.
* **Cara Penggunaan:** Buka terminal dan ketikkan perintah beserta nama domain target tanpa protokol (`http`/`https`).
* **Contoh:** `whois target.com`. Berpotensi mengungkap informasi kontak (seperti `admin@target.com`) yang berguna untuk *spear phishing* atau *credential stuffing*.

### 2. `dig` & `dnsrecon` — Enumerasi DNS
**`dig` (Domain Information Groper)**
* **Fungsi:** Melakukan kueri ke server DNS untuk mengumpulkan *records* suatu domain (A, MX, TXT, CNAME, NS) guna memetakan infrastruktur server target.
* **Cara Penggunaan:** Ketik `dig` diikuti nama domain, dan tambahkan parameter tipe *record* untuk pencarian spesifik.
* **Contoh:** `dig target.com MX` (mencari server email). Ini dapat mengungkap alamat seperti `mail.target.com`.

**`dnsrecon`**
* **Fungsi:** Alat enumerasi DNS tingkat lanjut berbasis Python untuk memetakan infrastruktur jaringan, menguji celah *Zone Transfer* (AXFR), melakukan *brute-force* subdomain, dan mengekstrak catatan SRV.
* **Cara Penggunaan:** Gunakan argumen `-d` untuk menentukan domain target.
* **Contoh:** `dnsrecon -d target.com -D subdomains.txt -t brt` (untuk *brute-force* subdomain menggunakan *wordlist*).

### 3. `theHarvester` — Penambangan Data OSINT
* **Fungsi:** Alat OSINT otomatis untuk mengekstrak alamat email, nama karyawan, subdomain, IP, dan URL dari berbagai sumber publik seperti mesin pencari, LinkedIn, dan *database* publik.
* **Cara Penggunaan:** Tentukan domain target dengan bendera `-d` dan sumber data dengan bendera `-b`.
* **Contoh:** `theHarvester -d target.com -l 500 -b all`. Kueri ini berpotensi mengungkap titik masuk seperti `vpn.target.com`.

### 4. Shodan — "Google untuk Peretas"
* **Fungsi:** Mesin pencari khusus perangkat yang terhubung ke internet (server, router, CCTV, IoT, SCADA) yang digunakan untuk *banner grabbing*, mendeteksi port terbuka, OS, dan kerentanan (CVE) pada IP publik.
* **Cara Penggunaan:** Digunakan via situs web `shodan.io` dengan sintaks pencarian spesifik atau melalui CLI terminal.
* **Contoh:** Melalui CLI `shodan search "port:22"`, atau via web `ssl:"target.com"`. Hal ini berpotensi mengungkap server pengembang dengan kredensial *default*.

### 5. `crt.sh` — Log Transparansi Sertifikat
* **Fungsi:** Antarmuka web untuk mencari log *Certificate Transparency* (CT), bertindak sebagai metode enumerasi pasif akurat untuk menemukan subdomain sah milik perusahaan berdasarkan sertifikat SSL/TLS mereka.
* **Cara Penggunaan:** Kunjungi [https://crt.sh](https://crt.sh) dan masukkan *wildcard* sebelum nama domain.
* **Contoh:** Pencarian `%.target.com` dapat mengungkapkan subdomain berharga seperti `dev.target.com`, `vpn.target.com`, dan `staging.target.com`.

---

## 🌐 Teknik OSINT Lanjutan (Di Luar Alat Khusus)

### Google Dorking
Teknik ini memanfaatkan operator pencarian tingkat lanjut pada Google untuk memetakan permukaan serangan (file/direktori terekspos) tanpa berinteraksi langsung dengan sistem target.
* **`site:`** Membatasi pencarian pada satu domain/sub-domain tertentu (contoh: `site:target.com`).
* **`filetype:`** Memfilter pencarian berdasarkan ekstensi file, seperti PDF atau DOCX (contoh: `filetype:pdf`).
* **`inurl:`** Mencari kata spesifik di dalam struktur URL (contoh: `inurl:login`).
* **`intitle:`** Menampilkan halaman yang memiliki kata tertentu pada judul (contoh: `intitle:"dashboard"`).
* **`" "` (Kutip Ganda):** Memaksa pencarian frasa presisi.
> **Contoh Kombinasi:** `site:target.com filetype:pdf confidential` atau pencarian repositori GitHub `site:github.com "target.com"`.

### Teknik Tambahan
* **Internet Archive (Wayback Machine):** Menggunakan `archive.org/web/` untuk menemukan *endpoint* API lama atau dokumen sensitif pada versi lampau situs web target.
* **Analisis Repositori Kode Publik:** Mencari *source code* organisasi di GitHub/GitLab untuk menemukan *API key* atau kata sandi basis data yang tidak sengaja *hardcoded*.
* **Analisis Media Sosial:** Menganalisis profil karyawan di LinkedIn/X untuk memetakan hierarki perusahaan (target *phishing*) dan spesifikasi infrastruktur teknologi dari sertifikasi mereka.
* **Ekstraksi Metadata Dokumen:** Menggunakan alat seperti ExifTool pada dokumen publik target untuk mengungkap *username* lokal, jalur *folder*, atau versi *software* pembuat dokumen.
* **Pencarian ASN (Autonomous System Number):** Memetakan seluruh rentang alamat IP (*netblock*) perusahaan via situs seperti BGP Toolkit untuk memperluas area pemindaian secara sah.

---

## 🧩 Contoh Alur Kerja: Dari WHOIS ke Pemetaan Subdomain

Berikut adalah simulasi alur kerja pengintaian pasif yang umum dan efektif:
1. **Pencarian WHOIS** → Ekstrak informasi registrar & email kontak.
   * *Ditemukan:* `it-admin@target.com`.
2. **theHarvester** → Cari email dan subdomain yang terhubung.
   * *Ditemukan:* `vpn.target.com`.
3. **crt.sh** → Temukan subdomain yang terdaftar SSL.
   * *Ditemukan:* `staging.target.com`.
4. **Shodan** → Cari layanan terekspos yang terkait dengan IP.
   * *Ditemukan:* Akses *Open RDP* di `dev.target.com`.

> **Hasil:** Anda kini memiliki 3 titik serangan potensial tanpa perlu mengirimkan satu paket pun langsung ke server target.

---

## 🎯 Studi Kasus Singkat

Dalam sebuah keterlibatan *Red Team*, kami memulai serangan hanya bermodalkan nama domain:
* **WHOIS** mengungkapkan pola penamaan email perusahaan (`firstname.lastname@target.com`).
* **LinkedIn** memberi kami daftar profil karyawan yang valid.
* **theHarvester** dan **crt.sh** berhasil mengungkap alamat `vpn.target.com`.
* **Shodan** menunjukkan bahwa VPN tersebut menggunakan versi OpenVPN dan SSL yang sudah sangat usang.

Hal ini membuka jalur eksploitasi via serangan *credential stuffing* pada login VPN, yang akhirnya menghasilkan peretasan jaringan internal secara menyeluruh.

---

## 🔑 Mengapa Pengintaian Pasif Sangat Penting bagi Pentester?

* **Stealth (Tersembunyi):** IDS/IPS di pihak target tidak akan mendeteksi pengumpulan informasi OSINT.
* **Nilai Intelijen:** Membantu memprioritaskan jalur serangan paling rentan.
* **Efisiensi:** Menghemat waktu secara drastis dengan mengeliminasi metode coba-coba yang buta.
* **Realisme:** Secara akurat mensimulasikan bagaimana penyerang tingkat lanjut benar-benar beroperasi di dunia nyata.

Tanpa pengintaian yang tepat, upaya eksploitasi sering kali hanya menjadi tembakan di ruang gelap.

---

## 💡 Tips Profesional dari Lapangan

* **Selalu periksa pencarian ASN** untuk memetakan seluruh rentang alamat IP (*netblock*) yang dimiliki oleh organisasi target.
* **Gunakan alat DNS historis** (seperti SecurityTrails) untuk mengidentifikasi subdomain lama yang catatan DNS-nya sudah tidak aktif tetapi servernya masih menyala.
* **Pantau Pastebin & forum kebocoran data** karena kredensial karyawan sering beredar di sana jauh sebelum pengumuman kebocoran data resmi dipublikasikan.
* **Baca papan lowongan pekerjaan** target; persyaratan kualifikasi sering kali membocorkan detail susunan teknologi internal (contoh: *"Kami merekrut AWS DevOps dengan pengalaman Kubernetes"*).
* **Otomatiskan Alur Kerja** menggunakan *framework* besar seperti `Amass` dan `Recon-ng` demi kecepatan dan cakupan data.

## 📚 Sumber Referensi

* **Medium:** [Pengintaian Pasif dalam Pengujian Penetrasi](https://medium.com/@vivekbhatt2002/%EF%B8%8F-%EF%B8%8F-passive-reconnaissance-in-penetration-testing-the-art-of-staying-unseen-part-1-b5b7ee706f24)