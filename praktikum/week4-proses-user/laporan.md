
# Laporan Praktikum Minggu [X]
Topik: [Tuliskan judul topik, misalnya "Arsitektur Sistem Operasi dan Kernel"]

---

## Identitas
- **Nama**  : RIDHO YOGA YUWANA
- **NIM**   : 250202963  
- **Kelas** : 1IKRA

---

## Tujuan
Tuliskan tujuan praktikum minggu ini.  
Setelah menyelesaikan tugas ini, mahasiswa mampu:
1. Menjelaskan konsep proses dan user dalam sistem operasi Linux.  
2. Menampilkan daftar proses yang sedang berjalan dan statusnya.  
3. Menggunakan perintah untuk membuat dan mengelola user.  
4. Menghentikan atau mengontrol proses tertentu menggunakan PID.  
5. Menjelaskan kaitan antara manajemen user dan keamanan sistem. 

---

## Dasar Teori
1. Konsep Proses dalam Sistem Operasi
2. Manajemen Proses oleh Sistem Operasi
3. Monitoring Proses
4. Kontrol dan Terminasi Proses
5. Peran User dan Hak Akses
---

## Langkah Praktikum
1. **Setup Environment**
   - Gunakan Linux (Ubuntu/WSL).  
   - Pastikan Anda sudah login sebagai user non-root.  
   - Siapkan folder kerja:
     ```
     praktikum/week4-proses-user/
     ```

2. **Eksperimen 1 – Identitas User**
   Jalankan perintah berikut:
   ```bash
   whoami
   id
   groups
   ```
   - Jelaskan setiap output dan fungsinya.  
   - Buat user baru (jika memiliki izin sudo):
     ```bash
     sudo adduser praktikan
     sudo passwd praktikan
     ```
   - Uji login ke user baru.

3. **Eksperimen 2 – Monitoring Proses**
   Jalankan:
   ```bash
   ps aux | head -10
   top -n 1
   ```
   - Jelaskan kolom penting seperti PID, USER, %CPU, %MEM, COMMAND.  
   - Simpan tangkapan layar `top` ke:
     ```
     praktikum/week4-proses-user/screenshots/top.png
     ```

4. **Eksperimen 3 – Kontrol Proses**
   - Jalankan program latar belakang:
     ```bash
     sleep 1000 &
     ps aux | grep sleep
     ```
   - Catat PID proses `sleep`.  
   - Hentikan proses:
     ```bash
     kill <PID>
     ```
   - Pastikan proses telah berhenti dengan `ps aux | grep sleep`.

5. **Eksperimen 4 – Analisis Hierarki Proses**
   Jalankan:
   ```bash
   pstree -p | head -20
   ```
   - Amati hierarki proses dan identifikasi proses induk (`init`/`systemd`).  
   - Catat hasilnya dalam laporan.

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 4 - Manajemen Proses & User"
   git push origin main
   ```
---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
 ```bash
   whoami
   id
   groups
   ```
 ```bash
     sudo adduser praktikan
     sudo passwd praktikan
 ```
 ```bash
   ps aux | head -10
   top -n 1
   ```
```bash
     sleep 1000 &
     ps aux | grep sleep
