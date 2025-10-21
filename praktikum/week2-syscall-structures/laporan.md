
# Laporan Praktikum Minggu [X]
Topik: [Tuliskan judul topik, misalnya "Arsitektur Sistem Operasi dan Kernel"]

---

## Identitas
- **Nama**  : Naufal Adib Bissibyan
- **NIM**   :  
- **Kelas** : 1IKRA

---

## Tujuan
Setelah menyelesaikan tugas ini, mahasiswa mampu:

Menjelaskan konsep dan fungsi system call dalam sistem operasi.
Mengidentifikasi jenis-jenis system call dan fungsinya.
Mengamati alur perpindahan mode user ke kernel saat system call terjadi.
Menggunakan perintah Linux untuk menampilkan dan menganalisis system call.

---

## Dasar Teori
System Call sebagai Antarmuka antara User dan Kernel System call merupakan mekanisme yang memungkinkan program di user space berinteraksi dengan kernel untuk mengakses sumber daya sistem seperti file, memori, dan perangkat keras. Tanpa system call, program user tidak dapat melakukan operasi penting seperti membaca file atau membuat proses baru.

Kernel bertanggung jawab untuk mengatur alokasi sumber daya seperti CPU, memori, dan perangkat I/O. Ketika program user membutuhkan sumber daya tersebut, kernel akan menangani permintaan melalui system call agar proses tetap terkontrol dan tidak saling mengganggu.

Alur Eksekusi System Call Saat sebuah program memanggil system call (misalnya read()), CPU akan beralih dari user mode ke kernel mode. Kernel kemudian mengeksekusi fungsi yang diminta, mengembalikan hasilnya ke program, dan berpindah kembali ke user mode setelah selesai.

Keamanan dan Isolasi Proses Salah satu tujuan utama penggunaan system call adalah menjaga keamanan sistem. Dengan membatasi akses langsung ke kernel, sistem operasi dapat mencegah kesalahan program atau serangan berbahaya yang dapat merusak data atau mengganggu proses lain.



---

## Langkah Praktikum
Setup Environment

Gunakan Linux (Ubuntu/WSL).
Pastikan perintah strace dan man sudah terinstal.
Konfigurasikan Git (jika belum dilakukan di minggu sebelumnya).
Eksperimen 1 – Analisis System Call Jalankan perintah berikut:

strace ls
Catat 5–10 system call pertama yang muncul dan jelaskan fungsinya.
Simpan hasil analisis ke results/syscall_ls.txt.

Eksperimen 2 – Menelusuri System Call File I/O Jalankan:

strace -e trace=open,read,write,close cat /etc/passwd
Analisis bagaimana file dibuka, dibaca, dan ditutup oleh kernel.

Eksperimen 3 – Mode User vs Kernel Jalankan:

dmesg | tail -n 10
Amati log kernel yang muncul. Apa bedanya output ini dengan output dari program biasa?

Diagram Alur System Call

Buat diagram yang menggambarkan alur eksekusi system call dari program user hingga kernel dan kembali lagi ke user mode.
Gunakan draw.io / mermaid.
Simpan di:
praktikum/week2-syscall-structure/screenshots/syscall-diagram.png
Commit & Push

git add .
git commit -m "Minggu 2 - Struktur System Call dan Kernel Interaction"
git push origin main
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
![Screenshot hasil](screenshots/Screenshotnopalstracels2.png)

---

## Analisis
Pentingnya System Call untuk Keamanan Sistem Operasi System call merupakan jembatan utama antara user space dan kernel space dalam sistem operasi. Tanpa adanya system call, program pengguna tidak akan bisa berinteraksi dengan sumber daya sistem seperti file, memori, atau perangkat keras. Namun, karena kernel memiliki hak istimewa tertinggi dalam sistem, maka setiap interaksi dari program pengguna ke kernel harus dilakukan secara hati-hati dan terkontrol. Inilah sebabnya system call berperan sangat penting dalam menjaga keamanan sistem operasi.

Pertama, system call memastikan bahwa proses pengguna tidak dapat mengakses langsung sumber daya kritis milik kernel. Semua permintaan dari aplikasi harus melalui API system call, di mana kernel akan memverifikasi izin dan konteks eksekusi sebelum mengeksekusi perintah. Misalnya, ketika sebuah proses mencoba membuka file menggunakan open(), kernel akan memeriksa hak akses pengguna terhadap file tersebut. Jika tidak memiliki izin, kernel akan menolak permintaan dengan mengembalikan kode kesalahan seperti EACCES. Dengan mekanisme ini, system call berfungsi sebagai lapisan keamanan yang mencegah penyalahgunaan sumber daya sistem, baik secara sengaja maupun tidak sengaja.

