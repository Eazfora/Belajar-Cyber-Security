# 🕵️‍♂️ Pengumpulan Informasi: Pasif vs Aktif dalam Pengujian Penetrasi

Setiap pengujian penetrasi (*penetration testing*) selalu dimulai dengan satu pertanyaan krusial: **"Apa yang kita ketahui tentang target?"** 

Jawabannya terletak pada **pengumpulan informasi** (*information gathering*), sebuah langkah mendasar yang menentukan seberapa efektif keseluruhan upaya pengujian Anda. Pengumpulan informasi tidak hanya sekadar label teknis; ia mendefinisikan seberapa banyak informasi yang Anda ungkapkan, seberapa dalam wawasan Anda, dan seberapa besar risiko yang Anda tanggung.

Repositori ini membahas perbedaan esensial antara pengumpulan informasi pasif dan aktif, apa saja yang perlu dikumpulkan, serta mengapa keduanya wajib dikuasai oleh seorang *Ethical Hacker*.

---

## 📌 Daftar Isi

1. [Apa itu Pengumpulan Informasi?](#-apa-itu-pengumpulan-informasi)
2. [Pengumpulan Informasi Pasif](#-pengumpulan-informasi-pasif)
3. [Pengumpulan Informasi Aktif](#-pengumpulan-informasi-aktif)
4. [Perbandingan: Pasif vs Aktif](#-pasif-vs-aktif-perbedaan-sebenarnya)
5. [Mengapa Keduanya Penting?](#-mengapa-keduanya-pendekatan-itu-penting)
6. [Contoh di Dunia Nyata](#-contoh-di-dunia-nyata)
7. [Risiko dan Batasan Etika](#-risiko-dan-batasan-etika)
8. [Kesimpulan & Poin Penting](#-kesimpulan--poin-penting)

---

## 📖 Apa itu Pengumpulan Informasi?

Pengumpulan informasi adalah proses mengumpulkan data tentang sistem, aplikasi, atau organisasi target **sebelum** mencoba mengeksploitasinya.

Langkah ini memiliki **dua tujuan penting**:
1. **Memetakan permukaan serangan** – Mengidentifikasi semua kemungkinan titik masuk (*entry points*).
2. **Membangun konteks** – Memahami teknologi, infrastruktur, dan orang-orang di balik sistem tersebut.

> 💡 **Analogi:** Anggap saja ini sebagai pengintaian dalam strategi militer. Semakin banyak yang Anda ketahui, semakin tepat serangan Anda, dan semakin kecil kemungkinan Anda membuang waktu atau tertangkap.

---

## 🤫 Pengumpulan Informasi Pasif

Pengumpulan informasi pasif berfokus pada penemuan informasi **tanpa berinteraksi langsung** dengan target. Pada dasarnya, Anda menyusun informasi intelijen dari sumber-sumber yang tersedia untuk umum (OSINT).

### 🎯 Apa yang Harus Dikumpulkan?
* Alamat IP dan catatan DNS (*DNS records*).
* Nama domain dan detail kepemilikan.
* Alamat email dan profil media sosial karyawan.
* Teknologi web yang digunakan (*framework*, CMS, jenis server).
* Subdomain yang dapat memperluas permukaan serangan.

### 🛠️ Teknik dan Alat (Tools)
* **Pencarian WHOIS** untuk data pendaftaran domain.
* **Google Dorking** untuk mencari file rahasia atau direktori yang terekspos.
* **Shodan / Censys** untuk mengidentifikasi layanan yang terekspos ke internet.
* **Sublist3r / Amass** untuk enumerasi subdomain.
* **Rekayasa Sosial** (mengumpulkan info via LinkedIn atau direktori perusahaan).

**Mengapa Sikap Pasif Itu Penting?**
Metode pasif memberikan pandangan luas terhadap target dengan risiko yang sangat kecil. Metode ini **tidak mencolok, aman**, dan sangat baik untuk memetakan lingkungan eksternal tanpa menimbulkan kecurigaan pihak target.

---

## 🔍 Pengumpulan Informasi Aktif

Berbeda dengan pasif, pengumpulan informasi aktif melibatkan **interaksi langsung** dengan sistem target. Tindakan ini dapat dideteksi oleh sistem keamanan (seperti IPS/IDS atau *Firewall*), tetapi memberikan data teknis yang jauh lebih akurat dan detail.

### 🎯 Apa yang Harus Dikumpulkan?
* Port yang terbuka dan layanan (*services*) yang sedang berjalan.
* Detail infrastruktur internal seperti nama *host* dan topologi jaringan.
* Data tingkat sistem seperti akun pengguna, versi OS, atau *share* jaringan (SMB).

### 🛠️ Teknik dan Alat (Tools)
* **Nmap** untuk pemindaian *port* TCP dan UDP.
* Mengambil spanduk (*Banner Grabbing*) menggunakan skrip Netcat atau Nmap.
* **SMBMap, enum4linux, atau SNMPwalk** untuk enumerasi spesifik.
* **Nessus / OpenVAS** untuk pemindaian kerentanan otomatis (*vulnerability scanning*).

**Mengapa Aktif Itu Penting?**
Metode aktif memberikan **wawasan yang lebih mendalam**. Metode ini mengungkapkan apa yang *sebenarnya* berjalan pada target dan bagaimana perilakunya. Tingkat detail ini sangat mutlak diperlukan untuk mempersiapkan eksploitasi.

---

## ⚖️ Pasif vs Aktif: Perbedaan Sebenarnya

| Aspek | Pengumpulan Pasif 🤫 | Pengumpulan Aktif 🔍 |
| :--- | :--- | :--- |
| **Penyembunyian** | Hampir tidak terlihat (*stealthy*). | Terlihat, berpotensi memicu log peringatan. |
| **Akurasi** | Bersifat luas tetapi seringkali tidak lengkap. | Data sangat presisi, akurat, dan terperinci. |
| **Risiko** | Sangat kecil (mendekati nol). | Risiko tinggi diekspos/diblokir oleh sistem pertahanan (*Blue Team*). |
| **Kasus Penggunaan**| Tahap awal pengintaian & OSINT. | Validasi kerentanan & persiapan eksploitasi akhir. |

---

## 🤝 Mengapa Keduanya Pendekatan Itu Penting?

Beberapa pemula menganggap teknik pasif sudah "cukup" karena aman. Di sisi lain, ada yang langsung terjun ke pemindaian aktif tanpa membangun konteks. Keduanya keliru jika digunakan secara terpisah:

* ❌ **Jika HANYA Pasif:** Anda tahu ada server, tapi tidak tahu apa yang berjalan di dalamnya.
* ❌ **Jika HANYA Aktif:** Anda dapat detail teknis, tapi mungkin melewatkan aset tersembunyi, atau langsung diblokir sebelum memulai karena membuat pihak target waspada.

**Sinergi Terbaik:**
1. Mulailah dengan **pengintaian pasif** untuk mengungkap domain, teknologi, dan info karyawan tanpa terdeteksi.
2. Lanjutkan dengan **enumerasi aktif** ke target yang sudah disaring untuk memvalidasi informasi, yang mengarah pada temuan yang dapat ditindaklanjuti.

---

## 🏢 Contoh di Dunia Nyata

Misalnya, Anda ditugaskan untuk menguji keamanan sebuah perusahaan jasa keuangan:

**Fase Pasif (Mengamati dari Jauh):**
* Anda mengidentifikasi subdomain `dev.company.com` dan `vpn.company.com`.
* Pencarian WHOIS mengungkapkan penyedia *hosting* mereka.
* Profil LinkedIn menunjukkan tim IT mereka sering bekerja dengan AngularJS.

**Fase Aktif (Menyentuh Sistem):**
* Pemindaian Nmap ke `vpn.company.com` menunjukkan bahwa OpenVPN berjalan pada port UDP 1194.
* Enumerasi aktif mengungkapkan versi OpenVPN tersebut usang dan memiliki kerentanan publik (CVE).
* Penyelidikan lebih lanjut mengungkap adanya akses SMB yang terbuka bebas dan berisi file konfigurasi sensitif.

*Perbedaannya jelas: pengumpulan pasif memberi tahu Anda **apa yang ada**, sementara pengumpulan aktif mengungkapkan **apa yang dapat dieksploitasi**.*

---

## ⚠️ Risiko dan Batasan Etika

Meskipun metode aktif sangat ampuh, ia datang dengan tanggung jawab besar. Sebagai *Penetration Tester* / *Ethical Hacker*, Anda harus selalu:
* ✅ **Tetap berada dalam lingkup (Scope) yang diizinkan** secara hukum tertulis (NDA/RoE).
* ✅ **Hindari pemindaian agresif** (seperti DoS) yang dapat menyebabkan server target lumpuh (*downtime*).
* ✅ **Laporkan temuan secara bertanggung jawab** untuk membantu organisasi memperkuat pertahanan mereka.

> **Ingat:** Tujuan pengujian penetrasi adalah untuk **meningkatkan keamanan**, bukan untuk merusak atau menimbulkan kepanikan yang tidak perlu.

---

## 🎯 Kesimpulan & Poin Penting

* **Pengumpulan Pasif = Fondasi tersembunyi.** Pengintaian luas dengan risiko rendah.
* **Pengumpulan Aktif = Akurasi detail.** Wawasan mendalam dengan risiko terdeteksi yang tinggi.
* **Keduanya = Visibilitas lengkap.** Salah satunya tanpa yang lain akan meninggalkan titik buta (*blind spot*).

Pengumpulan informasi bukan sekadar mengumpulkan data acak, melainkan mengumpulkan **data yang tepat dengan cara yang tepat**. Ketika digabungkan, pasif dan aktif memberikan kejelasan dan ketelitian yang dibutuhkan untuk penilaian keamanan yang bermakna. 

Lain kali Anda memulai pengujian penetrasi, jangan bertanya *"Haruskah saya menggunakan teknik pasif atau aktif?"* Sebaliknya, tanyakan: **"Bagaimana saya dapat menggunakan keduanya bersama-sama untuk melihat medan pertempuran secara menyeluruh?"**

---
*Materi disadur dari artikel ["Passive vs Active Information Gathering: What to Collect and Why" oleh Vivek Bhatt](https://medium.com/@vivekbhatt2002/passive-vs-active-information-gathering-what-to-collect-and-why-d0c85730e32b).*