```
 ```bash
     kill <PID>
 ```
 ```bash
   pstree -p | head -20
 ```
---


## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
<img width="1920" height="1080" alt="idoyy week 4 (2)" src="https://github.com/user-attachments/assets/929bdcd2-d250-4942-85b0-b0eea7e8457a" />
<img width="824" height="977" alt="idoyy week 4" src="https://github.com/user-attachments/assets/ab7d3fa5-5d26-43df-8e63-3a3f2f58625a" />

---

## Analisis
Dari hasil percobaan yang telah dilakukan, dapat dipahami bahwa setiap aktivitas di sistem operasi Linux dijalankan sebagai suatu proses yang memiliki identitas unik berupa PID (Process ID). Melalui perintah seperti ps, top, dan pstree, pengguna dapat memantau status, hierarki, serta penggunaan sumber daya dari setiap proses yang berjalan. Selain itu, dengan perintah sleep dan kill, pengguna juga dapat membuat, memantau, atau menghentikan proses secara langsung. Hasil ini menunjukkan bahwa Linux memiliki sistem multitasking yang efisien dan terstruktur, di mana setiap proses dapat dijalankan secara paralel tanpa saling mengganggu. Dengan adanya informasi seperti USER, %CPU, dan %MEM, pengguna dapat memahami bagaimana sistem mengalokasikan sumber daya untuk setiap proses.

Hasil percobaan ini berkaitan erat dengan teori dasar tentang fungsi kernel dan system call dalam arsitektur sistem operasi. Kernel berperan sebagai inti sistem yang bertugas untuk mengelola proses, memori, dan komunikasi antar-proses. Ketika pengguna menjalankan perintah melalui shell, kernel akan memanggil system call seperti fork() dan exec() untuk membuat dan mengeksekusi proses baru. Hal ini menunjukkan bahwa ada interaksi langsung antara user space (tempat perintah dijalankan) dengan kernel space (tempat kernel bekerja). Arsitektur Linux yang berlapis (layered architecture) memisahkan kedua ruang tersebut agar sistem tetap stabil dan aman. Dengan demikian, percobaan ini membuktikan bagaimana perintah sederhana di terminal sebenarnya merupakan bagian dari mekanisme yang lebih dalam antara shell, kernel, dan manajemen proses di sistem operasi.

Perbedaan hasil di lingkungan OS berbeda (Linux vs Windows) :

| Aspek                     | Linux                                                                 | Windows                                                                               |
| ------------------------- | --------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| **Manajemen Proses**      | Menggunakan perintah terminal (`ps`, `top`, `kill`, `pstree`).        | Menggunakan GUI (Task Manager) dan CLI (`tasklist`, `taskkill`).                      |
| **Struktur Hierarki**     | Memiliki *parent-child process tree*, berawal dari `systemd (PID 1)`. | Menggunakan *Process Manager*, tetapi hierarki tidak selalu ditampilkan secara jelas. |
| **System Call**           | Terbuka dan dapat diakses melalui shell, fleksibel untuk scripting.   | Lebih tertutup dan dikontrol oleh kernel secara internal.                             |
| **Interaksi User–Kernel** | Terjadi langsung melalui shell berbasis teks.                         | Lebih sering melalui antarmuka grafis (GUI).                                          |


## Kesimpulan

1. Dari hasil praktikum, dapat disimpulkan bahwa setiap aktivitas yang terjadi di sistem operasi Linux dikelola dalam bentuk proses dengan identitas unik (PID), yang dapat dipantau dan dikontrol menggunakan perintah seperti ps, top, kill, dan pstree.

2. Linux memiliki struktur hierarki proses yang jelas, di mana seluruh proses berasal dari proses induk utama systemd (PID 1). Hal ini menunjukkan cara kerja sistem operasi dalam mengatur komunikasi dan ketergantungan antar-proses secara efisien.

3. Melalui percobaan ini juga terbukti bahwa kernel berperan sebagai pengendali utama sistem, menghubungkan perintah pengguna (user space) dengan eksekusi nyata proses (kernel space) melalui mekanisme system call.

---

## Quiz
Tuliskan jawaban di bagian **Quiz** pada laporan:
1. Apa fungsi dari proses `init` atau `systemd` dalam sistem Linux?
   
   **Jawaban :**

Fungsinya adalah untuk:

1. Menginisialisasi sistem, seperti menyiapkan lingkungan kernel dan memulai layanan penting.

2. Menjalankan dan mengelola semua proses lain, termasuk servis background (daemon).

3. Mengatur urutan startup dan shutdown sistem secara terkoordinasi.
   
2. Apa perbedaan antara `kill` dan `killall`?

   **Jawaban :**
   
   | Perintah      | Fungsi Utama                                                                         | Target                           | Contoh Penggunaan | Keterangan                                            |
| ------------- | ------------------------------------------------------------------------------------ | -------------------------------- | ----------------- | ----------------------------------------------------- |
| **`kill`**    | Mengirim sinyal (biasanya untuk menghentikan) ke **proses tertentu berdasarkan PID** | Berdasarkan **PID (Process ID)** | `kill 1234`       | Menghentikan proses dengan PID 1234 saja              |
| **`killall`** | Mengirim sinyal ke **semua proses dengan nama tertentu**                             | Berdasarkan **nama proses**      | `killall firefox` | Menghentikan semua proses bernama “firefox” sekaligus |

3. Mengapa user `root` memiliki hak istimewa di sistem Linux?

   **Jawaban :**
   
   User root adalah penguasa tertinggi dalam sistem Linux, dirancang untuk melakukan tugas administrasi dan pemeliharaan yang tidak boleh dilakukan oleh pengguna biasa demi keamanan dan kontrol penuh terhadap sistem.


---


## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?

  Bagian yang paling menantang minggu ini adalah memahami hubungan antarproses dan cara kerja perintah seperti ps, pstree, dan kill, karena membutuhkan pemahaman tentang bagaimana sistem Linux mengelola proses secara hierarkis.
  
- Bagaimana cara Anda mengatasinya?
  
  Saya mengatasinya dengan membaca dokumentasi perintah menggunakan man, mencoba menjalankan perintah satu per satu di terminal, serta membandingkan hasilnya agar lebih memahami fungsi dan efek setiap perintah secara langsung.

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
