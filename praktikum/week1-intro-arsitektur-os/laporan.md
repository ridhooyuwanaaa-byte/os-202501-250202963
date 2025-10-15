
# Laporan Praktikum Minggu [X]
["Arsitektur Sistem Operasi dan Kernel"]

---

## Identitas
- **Nama**  : Naufal adib bissibyan  
- **NIM**   : 250505958 
- **Kelas** : 1 ikr a

---

## Tujuan
menjelaskan fungsi utama sistem operasi dan peran kernel serta system call.

---

## Dasar Teori
Sistem operasi adalah perangkat lunak dasar yang bertindak sebagai penghubung antara pengguna dan perangkat keras komputer, mengelola semua sumber daya sistem seperti prosesor, memori, dan perangkat penyimpanan. Tanpa sistem operasi, komputer atau ponsel tidak dapat menjalankan aplikasi atau instruksi apa pun karena tidak ada yang mengelola operasi dan interaksi dengan perangkat keras. Contoh sistem operasi yang populer antara lain Windows, macOS, Linux, dan Android

---

## Langkah Praktikum
1. Langkah-langkah yang dilakukan.  
2. Perintah yang dijalankan.  
3. File dan kode yang dibuat.  
4. Commit message yang digunakan.

---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash
uname -a
lsmod | head
dmesg | head
```

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](screenshots/example.png)

---

## Analisis
uname -a adalah perintah di Linux yang digunakan untuk menampilkan semua informasi detail tentang sistem, termasuk nama kernel, nama mesin.
Perintah 1smod digunakan untuk menampilkan daftar modul kernel yang saat ini sedang dimuat (loaded) di sistem.

Modul kernel ini bisa berupa driver perangkat keras atau modul fungsional lainnya yang digunakan oleh kernel Linux Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS).

Hubungkan hasil dengan teori

Hasil dapat dihubungkan dengan fungsi kernel sebagai inti sistem operasi yang menjembatani hardware dan software; panggilan sistem ((syscall)) sebagai jembatan antara aplikasi pengguna dan kernel untuk meminta layanan; dan arsitektur OS yang mendefinisikan struktur ini, di mana kernel menjadi komponen sentral yang mengelola sumber daya melalui panggilan sistem.

Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?

Perbedaan hasil antara Linux dan Windows terlihat dari struktur sistem file (garis miring / di Linux vs "C:\ di Windows), cara penamaan berkas (bisa ada dua berkas dengan nama sama di direktori berbeda di Linux, tidak bisa di Windows), sistem partisi (Linux lebih fleksibel, Windows mendukung partisi Linux namun Linux belum tentu mendukung partisi Windows), dan penggunaan baris perintah (terminal di Linux lebih ampuh, cmd di Windows lebih terbatas
---

## Kesimpulan
Monolithic kernel adalah arsitektur sistem operasi di mana semua layanan inti OS, seperti manajemen memori, penjadwalan proses, dan manajemen perangkat keras, berjalan dalam satu ruang alamat (satu program besar) bagian dapat menyebabkan crash seluruh. Mikrokernel adalah jenis kernel sistem operasi yang hanya berisi fungsionalitas inti minimal, seperti manajemen memori dan komunikasi antarproses (IPC), sementara layanan lainnya (seperti driver perangkat dan sistem berkas) berjalan di ruang pengguna Arsitektur berlapis (layered architecture) adalah pola desain perangkat lunak yang membagi aplikasi menjadi beberapa lapisan terpisah, di mana setiap lapisan memiliki tanggung jawab tertentu dan hanya berinteraksi dengan lapisan di bawahnya, sebagai server terpisah.
---

## Quiz
1. [Pertanyaan 1]  
   **tuliskan 3 fungsi sistem operasi**
     Windows (untuk PC dan server), macOS (untuk perangkat Apple), Linux (sistem operasi open-source untuk berbagai perangkat), Android (untuk perangkat seluler), iOS (untuk perangkat Apple seluler), dan Chrome OS (ringan dan berorientasi web)
   
2. [Pertanyaan 2]  
   **jelaskan perbedan antara konel mode dan user mode**  
   tingkat akses dan hak istimewa yang dimiliki oleh prosesor. Mode pengguna menjalankan aplikasi standar dengan akses terbatas ke perangkat keras dan sumber daya sistem, sedangkan mode kernel menjalankan inti sistem operasi dengan kontrol penuh atas seluruh perangkat keras, memori, dan sumber daya sistem. Pemisahan ini sangat penting untuk menjaga stabilitas dan keamanan sistem, karena mode kernel mencegah aplikasi pengguna yang salah atau berbahaya merusak sistem
3. [Pertanyaan 3]  
   **sebutkan contoh os dan arsitektur monolonithic microkornel** 
   Arsitektur monolitik
Pada arsitektur monolitik, semua layanan sistem, seperti manajemen memori, proses, dan perangkat, diimplementasikan dalam satu ruang kernel yang besar dan tunggal. 
Linux: Salah satu contoh paling terkenal. Meskipun banyak modul dapat dimuat secara dinamis, kernelnya secara keseluruhan tetap bersifat monolitik.
Microsoft Windows (versi lama): Versi Windows seperti Windows 95, 98, dan Me menggunakan arsitektur monolitik.
DOS: Sistem operasi yang sangat sederhana dan monolitik, di mana semua fungsi intinya terintegrasi.
Solaris: Sistem operasi dari Sun Microsystems yang juga menggunakan kernel monolitik.
BSD: Berbagai varian sistem operasi BSD, seperti FreeBSD dan OpenBSD, menggunakan kernel monolitik. 

---

## Refleksi Diri
 masih kurang paham, masih susah semua?  angel pak tetap semangat konsisten 
  
---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
