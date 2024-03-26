# Konfigurasi VLAN Menggunakan Packet Tracer

## Tabel Penyediaan Alamat

| Perangkat | Antarmuka | Alamat IP    | Subnet Mask   | VLAN |
| --------- | --------- | ------------ | ------------- | ---- |
| PC1       | NIC       | 172.17.10.21 | 255.255.255.0 | 10   |
| PC2       | NIC       | 172.17.20.22 | 255.255.255.0 | 20   |
| PC3       | NIC       | 172.17.30.23 | 255.255.255.0 | 30   |
| PC4       | NIC       | 172.17.10.24 | 255.255.255.0 | 10   |
| PC5       | NIC       | 172.17.20.25 | 255.255.255.0 | 20   |
| PC6       | NIC       | 172.17.30.26 | 255.255.255.0 | 30   |

## Tujuan

1. Verifikasi Konfigurasi VLAN Default
2. Konfigurasi VLAN
3. Menetapkan VLAN ke Port

## Latar Belakang

VLAN (Virtual Local Area Networks) digunakan untuk segmentasi logis jaringan, memberikan manfaat seperti peningkatan keamanan, penyederhanaan manajemen jaringan, dan penggunaan bandwidth yang lebih baik.

## Bagian 1: Lihat Konfigurasi VLAN Default

### Langkah 1: Tampilkan VLAN saat ini

Pada S1, gunakan perintah yang menampilkan semua VLAN yang dikonfigurasi. Secara default, semua antarmuka ditugaskan ke VLAN 1.

### Langkah 2: Verifikasi konektivitas antara PC di jaringan yang sama

Perhatikan bahwa setiap PC dapat melakukan ping ke PC lain yang berbagi subnet yang sama.

- PC1 dapat melakukan ping ke PC4
- PC2 dapat melakukan ping ke PC5
- PC3 dapat melakukan ping ke PC6

Ping ke host di jaringan lain gagal.

## Bagian 2: Konfigurasi VLAN

### Langkah 1: Buat dan Beri Nama VLAN pada S1

a. Buat VLAN berikut. Nama harus case-sensitive dan harus sesuai dengan persyaratan yang tepat:

- VLAN 10: Fakultas/Staf

```bash
S1#(config)# vlan 10
S1#(config-vlan)# name Faculty/Staff
```

b. Buat sisa VLAN.

- VLAN 20: Mahasiswa
- VLAN 30: Tamu(Default)
- VLAN 99: Manajemen&Native
- VLAN 150: VOICE

### Langkah 2: Verifikasi Konfigurasi VLAN

**Pertanyaan:** Perintah mana yang hanya akan menampilkan nama VLAN, status, dan port yang terkait pada sebuah switch?

### Langkah 3: Buat VLAN pada S2 dan S3

Gunakan perintah yang sama dari Langkah 1 untuk membuat dan memberi nama VLAN yang sama pada S2 dan S3.

### Langkah 4: Verifikasi Konfigurasi VLAN

Tutup jendela konfigurasi.

## Bagian 3: Menetapkan VLAN ke Port

### Langkah 1: Menetapkan VLAN ke port aktif pada S2

a. Konfigurasikan antarmuka sebagai port akses dan tetapkan VLAN seperti berikut:

- VLAN 10: FastEthernet 0/11

```bash
S2(config)# interface f0/11
S2(config-if)# switchport mode access
S2(config-if)# switchport access vlan 10
```

b. Tetapkan port yang tersisa ke VLAN yang sesuai.

- VLAN 20: FastEthernet 0/18
- VLAN 30: FastEthernet 0/6

### Langkah 2: Menetapkan VLAN ke port aktif pada S3

S3 menggunakan penugasan port akses VLAN yang sama seperti S2. Konfigurasikan antarmuka sebagai port akses dan tetapkan VLAN seperti berikut:

- VLAN 10: FastEthernet 0/11
- VLAN 20: FastEthernet 0/18
- VLAN 30: FastEthernet 0/6

### Langkah 3: Menetapkan VLAN VOICE ke FastEthernet 0/11 pada S3

