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

# Instalasi Debian dan Oracle Virtual Box

## Solve LAN Wired Not Connected

![versi http](assets/instalasi-debian-dan-oracleVM/1.png)

```
sudo dhclient -v
```

Perintah di atas digunakan untuk menginisialisasi kembali konfigurasi jaringan secara dinamis melalu DHCP dengan menampilkan output secara rinci

## IP Komputer Lab

![versi http](assets/instalasi-debian-dan-oracleVM/2.jpg)

Setelah berhasil connect dengan LAN maka komputer akan mendapatkan IP Address

## Clone Github

Install git di komputer lab

![versi http](assets/instalasi-debian-dan-oracleVM/3.png)

```
sudo apt install git
```

Gunakan command di atas untuk menginstall git di komputer lab

Lalu lakukan clone menggunakan git clone

![versi http](assets/instalasi-debian-dan-oracleVM/4.png)

```
git clone https://github.com/ferryastika/unix-and-linux-sysadmin-notes.git
```

## Cek OS

![versi http](assets/instalasi-debian-dan-oracleVM/5.png)

```
lsb_release -a
```

Gunakan command di atas untuk mengecek OS komputer yang digunakan

## Download VirtualBox

![versi http](assets/instalasi-debian-dan-oracleVM/6.png)

https://www.virtualbox.org/wiki/Linux_Downloads

Download menyesuaikan dengan OS yang digunakan komputer

## Download ISO Debian 12

![versi http](assets/instalasi-debian-dan-oracleVM/7.png)

https://www.debian.org/download

ISO yang akan digunakan di dalam VirtualBox

## Install VirtualBox

![versi http](assets/instalasi-debian-dan-oracleVM/8.png)

```
sudo dpkg -i virtualbox-7.1_7.1.6-167084~Debian~bookworm_amd64.deb
```

Gunakan command di atas untuk melakukan instalasi VirtualBox

## Solving Error VirtualBox

Setelah proses instalasi, akan muncul error seperti ini saat VirtualBox dibuka

![versi http](assets/instalasi-debian-dan-oracleVM/9.png)

Solve menggunakan perintah:

```
sudo usermod -a -G vboxusers $USERS
```

Perintah ini menambahkan pengguna yang sedang login ke dalam grup `vboxusers`, yang biasanya diperlukan agar bisa mengakses fitur tertentu di VirtualBox, seperti USB passthrough.

## New Virtual Machine

Membuat Virtual Machine baru, sesuaikan Name dan Operating System seperti gambar di bawah ini

![versi http](assets/instalasi-debian-dan-oracleVM/10.png)

Sesuaikan Unattended Install seperti gambar dibawah ini

![versi http](assets/instalasi-debian-dan-oracleVM/11.png)

Sesuaikan Hardware seperti gambar dibawah ini

![versi http](assets/instalasi-debian-dan-oracleVM/12.png)

Sesuaikan Hard Disk seperti gambar dibawah ini

![versi http](assets/instalasi-debian-dan-oracleVM/13.png)

## Kernel Error

![versi http](assets/instalasi-debian-dan-oracleVM/kernel_error.png)

Gunakan perintah ini untuk memperbaiki kernel error

```
sudo apt update
sudo apt install dkms build-essential linux-headers-$(uname -r)
sudo /sbin/vboxconfig
```
![versi http](assets/instalasi-debian-dan-oracleVM/fixing_kernel1.png)

![versi http](assets/instalasi-debian-dan-oracleVM/fixing_kernel2.png)

## Run Virtual Machine

Jalankan dan tunggu sampai debian pada VM sudah terinstall dan terinisialisasi dengan benar

![versi http](assets/instalasi-debian-dan-oracleVM/14.png)

![versi http](assets/instalasi-debian-dan-oracleVM/15.png)

![versi http](assets/instalasi-debian-dan-oracleVM/16.png)

Jika sudah seperti gambar di bawah, maka bisa dipastikan install debian 12 pada VirtualBox telah berhasil

![versi http](assets/instalasi-debian-dan-oracleVM/17.png)

Selanjutnya klik Next hingga done, jika sudah seperti gambar di bawah maka debian pada VirtualBox sudah siap digunakan

![versi http](assets/instalasi-debian-dan-oracleVM/18.png)