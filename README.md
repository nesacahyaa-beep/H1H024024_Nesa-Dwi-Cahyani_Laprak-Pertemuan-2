# Laporan Tugas: Sistem Counter 7-Segment Arduino Percobaan 2A
Dokumen ini menjelaskan hasil percobaan rangkaian seven-segment display berbasis Arduino Uno, yang mencakup susunan rangkaian, prinsip kerja program, serta analisis kemungkinan kesalahan pada sistem.

# 1. Gambarkan rangkaian schematic yang digunakan pada percobaan! 
Pada percobaan ini digunakan 7-segment display tipe common cathode yang dikendalikan menggunakan Arduino Uno. Setiap segmen dihubungkan ke pin digital Arduino untuk mengatur tampilan angka.
Koneksi rangkaian:
Segmen a sampai g → Pin digital D2 sampai D8
Pin common (GND) → Ground Arduino melalui resistor 220Ω sebagai pembatas arus
Tombol increment (tambah) → Pin digital D9
Tombol decrement (kurang) → Pin digital D10

# 2.Mengapa pada push button digunakan mode INPUT_PULLUP pada Arduino Uno? Apa keuntungannya dibandingkan rangkaian biasa? 
Arduino menyediakan mode INPUT_PULLUP yang mengaktifkan resistor internal (sekitar 20kΩ–50kΩ) yang terhubung ke tegangan 5V.
Alasan penggunaan INPUT_PULLUP:
Jika pin input tidak menggunakan resistor pull-up atau pull-down, maka kondisi pin akan mengambang (floating). Kondisi ini menyebabkan pembacaan sinyal menjadi tidak stabil karena mudah terpengaruh noise listrik.
Keunggulan INPUT_PULLUP:
Tidak memerlukan resistor eksternal tambahan
Rangkaian menjadi lebih sederhana dan rapi
Membuat kondisi input lebih stabil
Logika kerja menjadi jelas:
Tidak ditekan = HIGH
Ditekan = LOW

# 3. Jika salah satu LED segmen tidak menyala, apa saja kemungkinan penyebabnya dari sisi hardware maupun software?
Jika salah satu segmen tidak menyala, maka kemungkinan penyebabnya dapat berasal dari dua sisi:
a. Faktor Hardware:
Kabel jumper tidak tersambung dengan baik atau putus
LED pada segmen tertentu mengalami kerusakan
Resistor tidak sesuai nilai atau pemasangan tidak benar
Kesalahan pemasangan pin (salah sambung antara Arduino dan display)
b. Faktor Software:
Penulisan pin pada program tidak sesuai dengan rangkaian
Urutan pola biner untuk angka tidak benar
Pin belum dikonfigurasi sebagai OUTPUT pada fungsi setup

# 4.Modifikasi rangkaian dan program dengan dua push button yang berfungsi sebagai penambahan (increment) dan pengurangan (decrement) pada sistem counter dan berikan penjelasan disetiap baris kode nya
Program berikut digunakan untuk menampilkan angka 0–9 pada 7-segment dengan kontrol dua tombol (tambah dan kurang).
Penjelasan Singkat Program:
Pin segmen disimpan dalam array
Tombol digunakan untuk mengubah nilai counter
Pola angka disimpan dalam bentuk array biner
Fungsi khusus digunakan untuk menampilkan angka ke display
Prinsip kerja:
Tombol ditekan → nilai counter berubah
Arduino membaca input tombol
Display diperbarui sesuai nilai counter
Delay digunakan untuk mencegah pembacaan ganda (debouncing)

# Laporan Tugas: Sistem Counter Up/Down 7-Segment Arduino Perobaan 1B
Dokumen ini menjelaskan pengembangan sistem counter berbasis Arduino Uno yang menggunakan dua tombol eksternal sebagai input untuk mengatur nilai angka yang ditampilkan pada 7-segment display.

# 1. Gambarkan rangkaian schematic yang digunakan pada percobaan! 
Pada percobaan ini, rangkaian sebelumnya dikembangkan dengan menambahkan dua tombol sebagai pengendali nilai counter. Pada bagian koneksi rangkaian, 7-segment display digunakan dengan pin segmen a hingga g yang dihubungkan ke pin digital Arduino D2 sampai D8, sedangkan pin common (katoda) dihubungkan ke GND melalui resistor sebagai pembatas arus. Untuk bagian input, digunakan dua tombol, yaitu tombol increment (+) yang dihubungkan ke pin digital D9 dan GND, serta tombol decrement (–) yang dihubungkan ke pin digital D10 dan GND. Sementara itu, pada bagian power supply, jalur VCC dan GND didistribusikan melalui breadboard power rail menggunakan kabel merah dan hitam untuk menyuplai seluruh komponen pada rangkaian.

