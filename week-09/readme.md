# Konfigurasi DNS Host

![0](00.jpg)
## Konfigurasi Jaringan Internal
### Instalasi BIND

Masuk root, dan gunakan command dibawah untuk menginstall bind9

```bash
root@dlp:~# apt -y install bind9 bind9utils
```

### Konfigurasi dan Penyesuaian BIND

Menambahkan file konfigurasi baru yaitu `named.conf.internal-zones` ke dalam file utama konfigurasi BIND `/etc/bind/named.conf`

![1.jpg](1.jpg)

### Konfigurasi akses kontrol dan kebijakan query pada BIND DNS Server

![2.jpg](2.jpg)

- **Menentukan ACL (Access Control List)**
  - Membuat ACL bernama `internal-network` untuk jaringan **192.168.4.0/24**. Dimana jaringan ini adalah jaringan dari Mikrotik yang sudah diberikan untuk kelompok 4
  - ACL ini digunakan untuk menentukan siapa saja yang diizinkan mengakses layanan DNS.
- **Mengatur kebijakan query dan transfer zona**
  - `allow-query { localhost; internal-network; };` → Hanya mengizinkan **localhost** dan jaringan **internal** untuk melakukan query ke DNS server.
  - `allow-transfer { localhost; };` → Hanya mengizinkan **localhost** untuk melakukan transfer zona, biasanya untuk secondary DNS.
- **Mengaktifkan rekursi**
  - `recursion yes;` → Mengizinkan pencarian rekursif, yang berguna untuk melakukan resolusi nama domain selain zona yang dikelola sendiri.
- **Mengatur validasi DNSSEC dan konfigurasi IPv6**
  - `dnssec-validation auto;` → Mengaktifkan validasi DNSSEC secara otomatis.
  - `listen-on-v6 { any; };` → Konfigurasi agar BIND mendengarkan koneksi IPv6.

### Konfigurasi Zona DNS di BIND

![image.png](images/etc-bind-named-conf-internal-zones.png)

- **Zona Forward (kelompok4.home)**
  - Zona ini digunakan untuk menerjemahkan **nama domain ke alamat IP**.
  - Disimpan dalam file **`/etc/bind/kelompok4.home.lan`**.
  - Bertindak sebagai **master** (utama), artinya server ini adalah sumber resmi data DNS untuk domain tersebut.
  - `allow-update { none; };` → Tidak mengizinkan update dinamis ke zona ini.
- **Zona Reverse (80.168.192.in-addr.arpa)**
  - Zona ini digunakan untuk **menerjemahkan alamat IP ke nama domain** (reverse lookup).
  - Disimpan dalam file **`/etc/bind/80.168.192.db`**.
  - Juga bertindak sebagai **master**, dengan **update dinamis dinonaktifkan**.

### Konfigurasi opsi BIND untuk menggunakan hanya IPv4 dan menonaktifkan IPv6

![image.png](images/etc-default-named.png)

**Mengedit file `/etc/default/named`**

- Menambahkan opsi `OPTIONS="-u bind -4"`, yang menginstruksikan BIND untuk hanya menggunakan **IPv4** dan mengabaikan **IPv6**.
- Ini berguna jika jaringan Anda hanya menggunakan IPv4 dan ingin menghindari log error terkait IPv6.

## Konfigurasi Zone Files

### Pembuatan dan konfigurasi file zona forward lookup pada BIND DNS Server

Buat file zona yang memungkinkan server menerjemahkan nama domain menjadi alamat IP.
Konfigurasikan seperti di bawah ini menggunakan Jaringan internal [**192.168.80.0/24**.], Nama domain [kelompok4.home].

![image.png](images/etc-bind-kelompok4-home-lan.png)

### Pembuatan dan konfigurasi file zona reverse lookup pada BIND DNS Server.

Buat file zona yang memungkinkan server menerjemahkan alamat IP menjadi nama domain.
Konfigurasikan seperti di bawah ini menggunakan Jaringan internal [**192.168.80.0/24**.], Nama domain [kelompok4.home].

![image.png](images/etc-bind-80-168-192-db.png)

## BIND: Verify Resolution

### Restart BIND untuk menerapkan perubahan

Masuk root dan gunakan command dibawah ini

```bash
root@dlp:~# systemctl restart named
```

### Konfigurasi DNS Client untuk menggunakan DNS Server sendiri

![image.png](images/etc-resolve-conf.png)

File **`/etc/resolv.conf`** digunakan oleh sistem Linux untuk menentukan **DNS server mana yang akan digunakan untuk melakukan query DNS** (resolving domain ke IP dan sebaliknya).

Dengan mengedit **`/etc/resolv.conf`** dan mengubah **nameserver** menjadi **10.0.0.30**, berarti:

✅ Mengatur sistem supaya pakai **DNS Server sendiri** (BIND di **10.0.0.30**)

✅ Prioritaskan pencarian DNS ke **server lokal dulu**, sebelum ke DNS eksternal

✅ Bikin sistem bisa resolve **domain lokal** yang cuma dikenali oleh DNS internal

### **DNS Query menggunakan DiG (Domain Information Groper)** untuk **Forward Lookup**.

![image.png](images/dig-kelompok4-home.png)

Perintah di atas digunakan untuk **mengecek resolusi nama domain ke alamat IP (Forward DNS Lookup)** dengan memanfaatkan **DNS Server yang telah dikonfigurasi**.

### Reverse DNS Lookup

![image.png](images/dig-ip-server.png)

Perintah di atas digunakan untuk **melakukan pencarian balik (reverse lookup)** guna menemukan **nama domain yang terkait dengan alamat IP** tertentu.
