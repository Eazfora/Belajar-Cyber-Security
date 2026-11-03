# 🚀 Pengintaian Aktif dalam Pengujian Penetrasi (Active Reconnaissance)

Berbeda dengan pengintaian pasif yang bersifat mengumpulkan informasi dari jauh tanpa menyentuh target, **Pengintaian Aktif (Active Reconnaissance)** melibatkan **interaksi langsung** dengan sistem target. Pada tahap ini, *pentester* mengirimkan paket data ke server target dan menganalisis responsnya untuk mengungkap *port* yang terbuka, layanan yang berjalan, hingga sistem operasi yang digunakan.

Risiko terdeteksi oleh *Firewall* atau *Intrusion Detection System (IDS)* sangat tinggi, namun data yang didapatkan sangat detail, akurat, dan krusial untuk persiapan eksploitasi.

---

## 📑 Daftar Isi
1. [Alat Dasar: nslookup](#1-alat-dasar-nslookup)
2. [Senjata Utama: Nmap (Network Mapper)](#2-senjata-utama-nmap-network-mapper)
   - [Instalasi & Bantuan Dasar](#a-instalasi--bantuan-dasar)
   - [Penentuan Target (Target Specification)](#b-penentuan-target-target-specification)
   - [Pemindaian Port & Jaringan](#c-pemindaian-port--jaringan)
   - [Deteksi OS & Versi Layanan](#d-deteksi-os--versi-layanan)
   - [Bypass Firewall & Teknik Evasion](#e-bypass-firewall--teknik-evasion)
   - [Analisis Jaringan & Output](#f-analisis-jaringan--output)
3. [Alat Kustom: Skrip Pelacak Geolokasi IP](#3-alat-kustom-skrip-pelacak-geolokasi-ip)

---

## 1. Alat Dasar: `nslookup`

**Teori:**
`nslookup` (Name Server Lookup) adalah alat antarmuka baris perintah (CLI) yang digunakan untuk melakukan kueri ke *Domain Name System* (DNS). Alat ini membantu memetakan nama domain ke alamat IP (atau sebaliknya) dan mengambil catatan DNS spesifik seperti *Mail Exchange* (MX) atau *Name Server* (NS).

**Cara Penggunaan:**
`nslookup` dapat digunakan secara interaktif (masuk ke dalam *prompt* nslookup) atau non-interaktif (langsung dalam satu baris perintah).

**Contoh Penggunaan:**
```bash
# Mencari alamat IP dari sebuah domain (A Record)
nslookup target.com

# Mencari server email dari sebuah domain (MX Record)
nslookup -type=mx target.com

# Mencari Name Server (NS Record)
nslookup -type=ns target.com

# Menggunakan server DNS spesifik (misal server Google 8.8.8.8) untuk kueri
nslookup target.com 8.8.8.8
```

---

## 2. Senjata Utama: Nmap (Network Mapper)

Nmap, kodenya ditulis oleh Gordon Lyon, adalah aplikasi *open-source* yang sering dipakai sebagai alat keamanan (*security tool*) untuk mengeksplorasi jaringan komputer, memindai keamanan, dan mengauditnya. 

Nmap menjawab pertanyaan kritis seperti: komputer apa saja yang berjalan pada sebuah jaringan, IP address yang aktif, sistem operasi target, port yang digunakan, hingga menemukan komputer yang tidak sesuai dengan standar minimum keamanan.

Meskipun parameternya kompleks, berikut adalah panduan perintah Nmap yang sudah dirapikan untuk *Sysadmin* & *Pentester*:

### A. Instalasi & Bantuan Dasar
```bash
# Tahapan untuk menginstall Nmap pada Kali Linux/Debian:
sudo apt-get install nmap

# Menampilkan keseluruhan perintah/bantuan Nmap:
nmap -h
```

### B. Penentuan Target (Target Specification)
```bash
# Scan satu IP atau satu Host
nmap 10.11.9.111
nmap ftumj.ac.id

# Scan dengan verbose (info lebih detail)
nmap -v ftumj.ac.id

# Scan lebih dari satu IP / Range / Subnet
nmap 10.11.9.1 10.11.9.2 10.11.9.3
nmap 10.11.9.1,2,3
nmap 10.11.9.1-20
nmap 10.11.9.*           # Wildcard scan
nmap 10.11.9.0/24        # Scan keseluruhan subnet

# Memberikan pengecualian saat scan jaringan (--exclude)
nmap 10.11.9.0/24 --exclude 10.11.9.1
nmap 10.11.9.0/24 --exclude 10.11.9.1,10.11.9.3
```

### C. Pemindaian Port & Jaringan
```bash
# Scan untuk mencari server yang sedang "hidup" (Ping Scan)
nmap -sP 10.11.9.0/24

# Melakukan scan cepat (Fewer ports)
nmap -F 10.11.9.1

# Hanya menampilkan port yang terbuka / aktif
nmap --open 10.11.9.1

# Cara cepat scan port seluruh komputer dengan timing agresif (-T5)
nmap -T5 192.168.1.0/24

# Scan IP Protocol (Mengetahui protokol apa saja yang didukung target)
nmap -sO 192.168.1.1
```

### D. Deteksi OS & Versi Layanan (Fingerprinting)
```bash
# Mendeteksi Operating System (OS) mesin target
nmap -O 10.11.9.1
nmap -O --osscan-guess 10.11.9.1       # Memaksa menebak OS
nmap -v -O --osscan-guess 10.11.9.1    # Dengan verbose

# Mendeteksi versi layanan/aplikasi (Web server, SSH, dll)
nmap -sV 10.11.9.1

# Scan Agresif (Mendeteksi OS, Versi, Script Scanning, dan Traceroute sekaligus)
nmap -A 10.11.9.2
nmap -v -A 10.11.9.2
```

### E. Bypass Firewall & Teknik Evasion
```bash
# Mengetahui apakah host diproteksi firewall (TCP ACK Scan)
nmap -sA 10.11.9.1

# Scan target host yang memblokir Ping (No Ping / Treat as Online)
nmap -PN 10.11.9.2

# Bypass Firewall dengan TCP ACK / TCP SYN Ping (Jika ICMP diblokir)
nmap -PS 10.11.9.1
nmap -PS 80,21,443 10.11.9.1
nmap -PA 10.11.9.1

# UDP Ping & IP Ping
nmap -PU 192.168.1.1        # UDP Ping
nmap -PO 192.168.1.1        # IP Ping

# Macam-macam teknik Stealth & TCP Scan
nmap -sS 192.168.1.1        # Stealth (SYN) scan - Paling umum
nmap -sT 192.168.1.1        # TCP Connect scan
nmap -sW 192.168.1.1        # TCP Window scan
nmap -sM 192.168.1.1        # TCP Maimon scan
nmap -sU 192.168.1.1        # UDP scan (DNS, SNMP, DHCP)

# Fragmentasi Paket (Mengecoh deteksi Firewall/IDS)
nmap -f 192.168.1.1
nmap --mtu 32 192.168.1.1

# Decoy Scan (Menyelipkan IP Anda di antara IP umpan agar IP asli tersamarkan)
nmap -n -D decoy-ip1,decoy-ip2,your-ip,decoy-ip3 target-ip
nmap -n -D 192.168.1.5,10.5.1.2,ME,172.1.2.4 192.168.1.10

# MAC Address Spoofing (Memalsukan MAC Address)
nmap --spoof-mac MAC-ADDRESS-ANDA 192.168.1.1
nmap -v -sT -PN --spoof-mac 0 192.168.1.1    # "0" untuk Random MAC
```

### F. Analisis Jaringan & Output
```bash
# Menampilkan ALASAN (reason) mengapa port dilaporkan terbuka/tertutup
nmap --reason 10.10.10.1

# Menampilkan semua jejak paket yang dikirim dan diterima (Debugging)
nmap --packet-trace 10.11.9.1

# Menampilkan interface jaringan lokal dan routing table
nmap --iflist

# Menyimpan hasil scan ke dalam file teks biasa (-oN)
nmap 192.168.1.1 > output.txt
nmap -oN output.txt 192.168.1.1
```

---

## 3. Alat Kustom: Skrip Pelacak Geolokasi IP

Selain menggunakan *tools* bawaan, *Information Gathering* seringkali membutuhkan skrip buatan sendiri untuk tugas spesifik, seperti mencari lokasi server/IP. 

Berikut adalah implementasi Python bersih (menggunakan API publik) untuk melacak detail lokasi geografis dari sebuah nama domain.

**File:** `geolocation_tracker.py`
```python
import socket
import requests

def get_geolocation(hostname):
    """Mendapatkan informasi geolokasi dari sebuah nama domain atau IP."""
    try:
        # Resolve hostname ke IP address
        ip_address = socket.gethostbyname(hostname)
        print(f"IP Address: {ip_address}")
    except socket.gaierror:
        print(f"Error: Hostname '{hostname}' tidak dapat ditemukan (resolve).")
        return

    # Endpoint API publik untuk melacak IP
    request_url = f'https://geolocation-db.com/json/{ip_address}'
    
    try:
        # Menambahkan timeout agar program tidak hang jika server lambat
        response = requests.get(request_url, timeout=10)
        response.raise_for_status() 
        
        # Parse JSON response
        geolocation_data = response.json()
        
        print("\n--- Data Geolokasi ---")
        # Mencetak data secara rapi menggunakan formatting
        for key, value in geolocation_data.items():
             print(f"{key.capitalize():<15}: {value}")

    except requests.exceptions.RequestException as e:
        print(f"Error saat menghubungi API: {e}")
    except ValueError:
        print("Error: Format response dari server tidak valid.")

if __name__ == "__main__":
    print("=== Pelacak Geolokasi IP & Domain ===")
    domain_input = input('Masukkan nama domain (contoh: google.com): ').strip()
    
    if domain_input:
        get_geolocation(domain_input)
    else:
        print("Input tidak boleh kosong.")
```