
# Laporan Praktikum Minggu [X]
Topik: Penjadwalan CPU – FCFS dan SJF

---

## Identitas
- **Nama**  : RIDHO YOGA YUWANA  
- **NIM**   : 250202963 
- **Kelas** : 1IKRA

---

## Tujuan
Setelah menyelesaikan tugas ini, mahasiswa mampu:

Menghitung waiting time dan turnaround time untuk algoritma FCFS dan SJF.
Menyajikan hasil perhitungan dalam tabel yang rapi dan mudah dibaca.
Membandingkan performa FCFS dan SJF berdasarkan hasil analisis.
Menjelaskan kelebihan dan kekurangan masing-masing algoritma.
Menyimpulkan kapan algoritma FCFS atau SJF lebih sesuai digunakan.

---

## Dasar Teori
1. Penjadwalan CPU (CPU Scheduling)
Penjadwalan CPU adalah proses pemilihan urutan eksekusi proses oleh sistem operasi untuk memaksimalkan penggunaan CPU dan meminimalkan waktu tunggu.

2. First Come First Served (FCFS)
FCFS mengeksekusi proses berdasarkan urutan kedatangan. Sederhana dan adil, tetapi dapat menyebabkan convoy effect karena proses pendek menunggu proses panjang selesai.

3. Shortest Job First (SJF)
SJF memilih proses dengan waktu eksekusi terpendek terlebih dahulu. Memberikan waktu tunggu rata-rata paling rendah, namun sulit diterapkan karena memerlukan estimasi burst time dan berpotensi menyebabkan starvation pada proses panjang.

---

## Langkah Praktikum
1. **Siapkan Data Proses**
   Gunakan tabel proses berikut sebagai contoh (boleh dimodifikasi dengan data baru):
   | Proses | Burst Time | Arrival Time |
   |:--:|:--:|:--:|
   | P1 | 6 | 0 |
   | P2 | 8 | 1 |
   | P3 | 7 | 2 |
   | P4 | 3 | 3 |

2. **Eksperimen 1 – FCFS (First Come First Served)**
   - Urutkan proses berdasarkan *Arrival Time*.  
   - Hitung nilai berikut untuk tiap proses:
     ```
     Waiting Time (WT) = waktu mulai eksekusi - Arrival Time
     Turnaround Time (TAT) = WT + Burst Time
     ```
   - Hitung rata-rata Waiting Time dan Turnaround Time.  
   - Buat Gantt Chart sederhana:  
     ```
     | P1 | P2 | P3 | P4 |
     0    6    14   21   24
     ```

3. **Eksperimen 2 – SJF (Shortest Job First)**
   - Urutkan proses berdasarkan *Burst Time* terpendek (dengan memperhatikan waktu kedatangan).  
   - Lakukan perhitungan WT dan TAT seperti langkah sebelumnya.  
   - Bandingkan hasil FCFS dan SJF pada tabel berikut:

     | Algoritma | Avg Waiting Time | Avg Turnaround Time | Kelebihan | Kekurangan |
     |------------|------------------|----------------------|------------|-------------|
     | FCFS | ... | ... | Sederhana dan mudah diterapkan | Tidak efisien untuk proses panjang |
     | SJF | ... | ... | Optimal untuk job pendek | Menyebabkan *starvation* pada job panjang |

4. **Eksperimen 3 – Visualisasi Spreadsheet (Opsional)**
   - Gunakan Excel/Google Sheets untuk membuat perhitungan otomatis:
     - Kolom: Arrival, Burst, Start, Waiting, Turnaround, Finish.
     - Gunakan formula dasar penjumlahan/subtraksi.
   - Screenshot hasil perhitungan dan simpan di:
     ```
     praktikum/week5-scheduling-fcfs-sjf/screenshots/
     ```