Sesuai topologi, antarmuka S3 FastEthernet 0/11 terhubung ke IP Phone Cisco dan PC4. Antarmuka F0/11 harus dikonfigurasi untuk mendukung lalu lintas pengguna ke PC4 menggunakan VLAN 10 dan lalu lintas suara ke IP Phone menggunakan VLAN 150. Antarmuka juga harus mengaktifkan QoS dan mempercayai nilai Class of Service (CoS) yang diberikan oleh IP Phone.

```bash
S3(config)# interface f0/11
S3(config-if)# mls qos trust cos
S3(config-if)# switchport voice vlan 150
```

### Langkah 4: Verifikasi kehilangan konektivitas

Sebelumnya, PC yang berbagi jaringan yang sama dapat saling melakukan ping.

Studi output dari perintah berikut di S2 dan jawab pertanyaan berikut berdasarkan pengetahuan Anda tentang komunikasi antar VLAN. Perhatikan dengan cermat penugasan port Gig0/1.

```bash
S2# show vlan brief
```

Pertanyaan:

- Meskipun port akses ditetapkan ke VLAN yang sesuai, apakah ping berhasil? Jelaskan.

Ping tidak berhasil meskipun port akses ditetapkan ke VLAN yang sesuai. Hal ini terjadi karena PC1 dan PC4 sekarang berada dalam VLAN yang berbeda, yaitu VLAN 10 dan VLAN 20. VLAN memisahkan jaringan logis, sehingga perangkat dalam VLAN yang berbeda tidak dapat berkomunikasi langsung satu sama lain tanpa menggunakan router atau perangkat jembatan yang sesuai. Oleh karena itu, meskipun port akses sudah dikonfigurasi dengan benar, ping antara PC1 dan PC4 tidak akan berhasil karena mereka berada dalam VLAN yang berbeda.

- Apa yang bisa dilakukan untuk menyelesaikan masalah ini?

Untuk menyelesaikan masalah ketidakberhasilan ping antara PC1 dan PC4 setelah konfigurasi VLAN, langkah-langkah berikut dapat dilakukan:

1. **Periksa Konfigurasi VLAN**: Pastikan bahwa VLAN 10 dan VLAN 20 telah dibuat dan dikonfigurasi dengan benar di switch (S1, S2, dan S3). Pastikan juga bahwa port yang terhubung ke PC1 dan PC4 telah dikonfigurasi dengan benar sebagai bagian dari VLAN yang sesuai.

2. **Periksa Konektivitas Fisik**: Pastikan kabel yang terhubung ke PC1 dan PC4 terpasang dengan baik dan tidak mengalami masalah fisik seperti putus atau kendor.

3. **Periksa Konfigurasi IP**: Pastikan bahwa PC1 dan PC4 memiliki konfigurasi IP yang sesuai untuk VLAN yang mereka terhubung. Pastikan juga bahwa subnet mask yang digunakan benar.

4. **Periksa Konfigurasi Gateway**: Pastikan bahwa PC1 dan PC4 memiliki gateway yang benar untuk berkomunikasi antar-VLAN jika perlu.

5. **Periksa Firewall**: Pastikan tidak ada firewall atau perangkat keamanan lain yang memblokir lalu lintas antara VLAN 10 dan VLAN 20.

6. **Periksa Routing**: Jika komunikasi antar-VLAN diperlukan, pastikan ada router yang terhubung ke kedua VLAN dan telah dikonfigurasi dengan benar untuk melakukan routing antar-VLAN.

7. **Periksa Jaringan Keseluruhan**: Periksa apakah ada masalah jaringan yang lebih besar yang dapat memengaruhi komunikasi antara PC1 dan PC4, seperti masalah switch atau router lainnya.

Setelah melakukan langkah-langkah di atas, ping antara PC1 dan PC4 seharusnya berhasil jika masalahnya telah diatasi dengan benar.

## Kesimpulan:

Dalam aktivitas konfigurasi VLAN dengan Packet Tracer, langkah-langkah meliputi verifikasi konfigurasi VLAN default, pembuatan dan penamaan VLAN, serta penugasan VLAN ke port-port aktif. VLAN membantu dalam administrasi grup-grup logis pada jaringan dan memungkinkan manajemen yang lebih efisien.
