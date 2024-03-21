# Konfigurasi VLAN di Cisco Packet Tracer

Ini adalah contoh konfigurasi VLAN di Cisco Packet Tracer. Tutorial ini menunjukkan langkah-langkah untuk membuat VLAN dan menghubungkannya dengan antarmuka switch.

## Langkah-langkah Konfigurasi

1. **Buka Cisco Packet Tracer**: Buka aplikasi Cisco Packet Tracer di komputer Anda.

2. **Buat Topologi Jaringan**: Buatlah topologi jaringan yang sesuai dengan kebutuhan Anda. Pastikan untuk menambahkan switch atau switches yang akan digunakan untuk konfigurasi VLAN.

3. **Konfigurasi VLAN**:

   - Masuk ke mode konfigurasi switch dengan perintah `configure terminal`.
   - Buat VLAN baru dengan perintah `vlan <vlan-id>`.
   - Konfigurasikan antarmuka switch yang terhubung ke perangkat lain menggunakan perintah `interface <interface-id>`, `switchport mode access`, dan `switchport access vlan <vlan-id>`.

4. **Verifikasi Konfigurasi**: Lakukan verifikasi untuk memastikan bahwa VLAN telah dikonfigurasi dengan benar. Gunakan perintah `show vlan` dan `show interfaces switchport` untuk melihat konfigurasi VLAN dan antarmuka switch.

5. **Simpan Konfigurasi**: Terakhir, simpan konfigurasi switch menggunakan perintah `write memory` atau `copy running-config startup-config`.

## Verifikasi

Pastikan untuk memeriksa kembali konfigurasi setelah menyimpannya untuk memastikan bahwa semua perubahan telah disimpan dengan benar.

## Kontribusi

Kontribusi terhadap tutorial ini sangat dipersilakan. Jika Anda menemukan kesalahan atau memiliki saran untuk perbaikan, silakan buka pull request atau issue di repositori ini.