# 2. Mengapa pada push button digunakan mode INPUT_PULLUP pada Arduino Uno? Apa keuntungannya dibandingkan rangkaian biasa? 
Arduino Uno memiliki resistor internal yang dapat diaktifkan melalui pemrograman. Fitur ini digunakan karena tombol membutuhkan referensi tegangan yang stabil agar dapat bekerja dengan benar. Dengan menggunakan mode INPUT_PULLUP, kondisi pin akan bernilai HIGH (5V) ketika tombol tidak ditekan, dan akan berubah menjadi LOW (0V) saat tombol ditekan karena terhubung langsung ke GND.Penggunaan INPUT_PULLUP memberikan beberapa keuntungan, yaitu tidak memerlukan resistor pull-up eksternal sehingga rangkaian menjadi lebih sederhana, mengurangi jumlah kabel pada breadboard sehingga lebih rapi dan tidak terlalu padat, serta meningkatkan kestabilan pembacaan input dengan meminimalkan gangguan sinyal (noise) dari lingkungan sekitar.

# 3. Jika salah satu LED segmen tidak menyala, apa saja kemungkinan penyebabnya dari sisi hardware maupun software? 
Jika terjadi kendala pada salah satu segmen, maka perlu dilakukan proses pengecekan berdasarkan beberapa kemungkinan penyebab berikut. Dari sisi hardware, masalah dapat terjadi akibat jumper yang longgar pada breadboard sehingga koneksi tidak stabil, yang dapat diatasi dengan menekan kembali atau mengganti kabel jumper. Selain itu, kesalahan pemasangan pin juga sering terjadi, misalnya kabel segmen ‘a’ tertukar dengan segmen ‘b’, sehingga perlu dilakukan pengecekan ulang sesuai datasheet 7-segment. Kerusakan juga dapat disebabkan oleh LED pada segmen yang terbakar akibat arus berlebih, sehingga solusinya adalah mengganti modul 7-segment dengan yang baru. Dari sisi software, gangguan dapat terjadi karena kesalahan indeks pada array digits, sehingga urutan logika 0 dan 1 harus dipastikan sesuai dengan jenis display yang digunakan (common cathode). Selain itu, masalah juga dapat muncul jika pin segmen belum dideklarasikan sebagai OUTPUT dalam program, sehingga perlu memastikan seluruh pin telah dikonfigurasi dengan benar menggunakan fungsi pinMode().

# 4. Modifikasi rangkaian dan program dengan dua push button yang berfungsi sebagai penambahan (increment) dan pengurangan (decrement) pada sistem counter dan berikan penjelasan disetiap baris kode nya 
Program ini mendefinisikan pin yang digunakan untuk mengontrol setiap segmen 7-segment serta dua tombol input sebagai pengatur nilai counter.
- Array segments[] digunakan untuk memetakan pin Arduino (D2–D8) ke masing-masing segmen display.
- Variabel btnUp dan btnDown digunakan untuk menentukan pin input tombol tambah dan kurang.
- Variabel count berfungsi sebagai penyimpan nilai angka yang sedang ditampilkan.
- numTable merupakan tabel dua dimensi yang menyimpan pola nyala (1) dan mati (0) untuk membentuk angka 0 sampai 9 pada 7-segment display tipe common cathode.

Proses Inisialisasi:
Pada fungsi setup(), seluruh pin segmen dikonfigurasi sebagai output, sedangkan pin tombol diatur menggunakan mode INPUT_PULLUP untuk memanfaatkan resistor internal Arduino. Setelah itu, tampilan awal diatur ke angka 0.

Cara Kerja Program:
Pada fungsi loop(), Arduino akan terus membaca status tombol:
= Jika tombol increment ditekan (logika LOW), maka nilai counter akan bertambah selama belum mencapai angka 9, kemudian tampilan diperbarui.
= Jika tombol decrement ditekan, maka nilai counter akan berkurang selama belum mencapai angka 0, lalu display diperbarui.

Untuk mencegah pembacaan ganda akibat getaran mekanis tombol (bounce), digunakan delay(200) sebagai metode debouncing sederhana. Selain itu, while(digitalRead(...) == LOW) memastikan perubahan angka hanya terjadi satu kali untuk setiap kali tombol ditekan.