Kedua, keamanan juga dijaga melalui mekanisme transisi antara user mode dan kernel mode. Dalam arsitektur sistem operasi modern seperti Linux, terdapat dua mode utama eksekusi: user mode dan kernel mode. Saat sebuah program memanggil system call, prosesor akan beralih dari user mode ke kernel mode menggunakan instruksi khusus (seperti syscall atau int 0x80). Transisi ini penting karena di kernel mode, sistem memiliki akses penuh ke seluruh memori dan perangkat keras. Setelah perintah kernel selesai dijalankan, kontrol dikembalikan ke program di user mode.

Untuk memastikan proses transisi ini aman, sistem operasi menerapkan proteksi memori dan validasi parameter. Kernel memeriksa apakah data atau alamat memori yang diterima dari aplikasi berada di ruang memori pengguna dan bukan di area kernel. Jika ditemukan pelanggaran, sistem akan menghentikan proses tersebut untuk mencegah kebocoran atau kerusakan data. Selain itu, sistem juga menggunakan tabel khusus seperti System Call Table yang berisi daftar fungsi yang boleh diakses oleh user space. Dengan cara ini, hanya system call yang sah yang dapat dipanggil, sehingga mencegah eksekusi kode berbahaya di dalam kernel.

Contoh system call yang sering digunakan dalam sistem operasi Linux antara lain: • open() dan close() untuk membuka dan menutup file. • read() dan write() untuk membaca serta menulis data ke file atau perangkat. • fork() untuk membuat proses baru. • execve() untuk mengeksekusi program baru. • wait() untuk menunggu proses anak selesai. • exit() untuk mengakhiri proses dengan aman. • getpid() dan kill() untuk mengatur proses melalui ID-nya.



## Kesimpulan
System call berperan penting sebagai penghubung antara program pengguna dan kernel dalam sistem operasi. Melalui system call, program dapat meminta layanan seperti membuka file, membaca data, membuat proses baru, dan mengakses perangkat dengan aman tanpa langsung berinteraksi dengan kernel. Praktikum menggunakan perintah strace membantu memahami bagaimana kernel menangani setiap panggilan system call yang terjadi saat program dijalankan, sedangkan dmesg menunjukkan aktivitas dan pesan yang dicatat langsung oleh kernel. Selain itu, percobaan ini juga menunjukkan pentingnya mekanisme user mode dan kernel mode dalam menjaga keamanan serta kestabilan sistem. Dengan demikian, system call menjadi komponen krusial dalam pengelolaan sumber daya dan pengendalian akses pada sistem operasi Linux.


---

## Quiz
1.Apa fungsi utama system call dalam sistem operasi?
Jawaban: Fungsi utama system call adalah sebagai penghubung antara program pengguna (user space) dengan kernel (system space) agar aplikasi dapat meminta layanan dari sistem operasi seperti membaca atau menulis file, mengalokasikan memori, membuat proses baru, atau berkomunikasi dengan perangkat keras. System call memungkinkan interaksi ini dilakukan dengan aman dan terkontrol tanpa memberi akses langsung kepada user terhadap sumber daya kernel.

2. Sebutkan 4 kategori system call yang umum digunakan.
Jawaban: Empat kategori utama system call yang umum digunakan dalam sistem operasi adalah: 1. Process Control – untuk membuat, menghentikan, dan mengatur proses (contoh: fork(), execve(), exit(), wait()). 2. File Management – untuk operasi file seperti membuka, membaca, menulis, atau menutup file (contoh: open(), read(), write(), close()). 3. Device Management – untuk mengontrol dan mengakses perangkat input/output (contoh: ioctl(), read(), write()). 4. Information Maintenance – untuk mendapatkan atau mengatur informasi sistem (contoh: getpid(), uname(), gettimeofday()).

3. Mengapa system call tidak bisa dipanggil langsung oleh user program? Jawaban: System call tidak dapat dipanggil langsung oleh program pengguna karena berjalan di tingkat kernel (privileged mode), sedangkan program biasa berjalan di user mode. Hal ini bertujuan untuk menjaga keamanan dan stabilitas sistem operasi, agar pengguna tidak bisa mengakses atau mengubah sumber daya kernel secara langsung yang dapat menyebabkan kerusakan sistem, kebocoran data, atau crash. Oleh karena itu, program hanya dapat memanggil system call melalui antarmuka API yang disediakan oleh sistem operasi (misalnya pustaka C glibc di Linux).
---

## Refleksi Diri
Tuliskan secara singkat:
- berusaha belajar lebih sungguh sungguh
- bergaul dengan teman teman yang baik

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