5. **Analisis**
   - Bandingkan hasil rata-rata WT dan TAT antara FCFS & SJF.  
   - Jelaskan kondisi kapan SJF lebih unggul dari FCFS dan sebaliknya.  
   - Tambahkan kesimpulan singkat di akhir laporan.

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 5 - CPU Scheduling FCFS & SJF"
   git push origin main
   ```

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
Berdasarkan hasil simulasi, algoritma SJF menghasilkan kinerja yang sedikit lebih baik dibanding FCFS, karena mampu meminimalkan waktu tunggu (WT) dan turnaround time (TAT) rata-rata.
Secara teori, SJF memang dirancang untuk meminimalkan waktu tunggu rata-rata, walaupun lebih sulit diterapkan secara real-time karena harus mengetahui burst time setiap proses sebelumnya.

1. Kondisi di mana SJF lebih unggul dari FCFS

Algoritma SJF (Shortest Job First) akan lebih unggul dan efisien ketika sistem memiliki proses dengan variasi burst time yang cukup besar, artinya ada proses dengan waktu eksekusi yang sangat singkat dan ada yang cukup panjang. Dalam situasi seperti ini, SJF dapat menurunkan rata-rata waktu tunggu (Waiting Time) dan waktu penyelesaian (Turnaround Time) karena proses-proses yang lebih pendek diselesaikan terlebih dahulu, sehingga antrian proses tidak tertahan oleh proses yang panjang.
Selain itu, SJF juga sangat efektif pada sistem batch processing atau sistem yang burst time-nya sudah diketahui sebelumnya, seperti pada simulasi atau sistem non-interaktif. Dengan begitu, sistem dapat mengatur urutan proses dengan tepat untuk mendapatkan efisiensi maksimal. Secara umum, SJF memberikan kinerja terbaik dalam hal minimasi waktu tunggu rata-rata dan meningkatkan throughput sistem.

2. Kondisi di mana FCFS lebih unggul dari SJF

Sebaliknya, algoritma FCFS (First Come First Served) lebih unggul dan sesuai digunakan pada sistem yang sederhana, di mana setiap proses diperlakukan secara adil berdasarkan urutan kedatangan tanpa memperhatikan lama waktu eksekusi. FCFS lebih cocok untuk lingkungan interaktif atau sistem real-time yang menuntut keadilan (fairness) dan kepastian urutan eksekusi.
FCFS juga lebih mudah diimplementasikan karena tidak memerlukan informasi tambahan seperti burst time proses. Pada kondisi di mana seluruh proses memiliki burst time yang hampir sama, maka performa FCFS dan SJF akan relatif setara, sehingga FCFS menjadi pilihan praktis dengan kompleksitas rendah.

Namun, perlu diperhatikan bahwa FCFS memiliki kelemahan utama, yaitu kondisi ketika proses dengan burst time panjang datang lebih awal dan membuat proses-proses lain menunggu terlalu lama. Dalam situasi ini, SJF jelas lebih efisien.


---

## Kesimpulan
SJF lebih unggul saat sistem memiliki proses dengan variasi burst time yang besar dan burst time diketahui sebelumnya, karena mampu meminimalkan waktu tunggu rata-rata.
Sedangkan FCFS lebih unggul pada sistem sederhana yang membutuhkan keadilan urutan eksekusi dan tidak memerlukan pengetahuan tentang burst time setiap proses.

## Quiz
Tuliskan jawaban di bagian **Quiz** pada laporan:
1. Apa perbedaan utama antara FCFS dan SJF?
   
   **Jawaban :**

   Pada FCFS, proses dieksekusi berdasarkan urutan kedatangannya. Artinya, proses yang datang lebih dulu akan dijalankan terlebih
   dahulu tanpa memperhatikan lama waktu eksekusinya. Algoritma ini sederhana, tetapi bisa menyebabkan proses yang memiliki waktu
   eksekusi singkat menunggu lama jika ada proses panjang datang lebih dulu.
   Sedangkan pada SJF, proses dijalankan berdasarkan waktu eksekusi yang paling pendek terlebih dahulu. Jadi, proses yang membutuhkan
   waktu paling sedikit akan diprioritaskan. Cara ini membuat waktu tunggu rata-rata menjadi lebih kecil dan sistem menjadi lebih
   efisien. Namun, kekurangannya adalah sulit diterapkan karena waktu eksekusi setiap proses harus diketahui terlebih dahulu.

3. Mengapa SJF dapat menghasilkan rata-rata waktu tunggu minimum?
   
   **Jawaban :**
   SJF menghasilkan waktu tunggu rata-rata paling kecil karena proses dengan waktu eksekusi paling singkat dikerjakan lebih dulu,
   sehingga proses-proses cepat tidak perlu menunggu lama di belakang proses yang panjang.
   
5. Apa kelemahan SJF jika diterapkan pada sistem interaktif?

   **Jawaban :**
   
   SFJ tidak cocok untuk lingkungan yang membutuhkan respon cepat dan waktu kedatangan proses yang tidak pasti.
   Contohnya :

   - Sulit mengetahui waktu eksekusi (burst time) setiap proses di awal, padahal SJF membutuhkannya untuk menentukan prioritas.
   - Proses panjang bisa terus tertunda (starvation) jika selalu ada proses baru yang lebih pendek datang.
   - Tidak responsif terhadap permintaan pengguna secara langsung, karena proses yang baru datang bisa harus menunggu proses lain selesai.

---


## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?

  Lumayan mengalami kesulitan dalam menghitung WT dan TAT karena lumayan membingungkan.
- Bagaimana cara Anda mengatasinya?

  Mengulang dan mencoba terus proses penghitungannya, dan latihan dengan skenario yang berbeda
**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
