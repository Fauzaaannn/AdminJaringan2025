<div align="center">
  <h1 style="text-align: center;font-weight: bold">Laporan Praktikum
  <br>Workshop Administrasi Jaringan</h1>
  <h4 style="text-align: center;">Dosen Pengampu : Dr. Ferry Astika Saputra, S.T., M.Sc.</h4>
</div>
<br />
<div align="center">
  <img src="https://upload.wikimedia.org/wikipedia/id/4/44/Logo_PENS.png" alt="Logo PENS">
  <h3 style="text-align: center;">Disusun Oleh : </h3>
  <p style="text-align: center;">
    <strong>Nama: Fauzan Abderrasheed</strong><br>
    <strong>NRP: 3123500020 </strong><br>
    <strong>Kelas: D3 IT A</strong>
  </p>
<h3 style="text-align: center;line-height: 1.5">Politeknik Elektronika Negeri Surabaya<br>Departemen Teknik Informatika Dan Komputer<br>Program Studi Teknik Informatika<br>2023/2024</h3>
  <hr><hr>
</div>


### Instalasi Sistem Operasi

Distribusi Linux dan FreeBSD memiliki prosedur yang sederhana untuk instalasi dasar

- **Instalasi Fisik vs. Virtual:**
    
    Pada mesin fisik, proses booting dapat dilakukan dari CD, DVD atau USB drive. Sedangkan di mesin virtual, proses booting dapat dilakukan dari file ISO. Menginstal OS dasar dari media lokal cukup mudah berkat aplikasi GUI yang memandu untuk melalui proses tersebut.
    
- **Instalasi Jaringan:**
Jika anda harus menginstal sistem operasi pada lebih dari satu komputer, penggunaan media lokal (CD/DVD/USB) menjadi tidak praktis karena proses yang memakan waktu, rawan kesalahan dan membosankan karena mengulangi langkah yang sama berulang kali. Solusinya adalah melakukan instalasi sistem operasi melalui server jaringan.
    
    Metode yang paling umum adalah menggunakan protokol seperti DHCP dan TFTP tanpa media fisik, kemudian sistem akan mengunduh file instalasi OS dari server jaringan menggunakan HTTP, FTP, atau NFS. File instalasi tersebut bisa berada di server yang sama atau berbeda
    
    Metode PXE (Preboot eXecution Environment) memungkinkan kita untuk mengatur instalasi sepenuhnya otomatis. Skema ini adalah standar dari intel yang memungkinkan sistem melakukan booting dari antarmuka jaringan.
    
    PXE menyediakan kemampuan jaringannya melalui API standar yang digunakan oleh BIOS sistem, hal tersebut memungkinkan satu boot loader untuk melakukan netboot pada setiap PC yang mendukung PXE tanpa perlu menyediakan driver khusus untuk setiap kartu jaringan.
    

### Sistem Manajemen Paket Linux

- **Format Paket:**
    
    Format paket yang paling umum digunakan pada sistem Linux:
    
    - **RPM:** Digunakan oleh distribusi seperti Red Hat, CentOS, SUSE, dan Amazon Linux.
    - **.deb:** Digunakan oleh sistem Debian dan Ubuntu. Terpisah namun sama populer
    
    Kedua format ini secara fungsional sangat mirip.
    
- **Alat Tingkat Rendah:**
    
    Setiap sistem memiliki alat dasar:
    
    - **rpm** untuk paket RPM.
    - **dpkg** untuk paket .deb.

### **Manajemen Paket Tingkat Tinggi:**

- Alat manajemen paket tinggi memungkinkan anda untuk menginstal, menghapus, dan memperbarui paket. Alat ini juga memungkinkan pencarian paket dan melihat daftar paket yang terinstal pada sistem anda.
- **Repositori Paket**
    
    Konfigurasi default sistem manajemen paket biasanya mengarah ke satu atau beberapa server web atau FTP yang dikelola oleh distributor
    
    - *Release* adalah snapshot yang konsisten dari keseluruhan paket
    - *Component* adalah subset dari perangkat lunak dalam sebuah release
    - *Architecture* mewakili perangkat keras dengan harapan mesin dalam kelas arsitektur yang sama cukup serupa sehingga dapat menjalankan binary yang sama. Arsitektur adalah instansi dari release, misalnya, arsitektur i386 dari release Fedora 20.
- **yum (Yellowdog Updater, Modified)**
    
    **yum** adalah manajer paket untuk sistem Linux yang kompatibel dengan RPM. yum melakukan resolusi dependensi saat menginstal, memperbarui, dan menghapus paket. Ia dapat mengelola paket dari repositori yang sudah terinstal, dan juga dapat melakukan operasi baris perintah pada paket individual.
    
- **APT (Advanced Package Tool)**
    
    APT merupakan koleksi alat yang bekerja sama untuk menyediakan sistem manajemen paket yang lengkap. Kumpulan alat-alat tersebut awalnya dikembangkan untuk sistem berbasis Debian (.deb), alat-alat tersebut meliputi alat seperti: 
    
    - **apt-get**: Alat baris perintah untuk menangani paket. Ini melakukan tugas manajemen paket seperti instalasi, penghapusan, dan pembaruan.
    - **apt-cache**: Alat untuk mencari dan menanyakan cache paket APT.
    - **apt-file**: Alat untuk mencari file di dalam paket.
    - **apt-show-versions**: Alat untuk menampilkan versi paket.
    - **aptitude**: Antarmuka tingkat tinggi untuk sistem manajemen paket. Alat ini dapat melakukan sebagian besar tugas yang dapat dilakukan oleh **apt-get**, dan banyak lainnya.
    - **apt-mirror**: Alat yang memungkinkan Anda untuk mencerminkan repositori paket.
    
    APT dapat menangani paket .deb dan RPM, dan merupakan sistem yang paling banyak digunakan pada distribusi berbasis Debian.
    Aturan pertama dalam menggunakan APT pada sistem Ubuntu adalah untuk mengabaikan keberadaan **dselect**, yang bertindak sebagai antarmuka depan untuk sistem paket Debian.
    

### Lokalisasi dan Konfigurasi Perangkat Lunak

- Menyesuaikan sistem dengan lingkungan lokal (atau cloud) Anda adalah salah satu bidang utama dalam administrasi sistem. Pendekatan yang terstruktur dan dapat direproduksi penting untuk menghindari sistem yang unik ("snowflake") yang sulit untuk dipulihkan setelah terjadi masalah besar.

Secara keseluruhan, bab ini dirancang untuk memberikan pemahaman praktis mengenai cara menginstal sistem operasi dan mengelola paket perangkat lunak secara efisien, terutama dalam lingkungan yang memerlukan otomasi dan skalabilitas.